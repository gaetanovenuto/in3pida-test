<script>
export default {
    data() {
        return {
            scrollHeight: 0,
            isOffCanvasOpen: false,
            activeLink: null,
            offCanvasLinks: [
                {
                    title: 'Camere e suite',
                    imgLink: 'https://acapulcohotel.it/wp-content/uploads/2024/02/menu-camere.jpg'
                },
                {
                    title: 'Hotel',
                    imgLink: 'https://acapulcohotel.it/wp-content/uploads/2024/03/icona-menu-hotel-acapulco-cattolica.jpg',
                    subLinks: ['Cucina', 'Piscina', 'Family']
                },
                {
                    title: 'Servizi',
                    imgLink: 'https://acapulcohotel.it/wp-content/uploads/2024/03/aperitivo-piscina-icona-menu-hotel-acapulco-cattolica.jpg'
                },
                {
                    title: 'Offerte',
                    imgLink: 'https://acapulcohotel.it/wp-content/uploads/2024/03/icona-menu-offerte-hotel-acapulco-cattolica.jpg'
                },
                {
                    title: 'Cattolica',
                    imgLink: 'https://acapulcohotel.it/wp-content/uploads/2024/02/menu-dove.jpg'
                },
            ],
        }
    },
    methods: {
        handleScroll() {
            const scrollTop = window.scrollY;
            const documentHeight = Math.max(
                document.body.scrollHeight,
                document.documentElement.scrollHeight
            ) - window.innerHeight;
            const scrollPercentage = Math.min((scrollTop / documentHeight) * 100, 100);
            this.scrollHeight = scrollPercentage;
        },
        toggleOffCanvas() {
            this.isOffCanvasOpen = !this.isOffCanvasOpen;

            if (this.isOffCanvasOpen) {
                this.activeLink = this.offCanvasLinks[0];
            } else {
                this.activeLink = this.offCanvasLinks[i];
            }
        },
        setActiveLink(link) {
            if (link) {

                this.activeLink = link;
            }
        }
    },
    mounted() {
        window.addEventListener("scroll", this.handleScroll);
    },
    beforeUnmount() {
        window.removeEventListener("scroll", this.handleScroll);
    }
}
</script>

<template>
    <Aside class="sidebar">
        <div class="row flex-column align-items-center h-100">
            <div class="col-1 my-2 d-flex justify-content-center align-items-center">
                <button 
                    class="menu-toggle-btn"
                    @click="toggleOffCanvas"
                >
                    <i class="fa-solid fa-bars"></i>
                </button>
            </div>
            <div class="col-5 bar-container my-2 d-flex justify-content-center align-items-center">
                <div class="progress-bar">
                    <div
                        class="progress-fill"
                        :style="{ height: scrollHeight + '%' }"
                    ></div>
                </div>
            </div>
        </div>

        <div 
            class="offcanvas-menu urbanist text-darkBeige" 
            :class="{ 'is-open': isOffCanvasOpen }"
        >
            <div class="row justify-content-between p-3">
                <div class="col-4 m-2 fw-bold languages">
                    <div class="row d-flex align-items-center">
                        <div class="col-auto d-flex justify-content-center align-items-center">
                            IT
                        </div>
                        <div class="col-auto d-flex justify-content-center align-items-center">
                            <i class="fa-solid fa-diamond mx-2"></i>
                        </div>
                        <div class="col-auto d-flex justify-content-center align-items-center">
                            EN
                        </div>
                        <div class="col-auto d-flex justify-content-center align-items-center">
                            <i class="fa-solid fa-diamond mx-2"></i>
                        </div>
                        <div class="col-auto d-flex justify-content-center align-items-center">
                            DE
                        </div>
                    </div>
                </div>
                <div class="col-5 m-2 h-100">
                    <a class="header-logo" href="/">
                        <img 
                            src="https://acapulcohotel.it/wp-content/uploads/2024/01/logo-bianco.svg" 
                            alt="Acapulco Hotel" width="200px"
                        >
                    </a>
                </div>
                <button 
                    class="close-btn col-auto h-100" 
                    @click="toggleOffCanvas"
                >
                    <i class="fa-solid fa-times"></i>
                </button>
            </div>    
            <div class="offcanvas-links row">
            <div class="col-6 link-image-container">
                <div 
                    v-if="activeLink" 
                    class="image-wrapper m-0"
                >
                    <img 
                        :src="activeLink.imgLink" 
                        :alt="activeLink.title"
                        class="link-hover-image"
                    />
                </div>
            </div>
            <div class="col-6 pt-4 px-5">
                <div 
                    v-for="(link, index) in offCanvasLinks" 
                    :key="index" 
                    class="offcanvas-link-item"
                    @mouseenter="setActiveLink(link)"
                    @mouseleave="setActiveLink(null)"
                >
                    <a href="#" class="link-title">
                        {{ link.title }}
                    </a>
                    
                    <div 
                        v-if="link.subLinks" 
                        class="sub-links"
                    >
                        <a 
                            v-for="(subLink, subIndex) in link.subLinks" 
                            :key="subIndex" 
                            href="#"
                            class="sub-link"
                        >
                            {{ subLink }}
                        </a>
                    </div>
                </div>
            </div>
        </div>
        </div>
    </Aside>
