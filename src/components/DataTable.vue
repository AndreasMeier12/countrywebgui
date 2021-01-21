<template>
    <div id="data-table">
        <table>
            <tr id="data-pop">
                <th id="data-pop-left">Population</th>
                <th id="data-pop-right">{{country['population']}}</th>
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