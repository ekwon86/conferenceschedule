<template>
    <div class="floorPlan">
        <transition name="slide-left-fade">
            <div class="main-map-container" v-if="showMainMap">
                <div class="map-overlay">
                    <div class="regency-foyer" v-if="schedule[0].location === 'Regency Foyer'">
                        <div class="ringring regency-foyer-pulse"></div>
                        <div class="circle regency-foyer-circle"></div>
                    </div>
                    <div class="gold-ballroom" v-else-if="schedule[0].location === 'Gold Ballroom'">
                        <div class="ringring regency-foyer-pulse"></div>
                        <div class="circle regency-foyer-circle"></div>
                    </div>
                    <div class="grand-ballroom" v-else-if="schedule[0].location === 'Grand Ballroom'">
                        <div class="ringring regency-foyer-pulse"></div>
                        <div class="circle regency-foyer-circle"></div>
                    </div>
                </div>
                <img src="../assets/map2.png" class="map-pic" alt="map">
            </div>
        </transition>
        <transition name="slide-right-fade">
            <div class="side-container" v-if="showSideContent">
                <div class="weather-container">
                    <div class="weather-icon-container">
                        <img :src="weather.weatherIconUrl" class="weather-icon" alt="currentweather">
                    </div>
                    <div class="weather-desc-container">
                        <h1 class="temperature">{{ weather.currentTemp }}°</h1>
                        <h3 class="weather-desc">{{ weather.description }}</h3>
                    </div>
                </div>
                <div class="side-map-container">
                    <img src="../assets/sidemap.png" class="side-map" alt="sidemap">
                </div>
                <div class="legend-container">
                    <img src="../assets/dot.png" class="legend-dot" alt="dot">
                    <h1 class="next-session-text">Next</h1>
                    <h1 class="next-session-text">Session Location</h1>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
import axios from 'axios';
    export default {
        props: ['schedule', 'weather'],
        data(){
            return{
                showMainMap: false,
                showSideContent: false
            }
        },
        mounted: function(){
            let self = this;
            setTimeout(function(){
                self.showMainMap = true;
                self.showSideContent = true;
            }, 500);
        }
    }
</script>

<style scoped lang="scss">
    .ring-container {
        position: absolute;
    }
    .circle {
        width: 7em;
        height: 7em;
        background-color: #ffab35;
        border-radius: 50%;
    }
    .regency-foyer-circle {
        position: absolute;
        left: 2.25em;
        top: 3em;
    }
    .regency-foyer-pulse{
        position: absolute;
        top: 0.5em;
        left: -0.25em;
    }

    .ringring {
        border: 1em solid #ffab35;
        -webkit-border-radius: 999px;
        height: 12em;
        width: 12em;
        -webkit-animation: pulsate 2s ease-out;
        -webkit-animation-iteration-count: infinite;
        opacity: 0.0;
        position: absolute;
    }
    @-webkit-keyframes pulsate {
        0% {-webkit-transform: scale(0.1, 0.1); opacity: 0.0;}
        50% {opacity: 1.0;}
        100% {-webkit-transform: scale(1.2, 1.2); opacity: 0.0;}
    }

    .weather-icon-container {
        width: 25%;
        float: left;

    }
    .weather-desc-container {
        width: 75%;
        float: right;
        border-left: 1px solid rgba(171, 171, 171, 0.44);
        padding-left: 5%;
    }
    .floorPlan {
        background-color: white;
    }
    .slide-left-fade-enter-active {
        transition: all .3s ease;
    }
    .slideleft--fade-leave-active {
        transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }
    .slide-left-fade-enter, .slide-left-fade-leave-to
        /* .slide-fade-leave-active below version 2.1.8 */ {
        transform: translateX(-30px);
        opacity: 0;
    }

    .slide-right-fade-enter-active {
        transition: all .3s ease;
    }
    .slide-right-fade-leave-active {
        transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }
    .slide-right-fade-enter, .slide-right-fade-leave-to
        /* .slide-fade-leave-active below version 2.1.8 */ {
        transform: translateX(30px);
        opacity: 0;
    }
    .grand-ballroom {
        position: absolute;
        left: 62.5%;
        top: 20%;
    }
    .gold-ballroom {
        position: absolute;
        left: 71%;
        top: 60%;
    }
    .regency-foyer {
        position: absolute;
        left: 78.5%;
        top: 26%;
    }
    .map-icons {
        width: 10vw;
        color: rgba(255, 0, 0, 0.7);
    }
    .temperature {
        font-weight: 300;
        letter-spacing: 10px;
        font-size: 4em;
    }
    .weather-desc {
        font-weight: 300;
        letter-spacing: 5px;
        font-size: 3em;
        color: #36beeb;
        text-shadow: 1px 1px rgba(0,0,0,0.33);
    }
    .temperature, .weather-desc {
        font-family: 'Oswald', sans-serif;
        text-transform: uppercase;
    }
    .main-map-container {
        height: 100vh;
        width: 75%;
        float: left;
        padding: 3%;
        position: relative;
    }
    .map-overlay {
        width: 100%;
        height: 100%;
        position: absolute;
    }
    .map-pic {
        width: 100%;
        height: 100%;
    }
    .side-map {
        width: 100%;
        position: relative;
        top: 30%;
    }
    .weather-container {
        width: 100%;
        height: 25%;
        text-align: left;
        padding-top: 10%;
    }
    .weather-icon {
        width: 80%;
        position: relative;
        top: 1.5em;
    }
    .side-map-container {
        width: 100%;
        height: 35%;
    }
    .side-container {
        height: 100vh;
        width: 25%;
        float: right;
        padding-right: 2%
    }
    .legend-container {
        height: 35%;
        text-align: center;
    }
    .next-session-text {
        color: orange;
        margin-top: 0.5em;
        text-transform: uppercase;
        font-family: 'Oswald', sans-serif;
        letter-spacing: 3px;
    }
    .legend-dot {
        width: 7em;
        height: 7em;
    }
</style>
