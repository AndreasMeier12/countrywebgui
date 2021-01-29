<script>
    import {Bar} from 'vue-chartjs'


    export default {
        extends: Bar,
        name: "AreaPlot",
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
                                backgroundColor: '#2aa198',
                                data: [40, 20]
                            }
                        ]

                    }
                }

                const areas = this.allCountries.map(x => x['area']);
                const intervalSize = (Math.max(...areas) );
                var bins = [];
                var binLabels = [];
                for (var i = 0; i < nBins; i++) {
                    const binSize = intervalSize * Math.pow(0.5,i);
                    if (binSize >= 1){
                        bins.push(0);
                        binLabels.push(String(intervalSize * Math.pow(0.5,i)));
                    }
                }
                for (var j = 0; j < areas.length; j++) {
                    const curBin = Math.floor(Math.log(intervalSize/areas[j])/Math.log(2));
                    bins[curBin] = bins[curBin] + 1;
                }

                const res = {
                    labels: binLabels,
                    datasets: [
                        {
                            label: 'Area',
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