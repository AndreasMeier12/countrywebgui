<template>
    <div id="result-selection">
        <p>{{result.length}} result(s) <button v-on:click="toggleShowSelection" class="small-button">hide</button></p>
        <div v-if="showAll() && this.showSelection">
            <button v-if="result.length > 3" v-on:click="toggleShowMore" class="button-less">-</button>
            <button v-for="country in result" v-on:click="selectCountry(country['name'])" :key="country['name']"><img
                    :src="country['flag']" class="button-flag" :alt="country['name']"/> {{shortenName(country['name'])}}
            </button>
        </div>
        <div v-if="!showAll() && this.showSelection">
            <button v-for="country in result.slice(0,3)" v-on:click="selectCountry(country['name'])"
                    :key="country['name']"><img :src="country['flag']" class="button-flag" :alt="country['name']"/>
                {{shortenName(country['name'])}}
            </button>
            <button v-for="country in result.slice(3,4)" v-on:click="toggleShowMore" :key="country['name']"><img
                    :src="country['flag']"
                    class="grey-image" alt="more"/> ...
            </button>
        </div>
    </div>


</template>

<script>
    export default {
        name: "ResultSelection",
        props: {
            result: Array,


        },
        methods: {
            selectCountry(country) {
                this.$emit("select:country", country)
            },
            showAll() {
                return this.showMore || this.result.length <= 3;
            },
            toggleShowMore() {
                this.showMore = !this.showMore;
            },
            toggleShowSelection() {
                this.showSelection = !this.showSelection;
            },
            shortenName(a){
                if (a.length > 10){
                    return a.slice(0,8) + '...';
                }
                return a;

            }
        },
        data() {
            return {
                showMore: false,
                showSelection: true,
            }
        }
    }
</script>

<style scoped>
    .button-flag {
        width: 50px;
        height: auto;
    }

    .button-flag-more {
        width: 50px;
        height: auto;
        background-color: gray;
        opacity: .2;

    }

    .grey-image {
        width: 50px;
        height: auto;
        background-color: gray;
        opacity: .2;

    }

</style>