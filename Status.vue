<script setup>
const gameImage = new URL(`./assets/Query/cstrike.png`, import.meta.url);
const mapImage = new URL(`./assets/Query/cstrike/de_dust2.png`, import.meta.url);
</script>

<template>
    <div class="servers">
        <div class="info">
            <div style="display: flex; width: 10%;">
                <img
                    width="25"
                    height="25"
                    :src="gameImage"
                />
            </div>
            <div style="width: 10%;display: flex;justify-content: center;">
                <div class="icon" @click="copyURL(`${server.ip}:${server.port}`)">
                    <svg xmlns="http://www.w3.org/2000/svg" 
                        height="24px" 
                        viewBox="0 0 24 24" 
                        width="24px"
                        fill="#cefff6"
                    >
                        <path d="M0 0h24v24H0V0z" fill="none" />
                        <path d="M8 7h11v14H8z" opacity=".3" />
                        <path d="M16 1H4c-1.1 0-2 .9-2 2v14h2V3h12V1zm3 4H8c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h11c1.1 0 2-.9 2-2V7c0-1.1-.9-2-2-2zm0 16H8V7h11v14z"/>
                    </svg>
                </div>
            </div>
            <div style="width: 30%">
                <div class="mid" style="text-transform: uppercase">{{ server.name }}</div>
                <div class="smaller" style="text-transform: uppercase">{{ server.mode }}</div>
            </div>
            <div style="width: 20%; text-align: left">
                <div class="mid">{{ server.map }}</div>
            </div>
            <div style="width: 20%; text-align: center;">
                <div class="mid">{{ server.players_num }} / {{ server.players_max }}</div>
            </div>
            <div style="width: 50px; height: 50px">
                <apexchart
                    type="radialBar"
                    width="50px"
                    height="50px"
                    :options="{
                        chart: {
                            height: 30,
                            type: 'radialBar',
                            sparkline: {
                                enabled: true
                            },
                        },
                        plotOptions: {
                            radialBar: {
                                dataLabels: {
                                    show: false,
                                },
                                track: {
                                    background: '#41ffc3',
                                    opacity: 0.2,
                                },
                                startAngle: -135,
                                endAngle: 135,
                                hollow: {
                                    size: '30%',
                                },
                            },
                        },
                        colors: ['#41ffc3'],
                    }"
                    :series="[Math.floor((server.players_num / server.players_max) * 100)]"
                ></apexchart>
            </div>
        </div>
        <div class="background" :style="{backgroundImage: 'url(' + mapImage + ')'}"></div>
        <div class="chart">
            <apexchart
                type="area"
                width="480px"
                height="69px"
                :options="{
                    stroke: {
                        curve: 'stepline',
                        colors: ['#41ffc34f'],
                        width: [1]
                    },
                    chart: {
                        animations: {
                            enabled: true,
                            easing: 'easeinout',
                            speed: 999,
                            animateGradually: {
                                enabled: true,
                                delay: 150
                            },
                            dynamicAnimation: {
                                enabled: true,
                                speed: 350
                            },
                        },
                        type: 'area',
                        zoom: {
                            enabled: false,
                        },
                        sparkline: {
                            enabled: true
                        },
                        toolbar: {
                            show: false,
                        },
                    },
                    grid: {
                        show: false,
                        row: {
                            opacity: 0.1,
                        },
                        padding: {
                            left: 0,
                            right: 0
                        },
                    },
                    dataLabels: {
                        enabled: false,
                    },
                    fill: {
                        type: 'gradient',
                        gradient: {
                            colorStops: [ 
                                [
                                    {
                                        offset: 0.6,
                                        color: '#41ffc3',
                                        opacity: 0.4
                                    },
                                    {
                                        offset: 100,
                                        color: '#41ffc3',
                                        opacity: 0
                                    }
                                ],
                            ],
                        },
                    },
                    xaxis: {
                        show: false,
                        seriesName: 'time',
                        type: 'datetime',
                        labels: {
                            formatter: () => '',
                        },
                        axisBorder: {
                            show: false,
                        },
                        axisTicks: {
                            show: false,
                        },
                    },
                    yaxis: {
                        show: false,
                        seriesName: 'players',
                        min: 0,
                        max: server.players_max,
                    },
                    tooltip: {
                        enabled: false,
                    },
                }"
                :series="server.logs"
            ></apexchart>
        </div>
    </div>
</template>

<script>
export default {
    name: "Status",
    props: {
        server: {
            type: Object,
            default: () => {},
        },
    },
    methods: {
        async copyURL(mytext) {
            await navigator.clipboard.writeText(mytext);
        }
    },
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@200;300;400;500;600;700&display=swap');

.servers {
    color: white;
    margin: 0 auto;
    width: 500px;
    background-color: #3b3b3b;
    font-size: 16px;
    color: #cefff6;
    margin-bottom: 10px;
    position: relative;
    font-family: 'Oswald', sans-serif;
    font-weight: 300;
    letter-spacing: 1.5px;
}

.servers .smaller {
    font-size: 10px;
    letter-spacing: 1.5px;
}

.servers .mid {
    font-size: 14px;
    letter-spacing: 1.5px;
}

.servers .icon {
    width: 35px;
    height: 35px;
    padding: 0px;
    box-sizing: border-box;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 5px;
    cursor: pointer;
}

.servers .info {
    padding: 20px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 1px solid #0d2a57ad;
    position: relative;
    z-index: 999999;
}

.servers .background {
    background-size: cover;
    background-position: center;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    box-sizing: border-box;
    opacity: 0.5;
}

.servers .chart {
    position: absolute;
    top: 10px;
    left: 10px;
    right: 10px;
    bottom: 10px;
    box-sizing: border-box;
    opacity: 0.5;
}

.servers .chart .apexcharts-canvas {
    width: 100% !important;
    height: 100% !important;
}
.servers .chart svg {
    width: 100% !important;
    height: 100% !important;
}
</style>
