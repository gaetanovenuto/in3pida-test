<script>
export default {
    data() {
        return {
            activeSlide: 0,
            observer: null,
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
            ],
            observerView: {
                left: false,
                right: false,
            }
        };
    },
    mounted() {
        // Configura gli osservatori per la sezione rooms e il carosello
        this.setupIntersectionObserver();
        this.setupObserverForRooms();
    },
    beforeUnmount() {
        // Disconnetti l'osservatore quando il componente viene smontato
        if (this.observer) {
            this.observer.disconnect();
        }
    },
    methods: {
        /**
         * Configura un unico IntersectionObserver per animare le immagini della sezione rooms.
         */
        setupObserverForRooms() {
            const options = {
                root: null,
                rootMargin: '0px',
                threshold: 0.1
            };

            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        if (entry.target === this.$refs.leftRoomImg) {
                            this.observerView.left = true;
                        } else if (entry.target === this.$refs.rightRoomImg) {
                            this.observerView.right = true;
                        }
                    }
                });
            }, options);

            // Associa l'osservatore agli elementi
            if (this.$refs.leftRoomImg) observer.observe(this.$refs.leftRoomImg);
            if (this.$refs.rightRoomImg) observer.observe(this.$refs.rightRoomImg);
        },

        /**
         * Configura l'IntersectionObserver per il carosello.
         */
        setupIntersectionObserver() {
            const options = {
                root: null,
                rootMargin: '0px',
                threshold: 0.5
            };

            this.observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const slideIndex = Array.from(this.$refs.slides).findIndex(
                            slide => slide === entry.target
                        );
                        this.activeSlide = slideIndex;
                    }
                });
            }, options);

            this.$nextTick(() => {
                if (this.$refs.slides) {
                    this.$refs.slides.forEach(slide => {
                        this.observer.observe(slide);
                    });
                }
            });
        },

        /**
         * Effettua uno scroll fluido verso una specifica slide del carosello.
         */
        scrollToSlide(index) {
            this.$refs.slides[index].scrollIntoView({
                behavior: 'smooth',
                block: 'center'
            });
        }
    }
};
</script>

