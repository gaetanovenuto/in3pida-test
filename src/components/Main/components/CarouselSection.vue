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
                threshold: [0, 0.25, 0.5, 0.75, 1]
            };

            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const slideIndex = Array.from(this.$refs.slides).findIndex(slide => slide === entry.target)
                        
                        // Calcola la progressione del blur e della scala basata sul threshold
                        const blurProgress = entry.intersectionRatio;
                        const opacityFactor = Math.max(0, 1 - blurProgress * 1.5);
                        const scaleFactor = Math.max(0.9, 1 - blurProgress * 0.2);
                        const isHidden = blurProgress < 0.05;
                        
                        entry.target.classList.toggle('hidden', isHidden);
                        entry.target.style.setProperty('--opacity-progress', opacityFactor);
                        entry.target.style.setProperty('--scale-progress', scaleFactor);
                        
                        if (slideIndex !== this.activeSlide) {
                            this.activeSlide = slideIndex
                        }
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
            ref="slides"
            class="card-wrapper"
            :class="{ 
                'blurring': index < activeSlide,
                'disappeared': index < activeSlide 
            }"
        >
            <div class="card w-100 h-100">
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
        height: 100%;
        position: sticky;
        top: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        transition: all 3s ease;

        &.blurring {
            opacity: calc(var(--opacity-progress, 1));
            transform: scale(calc(var(--scale-progress, 1)));
            transition: all 3s ease;
        }

        &.disappeared {
            visibility: hidden;
            opacity: 0;
            transition: all 3s ease;
        }

        &.hidden {
            opacity: 0;
            visibility: hidden;
        }
    }
        
    .card {
        background: white;
        width: 90vw;
        margin: 0 20px;
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
    
    @media (max-width: 992px) {
        .card {
            width: 100%;
            margin: 5px 15px;
        }

        .carousel-section {
            padding: 50px 0;
        }
        
        .card-title {
            font-size: 48px;
        }
    }
}
</style>