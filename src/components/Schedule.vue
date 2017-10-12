<template>
    <div>
        <transition name="slide-fade">
            <div class="jumbotron jumbo-style" v-if="showNextSession">
                <h1 class="next-session-text">Next Session</h1>
                <hr class="my-4">
                <p class="lead lead-text-title">{{ schedule[0].title }}</p>
                <p class="lead lead-text-time">{{ schedule[0].start_time }} to {{ schedule[0].end_time }}</p>
                <p class="lead lead-text-location">{{ schedule[0].location }}</p>
                <p class="lead lead-text-speaker" v-if="schedule[0].speakers">{{ schedule[0].speakers }}</p>
                <p class="lead lead-text-description" v-if="schedule[0].description">{{ schedule[0].description }}</p>
            </div>
        </transition>
        <div class="jumbo-side-container">
            <div class="upcoming-sessions">
                <transition name="slide-right-fade">
                    <div class="upcoming-sessions-content next-event" v-if="showFirst">
                        <h2 class="upcoming-sessions-title">{{ schedule[0].title }}</h2>
                        <h5 class="upcoming-sessions-time-location">{{ schedule[0].start_time }} to {{ schedule[0].end_time }}</h5>
                        <h5 class="upcoming-sessions-time-location">{{ schedule[0].location }}</h5>
                        <hr class="upcoming-sessions-hr">
                        <p class="upcoming-sessions-speaker" v-if="schedule[0].speakers"><strong>{{ schedule[0].speakers }}</strong></p>
                        <h5 class="upcoming-sessions-description" v-if="schedule[0].description">{{ schedule[0].description }}</h5>
                    </div>
                </transition>
            </div>
            <div class="upcoming-sessions">
                <transition name="slide-right-fade">
                    <div class="upcoming-sessions-content second-event" v-if="showSecond">
                        <h2 class="upcoming-sessions-title">{{ schedule[2].title }}</h2>
                        <h5 class="upcoming-sessions-time-location">{{ schedule[2].start_time }} to {{ schedule[2].end_time }}</h5>
                        <h5 class="upcoming-sessions-time-location">{{ schedule[2].location }}</h5>
                        <hr class="upcoming-sessions-hr">
                        <p class="upcoming-sessions-speaker" v-if="schedule[2].speakers"><strong>{{ schedule[2].speakers }}</strong></p>
                        <h5 class="upcoming-sessions-description" v-if="schedule[2].description">{{ schedule[2].description }}</h5>
                    </div>
                </transition>
            </div>
            <div class="upcoming-sessions">
                <transition name="slide-right-fade">
                    <div class="upcoming-sessions-content third-event" v-if="showThird">
                        <h2 class="upcoming-sessions-title">{{ schedule[3].title }}</h2>
                        <h5 class="upcoming-sessions-time-location">{{ schedule[3].start_time }} to {{ schedule[3].end_time }}</h5>
                        <h5 class="upcoming-sessions-time-location">{{ schedule[3].location }}</h5>
                        <hr class="upcoming-sessions-hr">
                        <p class="upcoming-sessions-speaker" v-if="schedule[3].speakers"><strong>{{ schedule[3].speakers }}</strong></p>
                        <h5 class="upcoming-sessions-description" v-if="schedule[3].description">{{ schedule[3].description }}</h5>
                    </div>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['schedule'],
        data(){
            return{
                showNextSession: false,
                showFirst: false,
                showSecond: false,
                showThird: false
            }
        },
        mounted: function(){
            let self = this;
            setTimeout(function(){
                self.showNextSession = true;
            }, 500);
            setTimeout(function(){
                self.showFirst = true;
            }, 500);
            setTimeout(function(){
                self.showSecond = true;
            }, 600);
            setTimeout(function(){
                self.showThird = true;
            }, 700);
        }
    }
</script>

<style scoped>
    .jumbo-style {
        height: 100vh;
        width: 60%;
        float: left;
        background-color: transparent;
        padding: 10% 2%;
    }
    .jumbo-side-container {
        width: 40%;
        height: 100vh;
        float: right;
        padding-top: 1%;
        padding-bottom: 1%;
        padding-right: 1%;
    }
    .upcoming-sessions {
        width: 100%;
        height: 33%;
        padding: 1%;
    }
    .upcoming-sessions-content {
        height: 100%;
        padding: 3% 5%;
        color: white;
        box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
    }
    .next-event {
        background-color: #36beeb;
    }
    .second-event {
        background-color: #2e9abf;
    }
    .third-event {
        background-color: #2a7fa3;
    }
    .upcoming-sessions-speaker {
        margin: 0;
        font-size: 1.25em;
    }
    .upcoming-sessions-hr {
        border-top: 1px solid white;
    }
    .upcoming-sessions-title {
        font-size: 2.25em;
        font-family: 'Oswald', sans-serif;
        text-shadow: 1px 1px rgba(30,30,30,0.05);
    }
    .upcoming-sessions-time-location {
        font-size: 1.5em;
    }
    .upcoming-sessions-description {
        font-size: 1.0em;
        line-height: 2em;
    }
    h1, h2, h3, h4, h5, h6{
        font-weight: 200;
    }
    .lead-text-title {
        font-size: 4em;
    }
    .lead-text-time, .lead-text-location {
        font-size: 2em;
    }
    .lead-text-description {
        text-align: justify;
        font-size: 1.5em;
        font-style: italic;
    }
    .lead-text-speaker {
        font-size: 2em;
    }
    .next-session-text {
        font-size: 8em;
        letter-spacing: 1vw;
        color: #36beeb;
        text-transform: uppercase;
        text-align: justify;
        text-shadow: 1px 1px rgba(30, 30, 30, 0.2);
        font-family: 'Oswald', sans-serif;
    }

    .slide-fade-enter-active {
        transition: all .3s ease;
    }
    .slide-fade-leave-active {
        transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }
    .slide-fade-enter, .slide-fade-leave-to
        /* .slide-fade-leave-active below version 2.1.8 */ {
        transform: translateY(50px);
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
        transform: translateX(50px);
        opacity: 0;
    }
</style>