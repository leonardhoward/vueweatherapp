<template>
<!-- rain effect borrowed from https://codepen.io/jerrylow/pen/KaPvNa -->
<!-- snow effect borrowed from https://codepen.io/alphardex/pen/dyPorwJ  -->
<!--  -->
  <div id="app"
  :style="{ 'background-color': background }">
<div class="input">
<h1> Weather App </h1>
<p> Search the name of a city or a town to check the current weather! </p>
  <div class="input">
    <input type="text" placeholder="city/town name"
        v-model="query" 
        /> 
        <button @click="fetchWeather">Search for city
        </button> 
   </div>

<div class="weather-wrap" v-if="typeof weather.main != 'undefined'"> 

       <div>          
        {{ weather.name }}, {{ Math.round((weather.main.temp - 273.15) * 9/5 + 35) }}°F,
        {{ describe.description }}
        <img :src="icon"> 
        </div>
        </div>
        </div>

         <div v-if= "notSet"> 
    Oops! City was not found. Please check the city's spelling and try again.
    </div>
   
         <div class="background-container">
    <div class="background-layer layer-0" data-parallax-speed="0.05" data-max-scroll="565"></div>
    <div class="background-layer layer-1" data-parallax-speed="0.1" data-max-scroll="565"></div>
    <div class="background-layer layer-2" data-parallax-speed="0.3" data-max-scroll="565"></div>
    <div class="background-layer layer-3" data-parallax-speed="0.5" data-max-scroll="565"></div>
    <div class="background-layer layer-4" data-parallax-speed="0.7" data-max-scroll="565"></div>
    <div class="background-layer layer-5" data-parallax-speed="0.9" data-max-scroll="565"></div>
  </div>

    <div 
    v-show="clouds >= 20"
    class= "clouds">
      <img src="./img/cloud6.png" style="--i:1;">
      <img src="./img/cloud7.png" style="--i:2;">
      <img src="./img/cloud8.png" style="--i:3;">
      <img src="./img/cloud9.png" style="--i:4;">
      <img src="./img/cloud10.png" style="--i:5;"> 
    </div>
    

     ​<div
     v-if="timeNow < sunSet"
      class="theSun"></div>

      <div v-else-if="sunSet < timeNow"
      class="theMoon">
        </div>

        <div v-else></div>

        

<div
 v-show="weather.rain">
<i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i><i class="rain"></i>
</div>

<div v-show="weather.snow">
<div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div>
</div>

<div v-show="describe.description == 'light snow'">
<div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div><div class="snow"></div>
</div>
   </div>
 
</template>

<script>

export default {
  name: 'app',
   data: function()  {
        return {
        url_base: 'https://api.openweathermap.org/data/2.5/',
        api: '69f11ed696371e9d14b77fc98b82349c',
        weather: '',
        notSet: false,
        query:'',
        showClouds: false,
        clouds: 10,
        describe: '',
        icon_base: 'http://openweathermap.org/img/wn/10d@2x.png',
        icon:'',
        background: '#41b9ddd2',
        timeNow: 0,
        sunSet: 0,
        night: ' #343636d2'
        }
    },
    methods: {
        fetchWeather: function(e){
            
                fetch(`${this.url_base}weather?q=${this.query}&appid=${this.api}`)
                .then(res =>  {
                    return res.json();
                }).then(this.setResults)
                  if(!this.weather.startsWith("#")){
                    this.notSet = true
                  } 
        },
        setResults: function(results){
            this.weather= results
            this.clouds= Object.values(this.weather.clouds).pop()
            this.describe= Object.values(this.weather.weather).pop()
            this.icon= `http://openweathermap.org/img/wn/${this.describe.icon}.png`
            this.timeNow= this.weather.dt
            this.sunSet= this.weather.sys.sunset
            this.setBackground()
            this.notSet = false
          
        },
        setBackground: function(){


          if(this.sunSet < this.timeNow){
              this.background = ' #2a2a35'
          } else if (this.weather.rain){
              this.background = '#7c8e94d2'
          } else if (this.clouds >= 40){
              this.background = '#7c8e94d2'
          }else {
              this.background = '#41b9ddd2'
          }
          console.log(this.background)
        }
       
        
    }
 
}
</script>

<style lang="scss">

* { margin: 0 !important; }

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #f7f3f3;
    width: 100vw;
    height: 100vh;
     position: fixed;
      background-color: rgba(65, 185, 221, 0.822);
      background-size: 100%;
  transition: 0.4s;
   z-index: -1;
}