<template>
    <header class="header col-12">
        <video class="header-video" src="../../public/img/Acapulco/video-piscina-hotel-acapulco-home.mp4" autoplay muted loop playsinline preload="auto">
        </video>
        <a class="header-logo" href="/">
            <img src="https://acapulcohotel.it/wp-content/uploads/2024/01/logo-bianco.svg" alt="Acapulco Hotel">
        </a>
    </header>
    <main>
        <article class="about-article bg-beige">
            <section class="container">
                <div class="row">
                    <div class="col-12 text-center">
                        <h1 class="about-title hurricane text-darkBeige">
                            Lorem ipsum dolor aliquam
                        </h1>
                        <img src="https://acapulcohotel.it/wp-content/uploads/2024/01/immagine-in-evidenza.jpg" alt="About-image" width="680" height="470">
                        <p class="about-text urbanist text-darkBeige">
                            LOREM IPSUM DOLOR ALIQUAM NONUMMY SIT EIUSMONT AMET NIBH EUISMOD TINCIDUNT UT LAOREET DOLORE MAGNA ALIQUAM ERAT LOREM IPSUM ALIQUA DECIDIT SED EAM CORPORE.
                        </p>
                        <p class="text-center hurricane text-darkBeige about-signature">Marisa, Hotel Acapulco</p>
                    </div>
                </div>
            </section>
        </article>
        <section class="carousel-section">
            <div 
                class="card-wrapper" 
                v-for="(slide, index) in carouselSlides" 
                :key="index"
                :class="{ 'blurred': index < activeSlide }"
            >
                <div class="card">
                    <div class="row align-items-center justify-content-center">
                        <div class="col-md-6 position-relative w-100">
                            <img :src="slide.image" :alt="slide.title" class="card-image">
                        </div>
                        <div class="col-md-6 position-absolute">
                            <h2 class="card-title urbanist text-white">{{ slide.title }}</h2>
                            <button class="empty-button bg-none">
                                <a :href="slide.href" class="text-decoration-none">SCOPRI DI PIÙ</a>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>
        <section class="available-offers bg-white m-0 d-flex flex-column justify-content-start align-items-start">
            <div class="container text-darkBeige text-start urbanist p-0">
                <h1 class="offer-title m-0 p-0">
                    LOREM IPSUM OFFERTA 1
                </h1>
                <p class="offer-description m-0 p-0">
                    Valida dal xx.xx.xxxx al xx.xx.xxxx | a partire da xx euro a persona
                </p>
                <hr class="line-beige">
                <h1 class="offer-title m-0 p-0">
                    LOREM IPSUM OFFERTA 2
                </h1>
                <p class="offer-description m-0 p-0">
                    Valida dal xx.xx.xxxx al xx.xx.xxxx | a partire da xx euro a persona
                </p>
                <hr class="line-beige">
                <h1 class="offer-title m-0 p-0">
                    LOREM IPSUM OFFERTA 3
                </h1>
                <p class="offer-description m-0 p-0">
                    Valida dal xx.xx.xxxx al xx.xx.xxxx | a partire da xx euro a persona
                </p>
                <hr class="line-beige">
                <button class="filled-button my-5">
                    <a href="https://acapulcohotel.it/offerte/" class="text-decoration-none">TUTTE LE OFFERTE

                    </a>
                </button>
            </div>
        </section>
        <section class="rooms py-5">
            <div class="row justify-content-between align-items-center">
                <!-- Immagine sinistra -->
                <div 
                    class="col-12 col-md-6 room-img-container" 
                    :class="{ 'animate-left': observerView.left }"
                    ref="leftRoomImg"
                >
                    <img src="https://acapulcohotel.it/wp-content/uploads/2024/02/sezione-camere_grande-1.jpg" alt="Suite" class="suite-img w-100">
                    <h1 class="hurricane text-darkBeige text-end my-2">
                        Eleganza e design
                    </h1>
                </div>
                <!-- Immagine destra -->
                <div 
                    class="col-12 col-md-6 room-img-container" 
                    :class="{ 'animate-right': observerView.right }"
                    ref="rightRoomImg"
                >
                    <img src="https://acapulcohotel.it/wp-content/uploads/2024/02/sezione-camere_piccola.jpg" alt="room-img" class="room-img w-50">
                    <p class="room-description my-3 w-50 mx-auto text-start urbanist">
                        Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit
                        <button class="filled-button my-5">
                            <a href="https://acapulcohotel.it/camere-e-suite" class="text-decoration-none fs-3">
                                TUTTE LE CAMERE
                            </a>
                        </button>
                    </p>
                </div>
                <h1 class="urbanist text-veryDarkBeige rooms-title">CAMERE E SUITE</h1>
            </div>
        </section>
    </main>
</template>

<style lang="scss" scoped>
@import "../assets/scss/partials/variables.scss";
@import "../assets/scss/main.scss";

.header {
    position: fixed;
    top: 0;
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1;

    .header-video {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
    }

    .header-logo {
        width: 400px;
        z-index: 1;
    }
}

main {
    position: relative;
    z-index: 2;
    margin-top: 100vh;

    .about-article {

        .container {
    
            .row {
            
                .about-title {
                    font-size: 70px;
                    padding: 40px 0 20px 0;
                }
                
                .about-text {
                    width: 100%;
                    margin: 0 auto;
                    padding: 30px 10px;
                    font-size: 26px;
                    letter-spacing: .8px;
                    font-weight: 300;
                }

                .about-signature {
                    font-size: 32px;
                    letter-spacing: .8px;
                }
            }
        }
    }
    
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
                font-size: 64px;
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

    .available-offers {
        
        .container {
            max-width: 90vw !important;

            .offer-title {
                font-size: 64px;
                font-weight: 300;
                transition: all 0.3s ease;

                &:hover {
                    font-weight: 700;
                    cursor: pointer;
                    transition: font-weight 0.3s ease;
                }
            }

            .offer-description {
                font-size: 18px;
                font-weight: 300;
            }

        }
    }

    .rooms {
        background-color: white;
        position: relative;

        .rooms-title {
            font-size: 14rem;
            font-weight: 300;
            opacity: .5;
            position: absolute;
            top: 3%;
            left: 50%;
            transform: translateX(-50%);
        }

        .room-img-container {
            opacity: 0;
            transform: translateX(100px);
            transition: all 1s ease-out;

            &:nth-child(2) {
                margin-top: 15%;
            }

            &.animate-left {
                opacity: 1;
                transform: translateX(-50px);
            }

            &.animate-right {
                opacity: 1;
                transform: translateX(50px);
            }
        }

        .room-description {
            font-size: 20px;
            font-weight: 300;
            letter-spacing: .5px;
            opacity: .9;
            padding: 40px 0;
            line-height: 32px;
        }
    }

}
</style>
