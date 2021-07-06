<template>
  <div id="app" v-if="steps">
    <div>
      <h3>{{activity.name}}</h3>
      <h6>{{steps>0 ? rawData.steps[activeStep].type:''}} - {{activeStep+1}}/{{steps}}</h6>
    </div>
    <div>
      <Home :steps="steps" :activeStep="activeStep" :activity="activity" :rawData="rawData"/>
    </div>
    <div>
      <button v-on:click="stepPrevious()" class="btn btn-primary next-button">Previous</button>
      <button v-on:click="stepNext()" class="btn btn-primary next-button">Next</button>
    </div>
  </div>
</template>

<script>
import Home from './components/Home.vue'

import axios  from "axios"

const GET_ACTIVITY = `
  query activity($id: String, $shortCode: String){
	activity(id: $id, shortCode: $shortCode) {
    activity {
      id
      name
      displayName
      state
      uuid
      publishedRevision {
        rawData
      }
      displayLanguage
      scoringLanguage
      assets {
        id
        url
      }
    }
    scoring {
      endpoint
      token
      apiKey
      ttsServer
    }
  }
}
`;

export default {
  name: 'App',
  data () {
    return {
      activity: [],
      rawData:[],
      steps:0,
      activeStep:0
    };
  },
  methods:{
    async getActivity(){
      try {
        const res = await axios.post('https://api-dev.speak.ef.com/graphql', {query:GET_ACTIVITY, variables: {"shortCode": "WKZKPR"}});
        this.activity = res.data.data.activity.activity;
        this.rawData = JSON.parse(this.activity.publishedRevision.rawData);
        this.steps = this.rawData.steps.length;
        console.log(this.rawData);
      } catch (e) {
        console.log('err', e)
      }
    },
    stepNext:function(){
      if(this.activeStep<this.steps){
        this.activeStep += 1;
      }
    },
    stepPrevious:function(){
      if(this.activeStep>0){
        this.activeStep -= 1;
      }
    }
  },
  mounted: async function(){
    await this.getActivity()
  },
  components: {
    Home
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background:white;
  max-width: 750px;
  padding: 20px 20px 25px;
  margin: 10% auto;
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-shadow: 0 2px 16px 0 rgb(25 25 25 / 10%);
  border-radius: 4px;

}
body{
  background: rgb(228, 242, 247)!important;
}
h1{
  font-size: 2rem;
  font-weight: 400;
  margin-bottom: 24px;
}
.next-button{
  margin:5% 1% 0 0;
}
</style>