h1, h2 {
  font-weight: normal;
  font-size: 2rem;
  padding-top: 1em;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

p {
  padding: 0 1em 0 1em;
}

a {
  color: #42b983;
}



.input {
  z-index: 30;
  position: relative;
}

.background-layer {
  width: 100%;
  height: 95%; 
  position: fixed;
  background-position: bottom center;
  background-repeat: repeat-x;
  background-size: 100vw 100% ;
}

  
  .layer-1 {
    top: 10px;
    z-index: 1;
    background-image: url('./img/layer-1.png');
    overflow: hidden;
  }
  /* .layer-2 {
    top: -50px;
    z-index: 2;
    background-image: url('./img/layer-2.png');
   
  }
  .layer-3 {
    top: -10px;
    z-index: 3;
    background-image: url('./img/layer-3.png');
  } */
  .layer-4 {
    top: 70px;
    z-index: 4;
      background-image: url('./img/layer-5.png');
      overflow: hidden;
  }
  .layer-5 {
    top: 110px;
    z-index: 5;
    background-image: url('./img/layer-4.png');
    overflow: hidden;
  }

.theSun {
  width:100px;
  height:100px;
  top:60%;
  left:30%;
  position:absolute;
  animation:sunRising 10s linear forwards;
  border-radius:50%;
  -moz-border-radius:50%;
  /* Safari and Chrome */
  -webkit-animation:sunRising 10s linear forwards;
  background-image: -moz-radial-gradient(45px 45px 45deg, circle cover, yellow 0%, orange 100%, red 95%);
	background-image: -webkit-radial-gradient(45px 45px, circle cover, yellow, orange);
	background-image: radial-gradient(45px 45px 45deg, circle cover, yellow 0%, orange 100%, red 95%);
}

.theMoon {
  width:100px;
  height:100px;
  top:60%;
  left:30%;
  position:absolute;
  animation:moonRising 10s linear forwards;
  border-radius:50%;
  -moz-border-radius:50%;
  /* Safari and Chrome */
  -webkit-animation:moonRising 10s linear forwards;
  background-image: -moz-radial-gradient(45px 45px 45deg, circle cover, rgb(209, 209, 204) 0%, rgb(161, 160, 158) 100%, rgb(107, 105, 105) 95%);
	background-image: -webkit-radial-gradient(45px 45px, circle cover, rgb(209, 209, 204) 0%, rgb(161, 160, 158) 100%, rgb(107, 105, 105) 95%);
	background-image: radial-gradient(45px 45px 45deg, circle cover,rgb(209, 209, 204) 0%, rgb(161, 160, 158) 100%, rgb(107, 105, 105) 95%);
}
@keyframes sunRising
{
  0%   {top:60%;left:30%;}
  25%  {top:50%;left:40%;}
  50%  {top:40%;left:50%;}
  75%  {top:30%;left:60%;}
  100% {top:20%;left:70%;}
}

@-webkit-keyframes sunRising /* Safari and Chrome */{
    0%   {top:60%;left:30%;}
  25%  {top:50%;left:40%;}
  50%  {top:40%;left:50%;}
  75%  {top:30%;left:60%;}
  100% {top:20%;left:70%;}
}

@keyframes moonRising
{
  0%   {top:60%;left:30%;}
  25%  {top:50%;left:40%;}
  50%  {top:40%;left:50%;}
  75%  {top:30%;left:60%;}
  100% {top:20%;left:70%;}
}

@-webkit-keyframes moonRising /* Safari and Chrome */{
    0%   {top:60%;left:30%;}
  25%  {top:50%;left:40%;}
  50%  {top:40%;left:50%;}
  75%  {top:30%;left:60%;}
  100% {top:20%;left:70%;}
}
 
  .clouds {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 140%;
    
    overflow: hidden;
  }

  .clouds img {
    position: absolute;
    bottom: 5vh;
    max-width: 100%;
    animation: cloudStart calc(10s * var(--i)) linear infinite;
  }
 
 @keyframes cloudStart {
   0% {
     transform: translateX(-150%);
   }
   100% {
     transform: translateX(100%)
   }
 }

  
 .rain {
  background: rgb(180, 180, 180);
  background: linear-gradient(to bottom, rgba(255,255,255,0) 0%, #ffffff 100%);
  height: 50px;
  position: fixed;
  width: 2px;
  z-index: 20;
} 

$rain: 150;

@for $i from 1 through $rain {
  $top: (random(50) + 50) * 1%;
  $left: random(100) * 1%;
  $opacity: (random(30) + 30) * 0.02;
  $delay: random(20) - 1s;

  .rain:nth-of-type(#{$i}) {
    animation-name: rain-#{$i};
    animation-delay: $delay;
    animation-duration: random(6) + 4s;
    animation-iteration-count: infinite;
    left: $left;
    opacity: $opacity;
    top: -$top;
  }

  @keyframes rain-#{$i} {
    0% {
      left: $left;
      opacity: $opacity;
      top: -$top;
    }
    100% {
      opacity: 0;
      top: $top + 40%;
    }
  } 
}

@function random_range($min, $max) {
  $rand: random();
  $random_range: $min + floor($rand * (($max - $min) + 1));
  @return $random_range;
}

.snow {
  $total: 200;
  position: fixed;
  width: 10px;
  height: 10px;
  background: white;
  border-radius: 50%;
  z-index: 20;
  overflow:hidden;

  @for $i from 1 through $total {
    $random-x: random(1000000) * 0.0001vw;
    $random-offset: random_range(-100000, 100000) * 0.0001vw;
    $random-x-end: $random-x + $random-offset;
    $random-x-end-yoyo: $random-x + ($random-offset / 2);
    $random-yoyo-time: random_range(30000, 80000) / 100000;
    $random-yoyo-y: $random-yoyo-time * 100vh;
    $random-scale: random(10000) * 0.0001;
    $fall-duration: random_range(10, 30) * 1s;
    $fall-delay: random(30) * -1s;

    &:nth-child(#{$i}) {
      opacity: random(10000) * 0.0001;
      transform: translate($random-x, -10px) scale($random-scale);
      animation: fall-#{$i} $fall-duration $fall-delay linear infinite;
    }

    @keyframes fall-#{$i} {
      #{percentage($random-yoyo-time)} {
        transform: translate($random-x-end, $random-yoyo-y) scale($random-scale);
      }
      
      to {
        transform: translate($random-x-end-yoyo, 100vh) scale($random-scale);
      }
    }
  }
}

