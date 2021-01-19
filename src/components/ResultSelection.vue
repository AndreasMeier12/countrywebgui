<template>
    <div id="result-selection">
        <p>{{result.length}} result(s)</p>
        <div v-if="result.length<=3">        <button v-for="country in result" :key="country['name']"><img :src="country['flag']" class="button-flag" :alt="country['name']"/> {{country['name']}}</button>
        </div>
        <div v-if="result.length>3">        <button v-for="country in result.slice(0,3)" :key="country['name']"><img :src="country['flag']" class="button-flag" :alt="country['name']"/> {{country['name']}}</button>
            <button v-for="country in result.slice(3,4)" :key="country['name']"><img :src="country['flag']" class="button-flag-more" alt="more"/> ...</button>
        </div>
    </div>

    
</template>

<script>
    export default {
        name: "ResultSelection",
        props: {
            result: Array,

        }
    }
</script>

<style scoped>
    .button-flag{
        width: 50px;
        height: auto;
    }

    .button-flag-more{
        width: 50px;
        height: auto;
        filter: alpha(opacity=40);
        background-color: #000;

    }

</style>