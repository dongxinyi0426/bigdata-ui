<script>
import axios from 'axios';
import ListItem from './ListItem.vue';

export default {
    data() {
        return {
            formvalue: {},
            list: [],
            predictionCost: [],
            userId: '',
            bol: false,
            content: '',
        };
    },
    methods: {
        clear() {
            this.formvalue = {};
            this.list = [];
        },
        async search() {
            // 请求接口
            const params = this.formvalue;
            const res = await axios.post("http://54.179.112.4:8081/getRecommendationList", params);
            console.log("!!!!!!!!")
            this.userId = res.data.userId;
            console.log("userID ++  " + this.userId)
            this.list = res.data.data[0];
            this.pic = "./assets/dashboard.png";
            console.log(this.list)
        }
    },
    components: { ListItem }
}
</script>

<template>
  <div class="wrapper">

      <div class="header">
        <div class="logo">
          <img src="./assets/logo_new1.jpg" alt="">
        </div>
        <div class="title">
          <h1>Smart Recommendation System</h1>
        </div>
      </div>

      <el-card shadow="always" class="card">
        <el-form
          ref="form"
          :model="formvalue"
          label-width="auto"
          size="large"
        >
          <el-form-item class="form-item" label="Check my pediction cost">
            <el-input class="form-field"   v-model="formvalue.userId" />
          </el-form-item>
          
        </el-form>

        <div class="controls">
          <el-button type="primary" color="#574cc9" size="large" @click="clear">Clear</el-button>
          <el-button type="primary" color="#574cc9" size="large" @click="search">Check</el-button>
        </div>
        
      </el-card>
<!--    <div class="content-result">-->
<!--    <el-collapse class="list">-->
<!--      <el-collapse-item   :title="`Prediction Cost: ${this.list.predictionCost}  `">-->
<!--      </el-collapse-item>-->
<!--      <el-collapse-item   :title="`Cost Max: ${this.list.costMax}  `">-->
<!--      </el-collapse-item>-->
<!--      <el-collapse-item   :title="`Cost Min: ${this.list.costMin}  `">-->
<!--      </el-collapse-item>-->
<!--    </el-collapse>-->
<!--    </div>-->
    <el-card v-show="true ? this.list.predictionCost !=null : this.list.predictionCost ==null" class="card" style="height:300px; padding:30px">
      <el-form
      label-width="auto"
                size="medium"
      >
                <el-form-item style="height:30px" class="form-item" label="Prediction Cost">
                  <el-input class="paperview-input-text" style="background-color: #faf9fc"  v-model="this.list.predictionCost" :readonly="true"></el-input>

                </el-form-item>

                <el-form-item style="height:30px" class="form-item" label="Max Cost">
                   <el-input class="paperview-input-text"   v-model="this.list.costMax" :readonly="true"></el-input>
                </el-form-item>

                <el-form-item style="height:30px" class="form-item" label="Min  Cost">
                    <el-input class="paperview-input-text"   v-model="this.list.costMin" :readonly="true"></el-input>
                </el-form-item>

              </el-form>


    </el-card>
<!--    <el-card class="list">-->
<!--      <div>-->
<!--        <img :src="this.pic" >-->
<!--      </div>-->
<!--    </el-card>-->
  </div>
</template>

<style>
@import './assets/base.css';

.header {
  display: flex;
  justify-content: center;
}

.header .logo img {
  margin: 50px;
  width: 260px;
  height: 100px;
}

.list img{
  width: 640px;
  height: 400px;
}

h1 {
  margin: 50px;
  font-weight: 900;
  font-size: 60px;
  margin-left: 5px;
}

.card {
  display: flex;
  justify-content: center;
  margin-top:30px;
  padding: 50px;
  background-color: #faf9fc;
  border-radius: 10px;
  height: 300px;
}

.card .el-form-item__label {
  color: #574cc9;
  font-weight: bold;
  font-size: 30px;
}

.card .form-field {
  width: 500px;
  background-color: #faf9fc;
}

.wrapper {
  padding: 20px;
}

.form-item {
  margin-bottom: 50px;
}

.form-item input, .form-item select {
  height: 40px !important;
  font-size: 20px;
}

.label {
  margin-right: 5px;
  width: 150px;
  text-align: right;
}

.controls {
  margin-top: 20px;
  margin-left: 285px;
}

.controls button {
  margin-right: 50px;
  color: #fff;
  width: 150px;
  height: 50px;
  font-size: 24px;
}
.content-result{
  display: flex;
  justify-content: center;
}
.list {
  display: flex;
  justify-content: center;
  margin-top: 20px;
  margin-left: 10px;
  width: calc(100% - 16px);
  font-size: 28px;
  color: #574cc9;
  background-color:#f5f3f9;
  font-weight: bolder;
  border-radius: 10px;
}
.paperview-input-text .el-input__inner {
    background-color: #faf9fc;
   -webkit-appearance: none;
    background-color: #faf9fc;
    background-image: none;
    border-radius: 4px;
    border: none;

}

</style>
