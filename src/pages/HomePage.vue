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
                title: false,
                description: false,
                eleganceAndDesign: false,
                wishText: false,
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
                        } else if (entry.target === this.$refs.roomsTitle) {
                            this.observerView.title = true; 
                        } else if (entry.target === this.$refs.roomsDescription) {
                            this.observerView.description = true;
                        } else if (entry.target === this.$refs.eleganceAndDesign) {
                            this.observerView.eleganceAndDesign = true;
                        } else if (entry.target === this.$refs.wishText) {
                            this.observerView.wishText = true;
                        }
                    }
                });
            }, options);

            // Associa l'osservatore agli elementi
            if (this.$refs.leftRoomImg) observer.observe(this.$refs.leftRoomImg);
            if (this.$refs.rightRoomImg) observer.observe(this.$refs.rightRoomImg);
            if (this.$refs.roomsTitle) observer.observe(this.$refs.roomsTitle);
            if (this.$refs.roomsDescription) observer.observe(this.$refs.roomsDescription);
            if (this.$refs.eleganceAndDesign) observer.observe(this.$refs.eleganceAndDesign);
            if (this.$refs.wishText) observer.observe(this.$refs.wishText);
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
    <header class="header">
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
        <section class="rooms">
            <div class="row justify-content-between align-items-center">
                <!-- Immagine sinistra -->
                <div 
                    class="col-12 col-md-6 room-img-container" 
                    
                >
                    <img 
                        src="https://acapulcohotel.it/wp-content/uploads/2024/02/sezione-camere_grande-1.jpg" 
                        alt="Suite" 
                        class="suite-img w-100" 
                        :class="{ 'animate-left': observerView.left }"
                        ref="leftRoomImg">
                    <h1 
                        class="hurricane text-darkBeige text-end my-2 eleganceAndDesign"
                        :class="{ 'animate-eleganceAndDesign': observerView.eleganceAndDesign }"
                        ref="eleganceAndDesign">
                            Eleganza e design
                    </h1>
                </div>
                <!-- Immagine destra -->
                <div 
                    class="col-12 col-md-6 room-img-container" 
                    
                    
                >
                    <img 
                        src="https://acapulcohotel.it/wp-content/uploads/2024/02/sezione-camere_piccola.jpg" 
                        alt="room-img" 
                        class="room-img w-50"
                        :class="{ 'animate-right': observerView.right }"
                        ref="rightRoomImg">
                    <p 
                        class="room-description my-3 w-50 mx-auto text-start urbanist"
                        :class="{ 'animate-description': observerView.description }"
                        ref="roomsDescription">
                            Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit
                        <button class="filled-button my-5">
                            <a 
                                href="https://acapulcohotel.it/camere-e-suite" class="text-decoration-none fs-3">
                                TUTTE LE CAMERE
                            </a>
                        </button>
                    </p>
                </div>
                <h1 
                    class="urbanist text-veryDarkBeige rooms-title"
                    :class="{ 'animate-title': observerView.title }"
                    ref="roomsTitle">CAMERE E SUITE</h1>
            </div>
        </section>
        <section class="holidays">
            <div class="row">
                <div class="col-12 col-lg-2">
                    <img src="https://acapulcohotel.it/wp-content/uploads/2024/07/banner-immagine1-1.jpg" alt="Holidays">
                </div>
                <div class="col-12 col-lg-5 holidays-info-container">
                    <h1 class="text-darkBeige urbanist holidays-title w-75 mx-auto text-start">
                        LOREM IPSUM DOLOR SIT AMET
                    </h1>
                    <p class="urbanist w-75 mx-auto text-start fs-5 py-4 fw-light holidays-text">
                        Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat.
                    </p>
                    <div class="buttons w-75 mx-auto">
                        <div class="row justify-content-center">
                            <button class="filled-button col-5 me-5">
                                <a 
                                    href="https://acapulcohotel.it/camere-e-suite" class="text-decoration-none fs-5">
                                    ASSICURA LA CAPARRA
                                </a>
                            </button>
                            <button class="filled-button col-5 darkBeigeButton">
                                <a 
                                    href="https://acapulcohotel.it/camere-e-suite" class="text-decoration-none fs-5">
                                    ASSICURA LA VACANZA
                                </a>
                            </button>
                        </div>
                    </div>
                    <img src="https://acapulcohotel.it/wp-content/uploads/2024/07/banner-immagine2-1.jpg" alt="Wine" class="holidays-wine">
                </div>
                <div class="col-12 col-lg-5">
                    <img src="https://acapulcohotel.it/wp-content/uploads/2024/07/banner-immagine3-1.jpg" alt="Window">
                </div>
            </div>
        </section>
        <section class="light-wish d-flex justify-content-center align-items-center">
            <div class="row justify-content-center align-items-center w-100">
                    <h1 
                        class="col-12 urbanist text-darkBeige h-100 w-100"
                        :class="{ 'animate-text': observerView.wishText }"
                        ref="wishText">
                        LOREM IPSUM DOLOR SIT AMET, NIBH CONSECTETUER
                    </h1>
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
        padding: 100px 0;
        overflow-x: hidden;

        .rooms-title {
            font-size: 225px;
            font-weight: 300;
            opacity: 0;
            position: absolute;
            top: 5%;
            transform: translateY(200%);
            transition: all 1s ease-in-out;
            
            &.animate-title {
                opacity: .5;
                transform: translateY(0);
            }
        }

        .room-img-container {

            .suite-img {
                transform: translateX(-25%);
                transition: all 1.5s;
                opacity: .5;

                &.animate-left {
                    transform: translateX(0);
                    opacity: 1;
                }
            }

            .room-img {
                transform: translateX(100%);
                transition: all 1.5s;
                opacity: .5;

                &.animate-right {
                    transform: translateX(0);
                    opacity: 1;
                }
            }

            &:nth-child(2) {
                margin-top: 15%;
            }

            .eleganceAndDesign {
                transition: all 2s;
                transform: translateX(-30%);

                &.animate-eleganceAndDesign {
                    transform: translateX(0);
                }
            }


            
        }

        .room-description {
            font-size: 20px;
            font-weight: 300;
            letter-spacing: .5px;
            opacity: .9;
            padding: 40px 0;
            line-height: 32px;
            transition: all 2s;
            transform: translateY(40%);

            &.animate-description {
                transform: translateY(0);
            }
        }
    }

    .holidays {
        background: $beige2;
        padding: 100px 0;

        .holidays-info-container {

            position: relative;

            .holidays-title {
                font-size: 64px;
                font-weight: 300;
            }
    
            .holidays-text {
                letter-spacing: .5px;
            }
    
            .buttons {
                
                .darkBeigeButton {
                    background-color: white;
                    border-color: $darkBeige;
    
                    &::before {
                        background-color: $darkBeige;
                    }
    
                    &:hover {
                        * {
                            color: $darkBeige;
                        }
                    }
                   
                }
            }
    
            .holidays-wine {
                position: absolute;
                bottom: -270px;
                left: 100px;
                max-height: 800px;
            }
        }


    }

    .light-wish {
        min-height: 100vh;
        background-color: white;
        

        h1 {
            font-size: 175px;
            font-weight: 300;
            display: block;
            margin: 300px 0;
            opacity: .5;
            transition: opacity 1s ease-in-out;

            &.animate-text {
                opacity: 1;
            }
        }
    }
}
</style>
