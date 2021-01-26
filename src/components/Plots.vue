
<script>
    import { Bar } from 'vue-chartjs'
    var country;
    var allCountries;
    export default {
        extends: Bar,
        name: "Plots",
        props: {
            country,
            allCountries
        },
        data() {
            return {
                chartOptionsBar: {
                    xAxis: {
                        data: ['Q1', 'Q2', 'Q3', 'Q4']
                    },
                    yAxis: {
                        type: 'value',
                    },
                    series: [
                        {
                            type: 'bar',
                            data: [63, 75, 24, 92]
                        }
                    ]

                },
                chartdata: {
                    labels: ['January', 'February'],
                    datasets: [
                        {
                            label: 'Data One',
                            backgroundColor: '#f87979',
                            data: [40, 20]
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false
                }
            }
        },
        methods: {
            getPopData(nBins) {
                if(this.country === null || this.allCountries === null){
                    return {
                        xAxis: {
                            data: ['Q1', 'Q2', 'Q3', 'Q4']
                        },
                        yAxis: {
                            type: 'value',
                        },
                        series: [
                            {
                                type: 'bar',
                                data: [63, 75, 24, 92]
                            }
                        ]
                    }
                }

                const sorted = this.allCountries.map(x => x['population']);
                const intervalSize = (sorted[sorted.length-1] - sorted[0]) / nBins;
                var bins = [];
                var binLabels = [];
                for(var i =0; i < nBins; i++){
                    bins.push(0);
                    binLabels.push(String(intervalSize * i));
                }
                for (i =0; i < sorted.length; i++){
                    const curBin = Math.floor(sorted[i]/nBins);
                    bins[curBin] = bins[curBin] + 1;
                }

                return {
                    xAxis: {
                        data: binLabels
                    },
                    yAxis: {
                        type: 'value',
                    },
                    series: [
                        {
                            type: 'bar',
                            data: bins
                        }
                    ]
                }
            },

            getAreaData() {
            },
        },

        mounted () {
            this.renderChart(this.chartdata, this.options)
        }

    }


</script>

<style scoped>

</style>