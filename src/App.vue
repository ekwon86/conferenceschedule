<template>
  <div id="app">
      <transition name="fade">
          <schedule :schedule="confSchedule" v-if="showSchedule" class="content"></schedule>
      </transition>
      <transition name="fade">
          <floor-plan :schedule="confSchedule" :weather="weather" v-if="showFloorPlan" class="content"></floor-plan>
      </transition>
      <div class="overlay"></div>
  </div>
</template>

<script>
import axios from 'axios';
import Schedule from './components/Schedule.vue';
import FloorPlan from './components/FloorPlan.vue';
import Gallery from './components/Gallery.vue';
export default {
    name: 'app',
    data(){
      return {
        count: 1,
        showSchedule: true,
        showFloorPlan: false,
        showGallery: false,
        confSchedule: [],
        weather: {
            currentTemp: '',
            weatherIconUrl: '',
            description: ''
        }
      }
    },
    methods: {
        getData(){
            let self = this;
            let t = new Date();
            let tmpTime = t.toLocaleTimeString();
            let tmpHour = tmpTime.substr(0, tmpTime.indexOf(':'));
            let tmpMinute = tmpTime.substr(tmpTime.indexOf(':'), 3).slice(1);
            let parsedHour = parseInt(tmpHour);
            let parsedMinute = parseInt(tmpMinute)/60;
            let currentTime;

            if(tmpTime.includes('PM')){
                if(parsedHour === 1){
                    parsedHour = 13;
                } else if (parsedHour === 2){
                    parsedHour = 14;
                } else if (parsedHour === 3){
                    parsedHour = 15;
                } else if (parsedHour === 4){
                    parsedHour = 16;
                } else if (parsedHour === 5){
                    parsedHour = 17;
                } else if (parsedHour === 6){
                    parsedHour = 18;
                } else if (parsedHour === 7){
                    parsedHour = 19;
                } else if (parsedHour === 8){
                    parsedHour = 20;
                } else if (parsedHour === 9){
                    parsedHour = 21;
                } else if (parsedHour === 10){
                    parsedHour = 22;
                }
                currentTime = parsedHour + parsedMinute;
            } else {
                currentTime = parsedHour + parsedMinute;
            }

            axios.get('http://api.wunderground.com/api/59173ab4a817b423/conditions/q/CA/San_Francisco.json').then(function(response){
                self.weather.currentTemp = response.data.current_observation.feelslike_f;
                self.weather.description = response.data.current_observation.weather;
                self.weather.weatherIconUrl = 'https://icons.wxug.com/i/c/j/' + response.data.current_observation.icon + '.gif';
            }).catch(function(error){
                console.log(error);
            });

            axios.get('https://api.fieldbook.com/v1/5976160af677720300490797/lasschedule').then(function(response){
                let tmpSchedule = response.data;
                for(let i=0; i < tmpSchedule.length; i++) {
                    //Date
                    let d = new Date();
                    let currentDate = d.toLocaleDateString();
                    let reformattedCurrentDate = currentDate.split("/").reverse();

                    //Reformat date to proper format
                    let datetmp = '0' + reformattedCurrentDate[2];
                    reformattedCurrentDate[2] = reformattedCurrentDate[1];
                    if(reformattedCurrentDate[2].length === 1){
                        reformattedCurrentDate[2] = '0' + reformattedCurrentDate[2];
                    }
                    reformattedCurrentDate[1] = datetmp;
                    reformattedCurrentDate = reformattedCurrentDate.join("-");

                    let dateOfEvent = tmpSchedule[i].date;

                    //Start Time of Event
                    let tmpStartTime = tmpSchedule[i].start_time;
                    let tmpStartHour = tmpStartTime.substr(0, tmpStartTime.indexOf(':'));
                    let tmpStartMinute = tmpStartTime.substr(tmpStartTime.indexOf(':'), 3).slice(1);
                    let parsedHour = parseInt(tmpStartHour);
                    let parsedMinute = parseInt(tmpStartMinute)/60;
                    let startTime;

                    if(tmpStartTime.includes('PM')){
                        if(parsedHour === 1){
                            parsedHour = 13;
                        } else if (parsedHour === 2){
                            parsedHour = 14;
                        } else if (parsedHour === 3){
                            parsedHour = 15;
                        } else if (parsedHour === 4){
                            parsedHour = 16;
                        } else if (parsedHour === 5){
                            parsedHour = 17;
                        } else if (parsedHour === 6){
                            parsedHour = 18;
                        } else if (parsedHour === 7){
                            parsedHour = 19;
                        } else if (parsedHour === 8){
                            parsedHour = 20;
                        } else if (parsedHour === 9){
                            parsedHour = 21;
                        } else if (parsedHour === 10){
                            parsedHour = 22;
                        }
                        startTime = parsedHour + parsedMinute;
                    } else {
                        startTime = parsedHour + parsedMinute;
                    }

                    self.confSchedule.push(tmpSchedule[i]);

                    if(reformattedCurrentDate === dateOfEvent){
                        if(currentTime < startTime){
                            self.confSchedule.push(tmpSchedule[i]);
                            console.log(self.confSchedule);
                        }
                    }
                }
            }).catch(function(error){
                console.log(error);
            });
        },
        refreshPage(){
            setTimeout(function(){
                location.reload();
            }, 900000);
        },
        cycleComponents(){
            let self = this;
            setInterval(function(){
                if(self.count === 1){
                    self.showFloorPlan = false;
                    self.showSchedule = true;
                    self.count = 2;
                } else if(self.count === 2){
                    self.showSchedule = false;
                    self.showFloorPlan = true;
                    self.count = 1;
                }
            }, 10000);
        }
    },
    mounted: function(){
        this.getData();
//        this.refreshPage();
        this.cycleComponents();
    },
    components: {
        'schedule': Schedule,
        'floor-plan': FloorPlan,
        'gallery': Gallery
    }
}
</script>

<style lang="scss">
    body {
        overflow: hidden;
    }
    #app {
        height: 100vh;
        width: 100vw;
        /*background: linear-gradient(141deg, #0fb8ad 0%, #1fc8db 51%, #2cb5e8 75%);*/
    }
    .content {
        position: absolute;
        z-index: 2;
        width: 100vw;
    }
    .overlay {
        position: absolute;
        width: 100vw;
        height: 100vh;
        background-color: rgba(255,255,255,0.9);
        z-index: 1;
    }
    .fade-enter-active, .fade-leave-active {
        transition: opacity .5s
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
        opacity: 0
    }
</style>
