<script>
export default {
  data() {
    return {
    };
  },
};
</script>


<template>
    <header class="header w-100 d-flex justify-content-center align-items-center">
        <video 
            class="header-video w-100 h-100 img-fluid" 
            src="/img/Acapulco/video-piscina-hotel-acapulco-home.mp4" 
            autoplay 
            muted 
            loop 
            playsinline 
            preload="auto"
        >
        </video>
        <a class="header-logo" href="/">
            <img 
                src="https://acapulcohotel.it/wp-content/uploads/2024/01/logo-bianco.svg" 
                alt="Acapulco Hotel"
            >
        </a>
    </header>
</template>


<style lang="scss" scoped>

.header {
    position: fixed;
    height: 100vh;
    max-width: 100vw;
    top: 0;
    z-index: -1;

    .header-video {
        position: absolute;
        top: 0;
        left: 0;
        object-fit: cover;
        max-width: 100vw;
        max-height: 100vh;
    }

    .header-logo {
        width: 30vw;
        max-width: 500px;
        z-index: 0;
    }
}

</style>
