<script>
    import {Bar} from 'vue-chartjs'


    export default {
        extends: Bar,
        name: "Plots",
        props: {
            country: null,
            allCountries: null,
        },
        data() {
            return {
                chartdata: null,
                options: {
                    responsive: true,
                    maintainAspectRatio: false
                }
            }
        },
        methods: {
            getPopData(nBins) {
                if (this.country === null || this.allCountries === null) {
                    return {
                        labels: ['January', 'February'],
                        datasets: [
                            {
                                label: 'Data One',
                                backgroundColor: '#f87979',
                                data: [40, 20]
                            }
                        ]

                    }
                }

                const pops = this.allCountries.map(x => x['population']).sort();
                console.log(pops.length);
                const intervalSize = (Math.max(...pops) - Math.min(...pops)) / nBins;
                console.log("Interval size" + intervalSize);
                var bins = [];
                var binLabels = [];
                for (var i = 0; i < nBins; i++) {
                    bins.push(0);
                    binLabels.push(String(intervalSize * i));
                }
                for (var j = 0; j < pops.length; j++) {
                    const curBin = Math.floor(pops[j] / intervalSize);
                    console.log("bin" +curBin);
                    bins[curBin] = bins[curBin] + 1;
                }
                const res = {
                    labels: binLabels,
                    datasets: [
                        {
                            label: 'Population',
                            backgroundColor: '#f87979',
                            data: bins
                        }
                    ]
                };
                console.log(res);
                return res;

            },


            getAreaData() {
            },
        },

        mounted() {
            this.chartdata = this.getPopData(20);
            console.log(this.chartdata);
            this.renderChart(this.chartdata, this.options)
        }

    }


</script>

<style scoped>

</style>