@media screen and (max-width: 1370px) {

  h1, h2 {
    padding-top: 1em;
    font-size: 3rem;
  }

  p {
    padding: 0 1em 0 1em;
    font-size: 1.5rem;
  }
.background-layer {
  width: 100vw;
  height: 100vh;
  position: fixed;
  left: 0;
  background-position: bottom center;
  background-repeat: repeat-x;
  background-size: 100vw 40%;
}


}

@media screen and (max-height: 820px) {
 h1, h2 {
    padding-top: 2em;
    font-size: 1.7rem;
  }

  p {
    padding: 0 1em 0 1em;
    font-size: 1rem;
  }

  .background-layer {
  width: 100vw;
  height: 100vh;
  position: fixed;
  left: 0;
  background-position: bottom center;
  background-repeat: repeat-x;
  background-size: 100vw 50%;
}

  .layer-1 {
    top: 30px;
    z-index: 1;
    background-image: url('./img/layer-1.png');
  }
}


@media screen and (max-width: 850px)  {

   h1, h2 {
    padding-top: .5em;
    font-size: 1.7rem;
  }

  p {
    padding: 0 1em 0 1em;
    font-size: 1rem;
  }

 .background-layer {
  width: 100vw;
  height: 100vh;
  position: fixed;
  left: 0;
  top: 0;
  background-position: bottom center;
  background-repeat: repeat-x;
  background-size: 100% 80%;
}
 .layer-1 {
    top: 20px;
    z-index: 1;
    background-image: url('./img/layer-1.png');
  }

  .layer-4 {
    top: 60px;
    z-index: 4;
      background-image: url('./img/layer-5.png');
  }

   .layer-5 {
    top: 160px;
    z-index: 5;
    background-image: url('./img/layer-4.png');
  }

  .clouds {
    position: absolute;
    bottom: 5%;
    left: 0;
    width: 100%; 
    overflow: hidden;
  }

  .clouds img{
    height: 300px;
    width: auto;
  }


 .theSun {
  width:100px;
  height:100px;
  top: 90vh;
  left:30%;
  position:absolute;
  animation:sunRising 10s linear forwards;
  border-radius:50%;
  -moz-border-radius:50%;
  /* Safari and Chrome */
  -webkit-animation:sunRising 10s linear forwards;
  background-image: -moz-radial-gradient(45px 45px 45deg, circle cover, yellow 0%, orange 100%, red 95%);
	background-image: -webkit-radial-gradient(45px 45px, circle cover, yellow, orange);
	background-image: radial-gradient(45px 45px 45deg, circle cover, yellow 0%, orange 100%, red 95%);
}

.theMoon {
  width:100px;
  height:100px;
  top:60%;
  left:30%;
  position:absolute;
  animation:moonRising 10s linear forwards;
  border-radius:50%;
  -moz-border-radius:50%;
  /* Safari and Chrome */
  -webkit-animation:moonRising 10s linear forwards;
  background-image: -moz-radial-gradient(45px 45px 45deg, circle cover, rgb(209, 209, 204) 0%, rgb(161, 160, 158) 100%, rgb(107, 105, 105) 95%);
	background-image: -webkit-radial-gradient(45px 45px, circle cover, rgb(209, 209, 204) 0%, rgb(161, 160, 158) 100%, rgb(107, 105, 105) 95%);
	background-image: radial-gradient(45px 45px 45deg, circle cover,rgb(209, 209, 204) 0%, rgb(161, 160, 158) 100%, rgb(107, 105, 105) 95%);
}

}



@media screen and (max-width: 420px)  {
 h1, h2 {
    padding-top: 2em;
    font-size: 1.7rem;
  }

  p {
    padding: 0 1em 0 1em;
    font-size: 1rem;
  }

.background-layer {
  width: 100vw;
  height: 100vh;
  position: fixed;
  left: 0;
  background-position: bottom center;
  background-repeat: repeat-x;
  background-size: 180vw 50%;
}


  .clouds {
    position: absolute;
    bottom: 14%;
    left: 0;
    width: 1080px; 
    overflow: hidden;
  }

  .clouds img{
    height: 300px;
    width: 1080px;
  }
}


</style>
