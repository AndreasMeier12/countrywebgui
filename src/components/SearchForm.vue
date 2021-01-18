<template>
    <div id="search-field">
        <form id="search-form" @submit.prevent="search">
            <label>Search
                <input v-model="searchName" type="text"/>
            </label>
            <button>Go!</button>
        </form>

    </div>
</template>

<script>
    export default {
        name: "SearchForm",
        data() {
            return {
                searchName: '',
            }
        },
        methods: {
            async search() {
                console.log("Sorch name: " + this.searchName);
                try {
                    const url = 'https://restcountries.eu/rest/v2/name/' + this.searchName;
                    const data = await fetch(url);
                    console.log(data.json())
                } catch (e) {
                    console.log(e)
                }



            }

        },
    }
</script>

<style scoped>

</style>