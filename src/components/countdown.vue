<template>
    <div class="row align-bottom"  id="countdown">
        <div class="col-3 padding"><span  class="rond" :class="{shadow2: heures == '00'}" id="jours" :style="{bottom: postionJours + '%' }">{{jours}} jours</span></div>
        <div class="col-3 padding"><span class="rond" :class="{shadow2: minutes == '00'}" id="heures" :style="{bottom: postionHeures + '%' }">{{heures}} heures</span></div>
        <div class="col-3 padding"><span class="rond" :class="{shadow2: secondes == '00'}" id="minutes" :style="{bottom: postionMinutes + '%' }">{{minutes}} minutes</span></div>
        <div class="col-3 padding" ><span class="rond" id="secondes" :style="{bottom: postionSeconde + '%' }">{{secondes}} secondes </span></div>
        <!--:style="{paddingBottom: postionSeconde + 'vh' }"-->
    </div>
</template>

<script>
    export default {
        name: "countdown",
        data: function () {
            return {
                mois:0,
                jours:0,
                heures:0,
                minutes:0,
                secondes:0,
                MaxMinSec: 60,
                Maxheures:24,
                MaxDay:31,
                postionSeconde:0,
                positionMinutes:0,
                postionHeures:0,
                postionJours:0

            }
        },
        methods: {
            dateInit: function () {
                 let dateline = new Date ('2018-07-23T17:00:00')
                let dateNow = new Date()
                let dateInterval = dateline - dateNow
                let date = new Date(dateInterval);
                let mois = date.getMonth()
                let jours = date.getDate();
                let heures = date.getHours();

                let minutes = "0" + date.getMinutes();
                minutes = minutes.substr(-2)
                let secondes = "0" + date.getSeconds();
                secondes = secondes.substr(-2)


                this.mois = mois
                this.jours = jours
                this.heures = heures
                this.minutes = minutes
                this.secondes = secondes

                //position
                this.postionSeconde = secondes*80/60
                this.postionMinutes = minutes*80/60
                this.postionHeures = heures*80/24
                this.postionJours = jours*80/31

            },
        },
        mounted() {
            setInterval(()=>{ this.dateInit() }, 1000);
        }
    }
</script>

<style scoped>
    #countdown {
        margin-left: 8vw;
        margin-right: 8vw;
        height: 100vh;
    }
    .padding {
        padding: 50px;
        align-items: end;
    }
    .rond {
        text-align: center;
        width: 150px;
        height: 150px;
        border-radius: 50%;
        position: absolute;
        line-height: 150px;
        box-shadow: 10px 10px;
        transition:1s;
    }
    #jours {
        background-color: #4286f4;
       /* animation: shadow2 5000000s linear infinite*/
    }
    #heures {
        background-color: #2fef66;
        /*animation: shadow2 3600s linear infinite*/
    }
    #minutes {
        background-color: #e8ef2f;
        /*animation: shadow2 60s linear infinite*/
    }
    #secondes {
        background-color: #ef8f2f;
        animation: shadow2 1s linear infinite
    }
    .shadow2 {animation: shadow2 1s linear infinite}
    @keyframes shadow {
        0% {box-shadow: 10px 10px;}
        25% {box-shadow: -10px 10px;}
        50% {box-shadow: -10px -10px;}
        75% {box-shadow: 10px -10px;}
        100% {box-shadow: 10px 10px;}
    }
    @keyframes shadow2 {
        0% {
            box-shadow: 10px 10px;
            transform: translate(0px,0px);
        }
        80% {box-shadow: 0px 0px;
            transform: translate(10px,10px)}
        100% {
            box-shadow: 10px 10px;
            transform: translate(0px,0px);
        }
    }
</style>