</template>

<style lang="scss" scoped>
@import "../../assets/scss/partials/variables";
@import "../../assets/scss/main.scss";

aside {
    position: fixed;
    top: 0;
    right: 0;
    z-index: 999;
    background-color: transparent;
    width: 100px;
    height: 100vh;

    .menu-toggle-btn {
        background: none;
        border: none;
        cursor: pointer;
        transition: transform 0.3s ease;

        &:hover {
            transform: scale(1.1);
        }

        .fa-bars {
            font-size: 48px;
            color: $darkBeige;
            font-weight: 600;
        }
    }

    .bar-container {
        min-height: 400px !important;
    }

    .progress-bar {
        position: relative;
        width: 5px;
        background-color: rgb(226, 226, 226);
        border-radius: 10px;
        height: 100%;
    }

    .progress-fill {
        position: absolute;
        top: 0;
        width: 100%;
        background: $darkBeige;
        transition: height 0.1s ease-out;
    }

    .offcanvas-menu {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba($beige, 1);
        transform: translateX(-100%);
        transition: transform 0.4s ease;
        

        &.is-open {
            transform: translateX(0);
        }

        .row {
            max-height: 200px;
        }

        .close-btn {
            background: none;
            border: none;
            cursor: pointer;

            .fa-times {
                font-size: 36px;
                color: white;
            }
        }

        .languages {
            font-size: 18px;

            * {
                margin: 0;
                padding: 2px;
            }

            .fa-diamond {
                font-size: 10px;
            }
        }

        .offcanvas-links {
            position: relative;

            .offcanvas-link-item {
                margin-bottom: 20px;
                position: relative;

                .link-title {
                    font-size: 24px;
                    color: #8b7e6c;
                    text-decoration: none;
                    transition: color 0.3s ease;

                    &:hover {
                        color: darken(#8b7e6c, 15%);
                    }
                }

                .sub-links {
                    margin-top: 10px;
                    display: flex;
                    flex-direction: column;

                    .sub-link {
                        color: #333;
                        text-decoration: none;
                        margin-left: 15px;
                        transition: color 0.3s ease;

                        &:hover {
                            color: #8b7e6c;
                        }
                    }
                }
            }

            .link-image-container {

                position: relative;

                @media (max-width: 1024px) {
                    display: none;
                }

                .image-wrapper {
                    position: relative;
                    width: 100%;
                    height: 500px; // Altezza specifica come nel sito originale
                    overflow: hidden;
                    margin: 0;
                    padding: 0;
                }

                .link-hover-image {
                    width: 100%;
                    height: 100%;
                    object-fit: contain;
                    opacity: 1;
                    transform: scale(1);
                }

                .image-wrapper:hover .link-hover-image {
                    opacity: 1;
                    transform: scale(1);
                }

                .offcanvas-link-item {
                    .sub-links {
                        display: none; // Nascondi sub-link di default
                    }

                    &:hover .sub-links {
                        display: flex; // Mostra sub-link solo al passaggio del mouse
                    }

                    .link-title {
                        font-size: 72px; // Dimensione link più grande
                        font-weight: 600;
                    }

                    .sub-links {
                        margin-top: 20px;

                        .sub-link {
                            font-size: 24px;
                            margin-left: 30px;
                        }
                    }
                }

                img {
                    object-fit: cover;
                }
            }
        }

        .fade-enter-active, .fade-leave-active {
            transition: opacity 0.3s;
        }
        .fade-enter, .fade-leave-to {
            opacity: 0;
        }
    }
}
</style>