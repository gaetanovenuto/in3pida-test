<script>
export default {
    data() {
            return { 
                observerView: {
                    wishText: false
                }
            }
        },
    mounted() {
        this.setupObserverForWishText()
    },
    methods: {
        setupObserverForWishText() {
            const options = {
                root: null,
                rootMargin: '0px',
                threshold: 0.1
            }

            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting && entry.target === this.$refs.wishText) {
                        this.observerView.wishText = true
                    }
                })
            }, options)

            if (this.$refs.wishText) {
                observer.observe(this.$refs.wishText)
            }
        }
    }
}
</script>

<template>
    <section class="light-wish d-flex justify-content-center align-items-center">
        <div class="row justify-content-center align-items-center w-100">
            <h1 
                class="col-12 urbanist text-darkBeige h-100 w-100 text-center"
                :class="{ 'animate-text': observerView.wishText }"
                ref="wishText">
                LOREM IPSUM DOLOR SIT AMET, NIBH CONSECTETUER
            </h1>
        </div>
    </section>
</template>

<style lang="scss" scoped>
@import "../../../assets/scss/partials/variables";
@import "../../../assets/scss/main.scss";

.light-wish {
    min-height: 100vh;
    max-width: 100vw;
    background-color: white;

    .row {
        max-width: 100vw;
        width: 100%;
        margin: 0 auto;
    }

    h1 {
        font-size: 9vw;
        max-width: 100vw;
        font-weight: 300;
        display: block;
        margin: 300px 0;
        opacity: .5;
        transition: opacity 1s ease-in-out;
        width: 75%;

        &.animate-text {
            opacity: 1;
        }
    }
}
</style>