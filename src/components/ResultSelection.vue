<template>
    <div id="result-selection">
        <p>{{result.length}} result(s)</p>
        <div v-if="result.length<=3">        <button v-for="country in result" v-on:click="selectCountry(country['name'])" :key="country['name']"><img :src="country['flag']" class="button-flag" :alt="country['name']"/> {{country['name']}}</button>
        </div>
        <div v-if="result.length>3">        <button v-for="country in result.slice(0,3)" v-on:click="selectCountry(country['name'])" :key="country['name']"><img :src="country['flag']" class="button-flag" :alt="country['name']"/> {{country['name']}}</button>
            <button v-for="country in result.slice(3,4)" :key="country['name']"><img :src="country['flag']" class="grey-image" alt="more"/> ...</button>
        </div>
    </div>

    
</template>

<script>
    export default {
        name: "ResultSelection",
        props: {
            result: Array,

        },
        methods :{
            selectCountry(country){
                this.$emit("select:country", country)
            }
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
        background-color: gray;
        opacity: .2;

    }

    .grey-image{
        width: 50px;
        height: auto;
        background-color: gray;
        opacity: .2;

    }

</style>