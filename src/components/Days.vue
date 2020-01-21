<template >
    <div id="Day" >
        <div class="card">
            <h2 class="Name"><img class="picture" :src="period.icon" alt="Картинка погоды">{{period.name}}</h2>
            <h3>Temperature: {{period.temperature}} {{period.temperatureUnit}}</h3>
            <h3>{{period.detailedForecast}}</h3>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        period: {
            type: Object,
            required: true
        }
    }
}
</script>
<style>
    @import url('https://fonts.googleapis.com/css?family=Dancing+Script');
    .card {
        text-align: center;
        background: no-repeat;
    }
    #Day {
        background: url("https://cdn.pixabay.com/photo/2014/12/15/15/36/cloth-569222_960_720.jpg");
        width: 400px;
        height: 450px;
        display: -webkit-inline-flex;
        display: -ms-inline-flexbox;
        display: inline-flex;
        padding: 20px;
        margin: 15px;
        border-radius: 30px;
    }
    .picture {
        float: right;
        margin: 0 0 5px 5px;
    }
</style>