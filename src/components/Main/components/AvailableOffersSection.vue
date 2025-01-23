<script>
export default {
    data() {
            return { 
            
            }
        }
}
</script>

<template>
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
</template>

<style lang="scss" scoped>
@import "../../../assets/scss/partials/variables";
@import "../../../assets/scss/main.scss";

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
</style>