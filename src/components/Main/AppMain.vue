<script>
import AboutSection from './components/AboutSection.vue';
import CarouselSection from './components/CarouselSection.vue';
import AvailableOffersSection from './components/AvailableOffersSection.vue';
import RoomsSection from './components/RoomsSection.vue';
import HolidaysSection from './components/HolidaysSection.vue';
import WishSection from './components/WishSection.vue';

export default {
    data() {
            return { 
            
            }
        },
    components: {
        AboutSection,
        CarouselSection,
        AvailableOffersSection,
        RoomsSection,
        HolidaysSection,
        WishSection,
    }
}
</script>

<template>
    <main>
        <AboutSection />
        <CarouselSection />
        <AvailableOffersSection />
        <RoomsSection />
        <HolidaysSection />
        <WishSection />
    </main>
</template>

<style lang="scss" scoped>

main {
    position: relative;
    z-index: 1;
    margin-top: 100vh;
}


</style>
