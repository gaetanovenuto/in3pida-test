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
        <h1 class="words-about-us text-center d-flex justify-content-evenly align-items-center py-5">
            DICONO DI NOI <i class="fa-solid fa-diamond fs-4"></i> DICONO DI NOI
        </h1>
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
}
</style>
