<script>
export default {
    data() {
            return { 
            
            }
        }
}
</script>

<template>
    <article class="about-article bg-beige">
        <section class="container">
            <div class="row">
                <div class="col-12 text-center">
                    <h1 class="about-title hurricane text-darkBeige">
                        Lorem ipsum dolor aliquam
                    </h1>
                    <img 
                        src="https://acapulcohotel.it/wp-content/uploads/2024/01/immagine-in-evidenza.jpg" 
                        alt="about-us-image"
                        width="680"
                        height="470"
                        class="img-fluid"
                        >
                    <p class="about-text urbanist text-darkBeige w-100 m-auto">
                        LOREM IPSUM DOLOR ALIQUAM NONUMMY SIT EIUSMONT AMET NIBH EUISMOD TINCIDUNT UT LAOREET DOLORE MAGNA ALIQUAM ERAT LOREM IPSUM ALIQUA DECIDIT SED EAM CORPORE.
                    </p>
                    <p class="text-center hurricane text-darkBeige about-signature">
                        Marisa, Hotel Acapulco
                    </p>
                </div>
            </div>
        </section>
    </article>
</template>

<style lang="scss" scoped>
@import "../../../assets/scss/partials/variables";
@import "../../../assets/scss/main.scss";

.about-article {

    .container {

        .row {

            .about-title {
                font-size: 70px;
                padding: 40px 0 20px;
            }

            .about-text {
                padding: 30px 10px;
                font-size: 26px;
                font-weight: 300;
            }

            .about-signature {
                font-size: 32px;
            }

            .about-text, .about-signature {
                letter-spacing: .8px;
            }
        }
    }
}
</style>