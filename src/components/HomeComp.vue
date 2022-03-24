<template>
          <div id="app" :class="typeof  weather.main !== undefined  ? 'warm' : 'winter' ">
            <div class="form">
              <input @keypress.enter="searchAddress" class="input_search" type="text" placeholder="Enter address..." v-model="query"/>
              <div class="address" v-if=" weather.main !== undefined">
                  <h1 style="color: #ffff;font-weight: bolder"> {{weather.name}}, {{weather.sys.country}} </h1>
                  <div style="color: #ffff">{{getTime()}}</div>
                  <div class="deg">
                   {{Math.round((weather.main.temp)/10)}}℃
                  </div>
                <div style="color: #ffff;font-weight: bolder;font-size: 30px">{{weather.weather[0].main}}</div>

              </div>
            </div>

          </div>
</template>

<script>
import axios from 'axios'
export default {
  name: "HomeComp",
  data(){
    return{
      api_key:"11ad37619faf589835db88bf77429d76",
      urlBase:"https://api.openweathermap.org/data/2.5/",
      query:"",
      weather:{}
      }
    },


  methods:{
    searchAddress(){
        axios.get(`${this.urlBase}weather?q=${this.query}&unit=metric&APPID=${this.api_key}`)
    .then(res => {
      console.log(res.data)
      this.weather = res.data
    })
      .catch(err =>{
          console.log(err)
        alert('Please enter correct address!')
      })
    },
    getTime(){
      let current = new Date()
      return ` ${current.getDay()}/${current.getMonth()}/${current.getFullYear()} - ${current.toLocaleTimeString()}`
    }
  },
  update:{
    renderBackGround(){
      console.log('work')
    }
  }

}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Red Hat Mono', monospace;
}

.winter {
  background-image: url('../assets/winter.jpg');
  background-repeat: no-repeat;
  min-height: 100vh;
  background-size: cover;

}
.wrap{
  min-height: 100vh;
 background-color: rgba(0,0,0,0.2);
}

.warm{
  background-image: url('../assets/warm.jpg');
  background-repeat: no-repeat;
  min-height: 100vh;
  background-size: cover;
}
.form{
  margin: 0 auto;
  width: 60%;
}
.input_search{
  width: 100%;
  margin-top: 20%;
  height: 40px;
  border: none;
  outline: none;
  border-radius: 15px 0 15px 0;
  padding: 10px;
  box-shadow: 5px 5px 0 0  rgba(255,255,255,0.3);
  transition: 0.5s;
}

.input_search:focus{
  border-radius: 0 15px 0 15px;
  box-shadow: 5px 5px 0 0  rgba(0,0,0,0.2);
}
/*address*/
.address{
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
  transition: 0.4s;

}

.deg{

  height: 120px;
  padding-left: 30px;
  padding-right: 30px;
  background-color: rgba(255,255,255,0.4);
  border-radius: 10px;
  box-shadow: 5px 5px 0 0 rgba(0,0,0,0.4);
  margin-top: 20px;
  font-size: 50px;
  text-align: center;
  line-height: 120px;
  font-style: italic;
  color: #ffff;
  font-weight: bolder;
  text-shadow: 15px 0 0 15px rgba(0,0,0,0.5);
}
</style>