<template>
	<div class="container">
    	<div class="row justify-content-center">
            <div class="col-md-12">
                <div class="card card-default">
                	<div class="card-header">Calendar Management
        			</div>
        			<div class="card-body">

                    <full-calendar   :event-sources="eventSources" :config="config"></full-calendar>
        			</div>

        		</div>  <!-- end card -->
        	</div>
        </div>
    </div>
</template>

<script>
import 'fullcalendar/dist/fullcalendar.css';
import { FullCalendar } from 'vue-full-calendar';

var moment = require('moment');
 var demoEvents = [
//var events = [
    {
      title : 'Sunny Out of Office',
      start : '2019-06-20',
      end : '2019-06-23'
    },
    {
        title : 'Meeting : ADS',
      start : '2019-07-18',
      end : '2019-07-19'
    }
]

    export default {
        components: {
            FullCalendar
        },
        mounted() {
            console.log('Component example 1234ขถถไทยบ้าง mounted.');

        },
        created(){

        },
        data () {
            return {
                config: {
                            locale: 'en',
                            defaultView: 'month',
                        },
                events: [
                            {
                                id: 1,
                                title: 'event1',
                                start: moment().hours(12).minutes(0),
                            },
                            {
                                id: 2,
                                title: 'event2',
                                start: moment().add(-1, 'days'),
                                end: moment().add(1, 'days'),
                                allDay: true,
                            },
                        ], 
                fcEvents : demoEvents,
                //fcEvents : Models,
                errors: [],
                Models: [],
                Data: {},
                eventSources: [
                    {
                        events(start, end, timezone, callback){
                            // http://localhost/uoait/public/task/getcalendar1
                            axios.get('http://localhost/uoait/public/task/getcalendar2').then(
                                    response=> {
                                        //console.log("cal data:" + response.data.calendardata);
                                        callback(response.data.calendardata);
                                    }
                                )
                        },
                        color: 'white',
                        textColor: 'black'
                    },
                    {
                        events(start, end, timezone, callback){
                            // http://localhost/uoait/public/task/getcalendar1
                            axios.get('http://localhost/uoait/public/software/getcalendar').then(
                                    response=> {
                                        //console.log("cal data:" + response.data.calendardata);
                                        callback(response.data.calendardata);
                                    }
                                )
                        },
                        color: 'blue',
                        textColor: 'yellow'
                    },
                    {
                        events(start, end, timezone, callback){
                            axios.get('http://localhost/uoait/public/logbook/getcalendarflag/0').then(
                                    response=> {
                                        callback(response.data.calendardata);
                                    }
                                )
                        },
                        color: 'red',
                        textColor: 'black'
                    },
                                        {
                        events(start, end, timezone, callback){
                            axios.get('http://localhost/uoait/public/logbook/getcalendarflag/1').then(
                                    response=> {
                                        callback(response.data.calendardata);
                                    }
                                )
                        },
                        color: 'yellow',
                        textColor: 'black'
                    },
                                        {
                        events(start, end, timezone, callback){
                            axios.get('http://localhost/uoait/public/logbook/getcalendarflag/9').then(
                                    response=> {
                                        callback(response.data.calendardata);
                                    }
                                )
                        },
                        color: 'green',
                        textColor: 'white'
                    },

                ],

            }
        },
        methods: {

            getData(page = 1){
                const url = '/uoait/public/task/getall?page=' + page ;
                axios.get(url)
                .then(response=>{
                    this.Models = response.data.tasks.data;
                    this.Data = response.data.tasks;
                    //this.fcEvents = response.data.events;
                   // console.log("models -> " + this.Models[0]);
                    console.log("==> data ->" + response.data);
                })
                .catch(error=>{
                    console.log(error)
                });
            },
            addEvent(){

            }
        }
    }
</script>

<style>
	.highlightText {
		background: yellow;
	}
</style>