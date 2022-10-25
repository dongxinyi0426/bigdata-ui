<template>
    <div class="address">
        Address:  {{data.userId}}
    </div>
    <div class="carparkno">
        Car Park No:  {{data.predictionCost}}
    </div>
    <div class="lots">
        Current Lots Available: {{data.Current_Lots_Available}}
    </div>
     <div class="prediction">
        Prediction:
    </div>
    <div class="prediction-item" v-for="(item, index) in data.PredictionPointList" :key="index">
        Time: {{item.Time}}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
        Predict Available Lots: {{item.Value}}
    </div>
    <div class="distance">
        Distance:  {{data.Distance}}&nbsp;meters
    </div>

</template>

<script>
export default {
    data() {
        return {
            center: { lat: Number(this.data.Latitude), lng: Number(this.data.Longitude) }
        };
    },
    props: ['data', 'index'],
    methods: {
        genMap(){
            loader.load().then(() => {
                const map = new google.maps.Map(document.getElementById(`map-${this.index}`), {
                    center: this.center,
                    zoom: 16,
                });
                const myLatLng = this.center;
                new google.maps.Marker({
                    position: myLatLng,
                    map,
                    title: "Let's go!",
                });
            });
        }
    },
    mounted() {
        this.genMap();
    },
    updated() {
        this.genMap();
    }
}
</script>

<style>
    .map {
        height: 600px;
    }
    .address {
    color: #21bea0;
    background-color: #f4f9f7;
    height: 60px;
    padding-left: 20px;
    }
    .carparkno {
    color: #21bea0;
    background-color: #f4f9f7;
    height: 60px;
    padding-left: 20px;
    }
    .prediction {
    color: #21bea0;
    background-color: #f4f9f7;
    height: 40px;
    padding-left: 20px;
    }
    .prediction-item {
    color: #1281db;
    background-color: #f4f9f7;
    padding-left: 60px;
    }
    .lots {
    color: #21bea0;
    background-color: #f4f9f7;
    height: 60px;
    padding-left: 20px;
    }
    .distance {
    color: #21bea0;
    background-color: #f4f9f7;
    height: 60px;
    padding-left: 20px;
    }
</style>