<script>
export default {
    data() {
            return { 
            
            }
        }
}
</script>

<template>
    <section class="holidays">
        <div class="row w-100">
            <div class="col-12 col-xxl-2">
                <img src="https://acapulcohotel.it/wp-content/uploads/2024/07/banner-immagine1-1.jpg" alt="Holidays" class="holiday-img img-fluid">
            </div>
            <div class="col-12 col-xxl-5 holidays-info-container">
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
            <div class="col-12 col-xxl-4">
                <img src="https://acapulcohotel.it/wp-content/uploads/2024/07/banner-immagine3-1.jpg" alt="Window" class="window-image">
            </div>
        </div>
    </section>
</template>

<style lang="scss" scoped>
@import "../../../assets/scss/partials/variables";
@import "../../../assets/scss/main.scss";

.holidays {
    background: $beige2;
    padding: 100px 0;

    .holiday-img {
        max-width: 100vw;
    }

    .holidays-info-container {
        position: relative;

        @media screen and (max-width: 1400px) {
            padding: 30px 0;
        }

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

            @media (max-width: 1400px) {
                display: none;
            }
        }

    }

    .window-image {
        max-width: 100vw;
        object-fit: cover;
        margin: 0;

    }

    @media screen and (max-width: 1400px) {
        padding-bottom: 0;
        margin-bottom: 0;
    }
}
</style>