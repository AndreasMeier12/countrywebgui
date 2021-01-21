<template>
    <div id="data-table">
        <table>
            <tr id="data-pop">
                <th id="data-pop-left">Population</th>
                <th id="data-pop-right">{{country['population']}}</th>
            </tr>

            <tr id="data-continent">
                <th id="data-continent-left">Region</th>
                <th id="data-continent-right">{{country['region']}}</th>
            </tr>



        </table>

    </div>
</template>

<script>
    var country;
    export default {

        name: "data-table",
        props: {
            country
        },
    }
</script>

<style scoped>

</style>