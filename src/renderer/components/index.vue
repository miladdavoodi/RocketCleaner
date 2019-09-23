<template>
    <div class="content">

        <div class="cloudSky"></div>
        
        <div v-bind:class="{slideInUp:!startClean,fadeOutUp:startClean,'delay-1s':startClean}" class="Rocket animated "></div>


        <div v-bind:class="{fadeIn:!startClean,'delay-1s':!startClean,fadeOutUp:startClean}" class="Fire animated">
            <span class="infinite animated zoomIn"></span>
            <span class="infinite animated zoomIn"></span>
        </div>

        <div  v-bind:class="{roundC:startClean}" class="Scan" v-on:click="run">
            <span v-if="!startClean">SCAN</span>
            <span v-if="startClean">{{Progress}}%</span>
            <div v-if="startClean" v-bind:class="{rotating:startClean}" class="loadingC"></div>
        </div>

        <div  v-bind:class="{fadeIn:!startClean,'delay-1s':!startClean,fadeOut:startClean}" class="RocketLine animated"></div>

        <ul  v-bind:class="{fadeIn:!startClean,fadeOut:startClean}" class="cloud animated">
            <li class="infinite animated pulse" v-for="n in 8"></li>
        </ul>


    </div>
</template>
<script>
    export default {
        data(){
            return{
                startClean:false,
                Progress:0,
            }
        },
        watch:{
            startClean:function (val) {

                if (val==true) {

                    let _this = this;
                    let timterInterval = setInterval(function () {
                        if (_this.Progress <= 90) {
                            _this.Progress = _this.Progress + 10;
                        } else {
                            clearInterval(timterInterval);
                            _this.Progress = 0;
                            _this.startClean = false;
                        }
                    }, 600);
                }
            }
        },
        methods:{
            run(){
                this.startClean = true;
            }
        }
    }
</script>

