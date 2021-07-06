<template>
  <div>
    <!-- first step -->
    <div class="content" v-if="activeStep==0 && steps > 0">
      <img class="container-img" :src="rawData.steps[activeStep].asset.url">
      <p>{{rawData.steps[activeStep].content}}</p>
    </div>
    <!-- second step -->
    <div class="content" v-if="activeStep==1 && steps > 0">
      <img class="avartar-img" :src="rawData.steps[activeStep].roles[0].avatarAsset.url">
      <div class="message-box">
        <div class="message-content">{{rawData.steps[activeStep].sentences[0].sentence}}</div>
      </div>
      <div class="right-aligined chat-message">
        <div class="res-message-box">
          <div class="message-content">{{rawData.steps[activeStep].sentences[1].sentence}}</div>
        </div>
        <img class="profile-img" :src="rawData.steps[activeStep].roles[1].avatarAsset.url">
      </div>
    </div>
    <!-- third step -->
    <div class="content" v-if="activeStep==2 && steps > 0">
      <h5>{{rawData.steps[activeStep].sentence}}</h5>
    </div>
    <!-- fourth step -->
    <div class="content" v-if="activeStep==3 && steps > 0">
      <video class="video" controls>
        <source :src="rawData.steps[activeStep].asset.url" type="video/mp4">
      </video>
      <h5>{{rawData.steps[activeStep].sentence}}</h5>
    </div>
    <!-- fifth step -->
    <div class="content" v-if="activeStep==4 && steps > 0">
      <h5>{{rawData.steps[activeStep].title}}</h5>
      <img class="container-imgage" :src="rawData.steps[activeStep].asset.url">
      <div class="sentence">{{rawData.steps[activeStep].sentences[1]}}</div>
      <div class="sentence">{{rawData.steps[activeStep].sentences[0]}}</div>
    </div>
    
    <!-- sixth step -->
    <div class="content" v-if="activeStep==5 && steps > 0">
      <img class="container-img" :src="rawData.steps[activeStep].asset.url">
      <p>{{rawData.steps[activeStep].content}}</p>
    </div>
    <!-- seventh step -->
    <div class="content" v-if="activeStep==6 && steps > 0">
      There is not result
    </div>
  </div>
</template>

<script>

export default {
  name: 'Home',

  props: ['activeStep','steps','activity','rawData']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.content {
  background-color: #fff;
  -webkit-box-flex: 1;
  -ms-flex-positive: 1;
  flex-grow: 1;
  -ms-flex-negative: 1;
  flex-shrink: 1;
  overflow: auto;
  padding: 20px 16px 0 16px;
  position: relative;
}
.container-img, .container-imgage{
  height: auto;
  max-width: 100%;
  cursor: pointer;
  -o-object-fit: cover;
  object-fit: cover;
}
.container-imgage{
  max-width: 80%;
  margin-top:10px
}
p{
  margin-top:3%;
}
.avartar-img, .profile-img{
  object-fit: cover;
  border-radius: 29.5px;
  width: 59px;
  height: 59px;
  border: 2px solid #eaeaf1;
  float:left;
}
.message-box, .res-message-box {
  margin-left: 65px;
  font-size: 1rem;
  -webkit-box-shadow: 0 2px 8px rgb(142 142 167 / 24%);
  box-shadow: 0 2px 8px rgb(142 142 167 / 24%);
  border-radius: 0 4px 4px 4px;
  max-width: 80%;
}
.res-message-box{
  background-color: rgba(229,233,251,.6);
  margin: 15px 0 0 65px;
}
.profile-img{
  margin:20px 0 0 11px;
}
.message-content{
  text-align: left;
  padding: 16px;
}
.right-aligined{
  display: flex;
  float:right
}
.video{
  object-fit: cover;
  max-height: 300px;
  max-width: 100%;
}
.sentence{
  display: flex;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  flex-direction: row;
  flex-wrap: nowrap;
  -webkit-box-align: center;
  align-items: center;
  -webkit-box-pack: center;
  justify-content: center;
  background-color: #edf0fd;
  border-radius: 4px;
  margin: 12px;
  padding: 10px;
  font-weight: 500;
  transition: background-color .3s ease-in;
}
</style>
