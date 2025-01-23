<script>
export default {
    data() {
        return { 
            loremPhrases: [
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit",
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua",
                "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris",
                "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum",
                "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui"
            ],
        }
    },
    methods: {
    }
}
</script>

<template>
    <div class="reviews bg-darkBeige text-white">
        <h1 class="words-about-us text-center d-flex justify-content-evenly align-items-center pt-5 pb-1">
            DICONO DI NOI <i class="fa-solid fa-diamond fs-4"></i> DICONO DI NOI
        </h1>
        <div class="carousel-container d-flex align-items-center">
            <div class="carousel-slide d-flex align-items-center">
                <div v-for="(phrase, index) in loremPhrases" :key="index" class="text-white w-100 d-flex align-items-center mt-2">
                    {{ phrase }} <i class="fa-solid fa-diamond diamond-icon mx-2"></i>
                </div>
            </div>
            <div class="carousel-slide d-flex align-items-center">
                <div v-for="(phrase, index) in loremPhrases" :key="index" class="text-white w-100 d-flex align-items-center mt-2">
                    {{ phrase }} <i class="fa-solid fa-diamond diamond-icon mx-2"></i>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
@import "../../assets/scss/partials/variables";
@import "../../assets/scss/main.scss";

.reviews {
    .words-about-us {
        font-size: 115px;
        font-weight: 300;
    }

    .carousel-container {
        overflow: hidden;
        white-space: nowrap;

        .carousel-slide {
            display: inline-block;
            animation: 15s slide infinite linear;

            .diamond-icon {
                font-size: 8px;
            }
        }
    }

    @keyframes slide {
        from {
            transform: translateX(0);
        }
        to {
            transform: translateX(-100%);
        }
    }

}
</style>