<style>
    @import "../../../static/css/animate.css";
    body{
        background: rgba(0,0,0,0);
    }
    div.content{
        width: 100%;
        height: 540px;
        background-image: -moz-linear-gradient( 61deg, rgb(31,43,94) 0%, rgb(141,55,82) 100%);
        background-image: -webkit-linear-gradient( 61deg, rgb(31,43,94) 0%, rgb(141,55,82) 100%);
        background-image: -ms-linear-gradient( 61deg, rgb(31,43,94) 0%, rgb(141,55,82) 100%);
        border-radius: 20px;
    }
    div.cloudSky{
        width: 100%;
        height: 131px;
        background: url("../../../static/image/cloud.png");
        background-size: 349px 131px;
        position: absolute;
        top: 50px;
        animation: animatedBackground 500s linear infinite;
    }

    @keyframes animatedBackground {
        from {
            background-position: 0 0;
        }
        /*use negative width if you want it to flow right to left else and positive for left to right*/
        to {
            background-position: -10000px 0;
        }
    }

    @-webkit-keyframes rotating /* Safari and Chrome */ {
        from {
            -webkit-transform: rotate(0deg);
            -o-transform: rotate(0deg);
            transform: rotate(0deg);
        }
        to {
            -webkit-transform: rotate(360deg);
            -o-transform: rotate(360deg);
            transform: rotate(360deg);
        }
    }
    @keyframes rotating {
        from {
            -ms-transform: rotate(0deg);
            -moz-transform: rotate(0deg);
            -webkit-transform: rotate(0deg);
            -o-transform: rotate(0deg);
            transform: rotate(0deg);
        }
        to {
            -ms-transform: rotate(360deg);
            -moz-transform: rotate(360deg);
            -webkit-transform: rotate(360deg);
            -o-transform: rotate(360deg);
            transform: rotate(360deg);
        }
    }

    div.loadingC{
        background: url("../../../static/image/loading.png");
        background-size: cover;
        width: 74px;
        height: 74px;
        position: absolute;
        top: 14px;
        margin: 0 auto;
        left: 0;
        right: 0;
    }
    .rotating {
        -webkit-animation: rotating 2s linear infinite;
        -moz-animation: rotating 2s linear infinite;
        -ms-animation: rotating 2s linear infinite;
        -o-animation: rotating 2s linear infinite;
        animation: rotating 2s linear infinite;
    }

    div.Rocket{
        background: url("../../../static/image/Rocket.png");
        background-size: cover;
        width: 94px;
        height: 203px;
        position: fixed;
        margin: 0 auto;
        left: 0;
        right: 0;
        bottom: 170px;
        z-index: 5;
    }
    ul.cloud{
        position: absolute;
        width: 100%;
        height: 400px;
        bottom: 23px;
        overflow: hidden;
    }
    ul.cloud li{
        list-style: none;
        position: absolute;
        background: #8b8ba8;
        width: 70px;
        height: 70px;
        border-radius: 100px;
    }
    ul.cloud li:nth-child(1){
        bottom: -30px;
        right: 50px;
    }
    ul.cloud li:nth-child(2){
        bottom: -40px;
        right: 100px;
        width: 110px;
        height: 110px;
    }
    ul.cloud li:nth-child(3){
        bottom: 40px;
        right: 150px;
        width: 50px;
        height: 50px;
    }

    ul.cloud li:nth-child(4){
        bottom: -30px;
        left: 50px;
    }
    ul.cloud li:nth-child(5){
        bottom: -40px;
        left: 100px;
        width: 110px;
        height: 110px;
    }
    ul.cloud li:nth-child(6){
        bottom: 40px;
        left: 150px;
        width: 50px;
        height: 50px;
    }

    ul.cloud li:nth-child(7){
        bottom: -40px;
        left: 110px;
        width: 80px;
        height: 80px;
        background: #c2c2da;
        box-shadow: 0 0 20px 0 rgba(0,0,0,0.2);
    }
    ul.cloud li:nth-child(8){
        bottom: -40px;
        right: 110px;
        width: 90px;
        height: 90px;
        background: #c2c2da;
        box-shadow: 0 0 20px 0 rgba(0,0,0,0.2);
    }


    div.RocketLine{
        position: absolute;
        bottom: 20px;
        left: 0;
        right: 0;
        margin: 0 auto;
        background: #8b8ba8;
        width: 40px;
        height: 200px;
        border-radius: 100px;
    }
    div.Fire{
        background-image: -moz-linear-gradient( 108deg, rgb(255,216,184) 0%, rgb(254,191,242) 100%);
        background-image: -webkit-linear-gradient( 108deg, rgb(255,216,184) 0%, rgb(254,191,242) 100%);
        background-image: -ms-linear-gradient( 108deg, rgb(255,216,184) 0%, rgb(254,191,242) 100%);
        width: 24px;
        height: 63px;
        border-radius: 100%;
        position: fixed;
        margin: 0 auto;
        z-index: 3;
        left: 0;
        right: 0;
        bottom: 130px;
        box-shadow: 0 0 20px 0 rgba(0,0,0,0.2);
    }
    div.Fire span{
        position: absolute;
        width: 14px;
        height: 43px;
        border-radius: 100%;
        z-index:5;
        right: 15px;
        bottom: -10px;
        background-image: -moz-linear-gradient( 108deg, rgb(255,216,184) 0%, rgb(254,191,242) 100%);
        background-image: -webkit-linear-gradient( 108deg, rgb(255,216,184) 0%, rgb(254,191,242) 100%);
        background-image: -ms-linear-gradient( 108deg, rgb(255,216,184) 0%, rgb(254,191,242) 100%);
        box-shadow: 0 0 20px 0 rgba(0,0,0,0.2);
        opacity: 0.8;
    }
    div.Fire span:last-child{
        right: -5px;
        height: 33px;
        opacity: 0.3;
    }

    div.Scan{
        overflow: hidden;
        width: 100px;
        height: 100px;
        background-image: -moz-linear-gradient( 61deg, rgb(31,43,94) 0%, rgb(210,55,82) 100%);
        background-image: -webkit-linear-gradient( 61deg, rgb(31,43,94) 0%, rgb(210,55,82) 100%);
        background-image: -ms-linear-gradient( 61deg, rgb(31,43,94) 0%, rgb(210,55,82) 100%);
        border-radius: 45px;
        position: absolute;
        bottom: 0;
        z-index: 8;
        left: 0;
        right: 0;
        margin: 0 auto;
        box-shadow: 0 0 20px 0 rgba(0,0,0,0.3),0 0 0 5px rgba(0,0,0,0.2) inset;
        transition: all 0.4s;
        cursor: pointer;
    }
    div.Scan.roundC{
        border-radius: 100px;
    }
    div.Scan:hover{
        background-image: -moz-linear-gradient( 61deg, rgb(31,43,94) 20%, rgb(210,55,82) 100%);
        background-image: -webkit-linear-gradient( 61deg, rgb(31,43,94) 20%, rgb(210,55,82) 100%);
        background-image: -ms-linear-gradient( 61deg, rgb(31,43,94) 20%, rgb(210,55,82) 100%);
    }
    div.Scan span{
        text-align: center;
        display: block;
        font-family: Arial,serif;
        font-weight: bold;
        font-size: 19px;
        padding-top: 38px;
        color: #fff;
    }
</style>