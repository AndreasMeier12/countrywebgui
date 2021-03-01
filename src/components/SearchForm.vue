<template>
    <div id="search-field">
        <form id="search-form" @submit.prevent="search">
            <label>Search for country
                <input v-model="searchName" type="text" id="search-form-input" placeholder="antigua:" />
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
            search() {
                console.log("Sorch name: " + this.searchName);
                    const data = this.allCountries.filter(x => x['name'].toLowerCase().includes(this.searchName.toLocaleLowerCase()));
                    this.$emit('search:country', data)
            }
        },
        props: {
            allCountries: Array,
        }
    }
</script>

<style scoped>

</style>