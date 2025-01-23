<script>
export default {
    data() {
            return { 
                activeSlide: 0,
                carouselSlides: [
                {
                    image: 'https://acapulcohotel.it/wp-content/uploads/2024/03/piscina-acapulco-buon-motivo.jpg',
                    title: 'PISCINA E BENESSERE',
                    href: 'https://acapulcohotel.it/piscina/',
                },
                {
                    image: 'https://acapulcohotel.it/wp-content/uploads/2024/03/buon-motivo-vacanze-in-famiglia.jpg',
                    title: 'VACANZE IN FAMIGLIA',
                    href: 'https://acapulcohotel.it/vacanze-in-famiglia/',
                },
                {
                    image: 'https://acapulcohotel.it/wp-content/uploads/2024/02/buon-motivo01.jpg',
                    title: 'ECCELLENZE NEL PIATTO',
                    href: 'https://acapulcohotel.it/ristorante/',
                }
                ]
            }
        },
    mounted() {
        this.setupIntersectionObserver();
    },
    methods: {
        setupIntersectionObserver() {
            const options = {
                root: null,
                rootMargin: '0px',
                treshold: 0.5
            }

            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const slideIndex = Array.from(this.$refs.slides).findIndex(slide => slide === entry.target)
                        this.activeSlide = slideIndex
                    }
                })
            }, options)

            this.$nextTick(() => {
                if (this.$refs.slides) {
                    this.$refs.slides.forEach(slide => {
                        observer.observe(slide)
                    })
                }
            })
        }
    }
}
</script>

<template>
    <section class="carousel-section">
        <div
            v-for="(slide, index) in carouselSlides"
            :key="index"
            class="card-wrapper"
            :class="{ 'blurred': index < activeSlide }"
        >
            <div class="card">
                <div class="row align-items-center justify-content-center">
                    <div class="col-md-6 position-relative w-100">
                        <img 
                            :src="slide.image" 
                            :alt="slide.title"
                            class="card-image"
                        >
                    </div>
                    <div class="col-md-6 position-absolute text-center">
                        <h2 class="card-title urbanist text-white">{{ slide.title }}</h2>
                        <button class="empty-button bg-none fs-4">
                            <a :href="slide.href" class="text-decoration-none">SCOPRI DI PIÙ</a>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<style lang="scss" scoped>
@import "../../../assets/scss/partials/variables";
@import "../../../assets/scss/main.scss";

.carousel-section {
        position: relative;
        background-color: white;
        padding: 75px 0;
        
        
        .card-wrapper {
            height: 100vh;
            position: sticky;
            top: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            
        }
        
        .card {
            background: white;
            width: 90vw;
            margin: 0 auto;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            
            &-image {
                width: 100%;
                height: auto;
                object-fit: cover;
                
            }
            
            &-title {
                font-size: 78px;
                margin-bottom: 1.5rem;
                color: white;
                font-weight: 300;
                
            }
            
        }
        
        @for $i from 1 through 10 {
            .card-wrapper:nth-child(#{$i}) {
                z-index: #{$i};
                
            }
        }
        
    }
</style>