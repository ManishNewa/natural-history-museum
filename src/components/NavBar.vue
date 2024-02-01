<template>
    <div class="nav">
        <div class="nav__title">
            <span class="nav__title__logo"><i class="fa-solid fa-earth-americas"></i></span>
            <p class="nav__title__text">Natural History Museum</p>
        </div>
        <nav class="nav-menu">
            <input type="checkbox" id="navToggle" class="nav-menu__toggle-input">
            <label for="navToggle" class="nav-menu__toggle-btn">
                <i class="fa fa-bars"></i>
            </label>

            <div class="nav-menu__overlay">
                <ul class="nav-menu__overlay__links">
                    <li><a href="#">Dinosaurs</a></li>
                    <li><a href="#" class="nav-menu__overlay__links__active">Space</a></li>
                    <li><a href="#">Oceans</a></li>
                    <li><a href="#">Wildlife</a></li>
                </ul>
            </div>
        </nav>
    </div>
</template>
  
<script>
export default {
    name: 'MyComponent',
};
</script>
  
<style lang="scss" scoped>
.nav {
    background: #fff;
    overflow: auto;

    &__title {
        color: #fff;
        background: #0a0a2a;
        display: flex;
        align-items: center;
        gap: 20px;
        height: 84px;
        padding-left: 50px;

        &__logo {
            font-size: 48px;
        }
        &__text{
            font-size: 24px;
        }
    }
}

.nav-menu {
    &__toggle-input {
        display: none;

        &:checked~.nav-menu__overlay {
            clip-path: circle(75%);
            z-index: 1;
        }

        &:checked~.nav-menu__toggle-btn {
            background: #fff;
            color: #4158d0;

            i:before {
                content: '\f00d';
            }
        }
    }

    &__toggle-btn {
        position: fixed;
        z-index: 2;
        right: 20px;
        top: 20px;
        height: 50px;
        width: 50px;
        text-align: center;
        line-height: 50px;
        border-radius: 50%;
        font-size: 20px;
        color: #fff;
        cursor: pointer;
        background: linear-gradient(-135deg, #0a0a2a, #364059);

        transition: all 0.3s ease-in-out;
    }

    &__overlay {
        position: fixed;
        top: 0;
        left: 0;
        height: 100%;
        width: 100%;
        background: linear-gradient(-135deg, #0a0a2a, #364059);
        clip-path: circle(25px at calc(100% - 45px) 45px);
        transition: all 0.3s ease-in-out;

        &__links {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            list-style: none;
            text-align: center;

            li {
                margin: 15px 0;

                a {
                    text-decoration: none;
                    font-size: 30px;
                    font-weight: 500;
                    padding: 5px 30px;
                    color: #fff;
                    position: relative;
                    line-height: 50px;
                    transition: all 0.3s ease;

                    &:after {
                        position: absolute;
                        content: "";
                        background: #4158d0;
                        width: 100%;
                        height: 50px;
                        left: 0;
                        border-radius: 50px;
                        transform: scaleY(0);
                        z-index: -1;
                        transition: transform 0.3s ease;
                    }

                    &:hover {
                        color: #fff;
                    }

                    &:hover::after {
                        transform: scaleY(1);
                    }

                }

                &:nth-child(2) {

                    color: #fff;
                    background: #4158d0;
                    border-radius: 50px;
                }
            }

        }
    }

}
</style>
  