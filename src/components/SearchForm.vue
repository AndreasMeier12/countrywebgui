<template>
    <div id="search-field">
        <form id="search-form" @submit.prevent="search">
            <label>Search
                <input v-model="searchName" type="text"/>
            </label>
            <button class="small-button">Go!</button>
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
                    const response = await fetch(url)
                    const data = await response.json()
                    this.$emit('search:country', data)
                } catch (e) {
                    console.log(e)
                }
            }
        },
    }
</script>

<style scoped>

</style>