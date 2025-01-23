<script>
export default {
    data() {
        return {
            observerView: {
                left: false,
                right: false,
                title: false,
                description: false,
                eleganceAndDesign: false
            }
        }
    },
    mounted() {
        this.setupObserverForRooms()
    },
    methods: {
        setupObserverForRooms() {
            const options = {
                root: null,
                rootMargin: '0px',
                threshold: 0.1
            }

            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        if (entry.target === this.$refs.leftRoomImg) {
                            this.observerView.left = true
                        } else if (entry.target === this.$refs.rightRoomImg) {
                            this.observerView.right = true
                        } else if (entry.target === this.$refs.roomsTitle) {
                            this.observerView.title = true
                        } else if (entry.target === this.$refs.roomsDescription) {
                            this.observerView.description = true
                        } else if (entry.target === this.$refs.eleganceAndDesign) {
                            this.observerView.eleganceAndDesign = true
                        }
                    }
                })
            }, options)

            const elementsToObserve = [
                this.$refs.leftRoomImg,
                this.$refs.rightRoomImg,
                this.$refs.roomsTitle,
                this.$refs.roomsDescription,
                this.$refs.eleganceAndDesign
            ]

            elementsToObserve.forEach(el => {
                if (el) observer.observe(el)
            })
        }
    }
}
</script>

<template>
    <section class="rooms">
            <div class="row justify-content-between align-items-center w-100">
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
                    class="urbanist text-veryDarkBeige rooms-title text-center"
                    :class="{ 'animate-title': observerView.title }"
                    ref="roomsTitle">CAMERE E SUITE</h1>
            </div>
        </section>
</template>

<style lang="scss" scoped>
@import "../../../assets/scss/partials/variables";
@import "../../../assets/scss/main.scss";

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
                transform: translateX(50%);
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

</style>