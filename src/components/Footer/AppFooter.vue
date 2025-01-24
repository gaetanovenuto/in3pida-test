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
        <div class="row">
            <h1 class="words-about-us col-12 text-center d-flex justify-content-evenly align-items-center pt-5 pb-1">
                DICONO DI NOI <i class="fa-solid fa-diamond fs-4 d-md-inline-block"></i><span class="d-md-inline-block">DICONO DI NOI</span>
            </h1>
            <div class="carousel-container d-flex align-items-center mb-4">
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
    </div>
    <div class="info bg-beige text-darkBeige">
        <div class="row g-0 w-100">
            <div class="col-12 col-md-3 video-container">
                <video src="https://acapulcohotel.it/wp-content/uploads/2024/03/video-piscina-foote-hotel-acapulco.mp4" autoplay muted loop playsinline preload="auto" class="w-100"></video>
            </div>
            <div class="col-12 col-md-9 info-container text-darkBeige">
                <div class="row">
                    <img src="https://acapulcohotel.it/wp-content/uploads/2024/01/logo-oro-1.svg" alt="Hotel Acapulco Cattolica" class="logo-footer">
                </div>
                <hr class="line-beige footer-line">
                <div class="row urbanist">
                    <div class="col-12 col-lg-4">
                        <h4>
                            DOVE TROVARCI
                        </h4>
                        <p>Via del Turismo 1</p>
                        <p>47841 Cattolica (RN)</p>
                    </div>
                    <div class="col-12 col-lg-4">
                        <h4>
                            CONTATTI
                        </h4>
                        <p>Tel. 0541.958060 -  Cell. 3756841613</p>
                        <p>Email. info@acapulcohotel.it</p>
                    </div>
                    <div class="col-12 col-lg-4">
                        <h4>
                            DATI SOCIETARI
                        </h4>
                        <p>P.Iva 03140750401</p>
                        <a class="text-decoration-none text-darkBeige" href="https://acapulcohotel.it/privacy-policy/">Privacy</a> - <a class="text-decoration-none text-darkBeige" href="https://acapulcohotel.it/cookie-policy/">Cookie policy</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
@import "../../assets/scss/partials/variables";
@import "../../assets/scss/main.scss";

.reviews {
    max-width: 100vw;
    overflow: hidden;

    .words-about-us {
        font-size: 6vw;
        font-weight: 300;
        overflow: hidden;
        max-width: 100vw;

        @media screen and (max-width: 768px) {
            font-size: 10vw;
        }

        i, .d-md-inline-block {
            display: none;
        }
    
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

.info {
    max-height: 100%;
    width: 100%;

    .video-container {

        @media screen and (max-width: 768px) {
            margin: 0 auto;
            padding: 0;
        }
        
        video {
            object-fit: cover;
        }
    }


    .info-container {
        background-image: url('/public/img/Acapulco/footer-background.jpg');
        padding: 115px;

        .logo-footer {
            width: 300px;
            
            @media screen and (max-width: 992px) {
                width: 200px;
            }
            
        }

        .footer-line {
            height: 2px;
            opacity: .7;
            margin: 80px 0;
        }

        h4 {
            font-weight: 300;
            font-size: 32px;
        }

        p, a {
            font-size: 18px;
            
        }
        
    }
}
</style>
