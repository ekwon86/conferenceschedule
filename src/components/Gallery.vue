<template>
    <div>
        <transition name="slide-left-fade">
            <div class="jumbotron" v-if="showGallery">
                <h1 class="display-2">Gallery</h1>
                <a class="twitter-timeline"  href="https://twitter.com/hashtag/laserappsoftware" data-widget-id="893120359381123072">#laserappsoftware Tweets</a>
            </div>
        </transition>
    </div>
</template>

<script>
    export default {
        data(){
            return{
                showGallery: false
            }
        },
        methods: {
            getTwitterData(){

            }
        },
        mounted: function(){
            let self = this;
            setTimeout(function(){
                self.showGallery = true;
            }, 500);
        }
    }
</script>

<style scroped>
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
</style>