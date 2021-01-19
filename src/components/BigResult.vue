<template>
    <div id="big-result">
    <h1>{{country['name']}}</h1>
    </div>
</template>

<script>
    var country;
    export default {
        props: {
            country
        }
    }

</script>

<style scoped>

</style>