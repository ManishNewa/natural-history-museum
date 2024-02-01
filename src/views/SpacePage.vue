<template>
    <div class="space-page">

        <h1 class="space-page__title">
            Space
        </h1>
        <!-- Add the museum highlight cards based on the data provided below -->

        <div class="cards-container">
            <div class="cards-container__cards">
                <MuseumHighlight v-for="celestialData in ascCelestialData" :data="celestialData" :key="celestialData.name">
                    <template #card-badge>
                        <svg xmlns="http://www.w3.org/2000/svg"
                            viewBox="0 0 576 512"><!--!Font Awesome Free 6.5.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.-->
                            <path fill="#FFD43B"
                                d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z" />
                        </svg>
                    </template>
                    <!-- Quiz button -->
                    <template #action-btns>
                        <div v-if="celestialData.quiz">
                            <a :href="celestialData.quiz" target="_blank">
                                <button class="quiz-btn">Quiz</button>
                            </a>
                        </div>
                    </template>
                </MuseumHighlight>
            </div>
        </div>
    </div>
</template>

<script>

import MuseumHighlight from '../components/MuseumHighlight.vue';

export default {
    name: 'SpacePage',
    components: {
        MuseumHighlight,
    },
    mixins: [
    ],
    props: {

    },
    data() {
        return {
            spaceHighlights: [
                {
                    date: '2020-04-20 12:20:00',
                    description: 'Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.',
                    id: 1,
                    image: '',
                    name: 'Asteroids',
                },
                {
                    date: '2020-05-20 15:50:00',
                    description: 'A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.',
                    id: 9,
                    image: '',
                    name: 'Comets',
                },
                {
                    date: '2020-05-01 9:22:00',
                    description: 'The term planet is ancient, with ties to history, astrology, science, mythology, and religion.',
                    id: 7,
                    image: '',
                    name: 'Planets',
                    news: {
                        date: '2020-08-18 18:00:00',
                        title: 'Attend our talk about Jupiter with Dr. Hogarth',
                    },
                    quiz: 'https://planetquiz.space',
                },
                {
                    date: '2020-07-05 4:10:00',
                    description: 'A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.',
                    id: 12,
                    image: '',
                    name: 'Meteor showers',
                    news: {
                        title: 'The Lyrids will peak at on April 21-22 2021, at night',
                    },
                },
            ],
            spacePartners: {
                observatory: {
                    createdAt: '2020-06-01 11:45:00',
                    info: 'The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.',
                    image: '',
                    name: 'Mauna Kea Observatories',
                },
            },
        };
    },
    computed: {
        // Combined data in ascending order of date
        // spacePartners atm is Object array but could be normal array as well
        ascCelestialData() {
            return [
                ...this.spaceHighlights,
                ...(Array.isArray(this.spacePartners)
                    ? this.spacePartners.map(data => ({
                        ...data,
                        isPartner: true,
                        description: data.info,
                        date: data.createdAt,
                    }))
                    : Object.values(this.spacePartners).map(data => ({
                        ...data,
                        isPartner: true,
                        description: data.info,
                        date: data.createdAt,
                    })))
            ].sort((a, b) => {
                return new Date(b.date) - new Date(a.date)
            })
        }
    },
    methods: {

    },
    created() {

    },
};
</script>

<style lang="scss" scoped>
.space-page {
    margin: 50px 40px;

    &__title {
        color: #000;
        font-size: 50px;
        font-weight: 200;
    }
}

.cards-container {
    &__cards {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
        gap: 30px;
        padding: 50px 0
    }
}

.quiz-btn {
    display: inline-block;
    padding: 10px 20px;
    margin-top: 15px;
    font-size: 1rem;
    color: #fff;
    background-color: #14b8a6;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;

    &:hover {
        background-color: #0d9488;
    }
}
</style>
