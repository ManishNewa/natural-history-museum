<template>
    <div class="museum-highlight">
        <div class="card" :class="{ 'partner-card': data.isPartner }">
            <!-- Badge -->
            <CardBadge>
                <slot name="card-badge" />
            </CardBadge>
            <!-- Image -->
            <div class="card__image-container">
                <span v-if="imageLoading" class="card__image-refresh">
                    <i class="fa-solid fa-spinner"></i>&nbsp;
                    Refreshing...</span>
                <img v-else :src="imageUrl" :alt="`${data.name.toLowerCase()} image`">
            </div>
            <div class="card__title">
                {{ data.name }}
            </div>
            <!-- Content -->
            <div class="card__contents">
                <span>
                    <p>{{ data.description }}</p>
                </span>
                <!-- Only show if there is news in data -->
                <div v-if="data.news" class="card__contents__news">
                    <div class="title">
                        News
                    </div>
                    <ul>
                        <li>{{ data.news.title }}</li>
                    </ul>
                </div>
                <!--slot For Extra information  -->
                <div class="card__extra-info">
                    <Slot name="info" />
                </div>
            </div>
            <!-- Buttons/Actions -->
            <div class="card__action-btns">
                <slot name="action-btns" />
                <button class="card__refresh-btn" @click="refreshImage">Refresh Image</button>
            </div>
        </div>
    </div>
</template>

<script>
import CardBadge from './CardBadge.vue';

export default {
    name: 'MuseumHighlight',
    components: {
        CardBadge
    },
    mixins: [
    ],
    props: {
        data: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            imageLoading: false,
            refreshedImageUrl: null,
        };
    },
    computed: {
        newsDate() {
            // Highlight's news item date
            return this.data.date
        },
        imageUrl() {
            return this.data.image || this.refreshedImageUrl || `/images/${this.data.name.toLowerCase()}.jpg`
        }
    },
    methods: {
        async refreshImage() {
            // Fetch a new image for the highlight
            try {
                this.imageLoading = true;
                const response = await fetch(`https://source.unsplash.com/featured/${this.data.name}`);
                // To avoid props mutation we will use a separate variable for refreshed image url
                this.refreshedImageUrl = response.url;
            } catch (error) {
                console.log('Error refreshing image', error?.data?.message)
            } finally {
                this.imageLoading = false;
            }
        },
    },
    created() {

    },
};
</script>

<style lang="scss" scoped>
.museum-highlight {
    position: relative;

    .card {
        display: flex;
        flex-direction: column;
        height: 100%;
        color: #334155;
        background: #ffffff;
        box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px -1px rgba(0, 0, 0, 0.1);
        border-radius: 10px;
        padding: 20px;
        transition: all 0.4s ease-in-out;

        &:hover {
            transform: translateY(-10px);
        }

        &__image-container {
            position: relative;
            height: 250px;
            overflow: hidden;

            img {
                width: 100%;
                height: inherit;
                object-fit: cover;
                transition: all 0.4s ease-in-out;
            }

            &:hover {
                img {
                    transform: scale(1.2);
                }
            }
        }

        &__image-refresh {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100%;
        }

        &__title {
            font-size: 20px;
            padding: 10px 0;
            letter-spacing: 1.1px;
            width: calc(100% - 20px);
        }

        &__contents {
            line-height: 30px;
            padding: 8px 8px 12px 0;

            &__news {
                .title {
                    letter-spacing: 2px;
                    font-size: 18px;
                    font-weight: 700;
                }

                ul {
                    margin: 5px 20px;
                }
            }
        }

        &__action-btns {
            display: flex;
            justify-content: center;
            gap: 12px;
            margin-top: auto;
        }

        &__refresh-btn {
            display: inline-block;
            padding: 10px 20px;
            margin-top: 15px;
            font-size: 1rem;
            color: #ffffff;
            background: #020617;
            border: 1px solid #020617;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.3s ease;

            &:hover {
                background: #1e293b;
                color: #ffffff;
                border-color: #1e293b;
            }

            &:active {
                background: #0f161c;
                border-color: #0f161c;
                color: #ffffff;
            }
        }
    }

    .partner-card {
        background: #f5f5f5;
    }
}
</style>
