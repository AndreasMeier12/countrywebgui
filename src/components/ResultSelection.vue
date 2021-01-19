<template>
    <div id="result-selection">
        <p>{{result.length}} result(s)</p>
        <button  v-for="country in result" :key="country['name']"><img :src="country['flag']" class="button-flag" :alt="country['name']"/> {{country['name']}}</button>
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

</style>