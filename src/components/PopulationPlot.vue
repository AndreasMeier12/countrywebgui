<script>
    import {Bar} from 'vue-chartjs'


    export default {
        extends: Bar,
        name: "Plots",
        props: {
            country: null,
            allCountries: null,
            width: {
                value: '100vw',
            }
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
                                backgroundColor: '#2aa198',
                                data: [40, 20]
                            }
                        ]

                    }
                }

                const pops = this.allCountries.map(x => x['population']);
                const intervalSize = (Math.max(...pops) );
                var bins = [];
                var binLabels = [];
                for (var i = 0; i < nBins; i++) {
                    bins.push(0);
                    binLabels.push(String(intervalSize * Math.pow(0.5,i)));
                }
                for (var j = 0; j < pops.length; j++) {
                    const curBin = Math.floor(Math.log(intervalSize/pops[j])/Math.log(2));
                    bins[curBin] = bins[curBin] + 1;
                }

                const res = {
                    labels: binLabels,
                    datasets: [
                        {
                            label: 'Population',
                            backgroundColor: '#2aa198',
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
            this.chartdata = this.getPopData(30);
            console.log(this.chartdata);
            this.renderChart(this.chartdata, this.options)
        }

    }


</script>

<style scoped>
    @import "../assets/styles/shared.css";
    @import "../assets/styles/light.css";

</style>