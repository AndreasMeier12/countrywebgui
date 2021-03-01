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
                    maintainAspectRatio: false,
                    scales: {
                        xAxes: [{
                            display: true,
                            scaleLabel: {
                                display: true,
                                labelString: "Upper bound of population"
                            }
                        }
                        ],
                        yAxes: [ {
                            display: true,
                            scaleLabel: {
                                display: true,
                                labelString: 'count'
                            }
                        } ],
                    }
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
                    const binSize = intervalSize * Math.pow(0.5,i);
                    if (binSize >= 1){
                    bins.push(0);
                        binLabels.push(String(this.formatNumber(Math.floor(intervalSize * Math.pow(0.5,i)))));
                    }
                }
                binLabels = binLabels.reverse();
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

            formatNumber(a){
                return a.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");

            }
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