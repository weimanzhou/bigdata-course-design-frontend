<template>
    <div id="app">
        <div id="container">
            <div id="left">
                <input type="button" autofocus value="查看男女比例" @click="manAndWoman">
                <input type="button" value="统计开有直播间的用户和未开直播间的用户" @click="liveMan">
                <input type="button" value="统计VIP用户比例" @click="vip">
                <input type="button" value="生日分布" @click="birthday">
                <input type="button" value="统计等级分布" @click="level">
            </div>
            <div id="right">
                <v-chart :options="polar1"/>
            </div>
        </div>
    </div>
</template>

<script>
    import 'echarts/lib/component/polar'

    export default {
        name: 'App',
        data() {
            return {
                polar1: {}
            }
        },
        created: function () {
            this.manAndWoman()
        },
        methods: {
            manAndWoman() {
                this.axios.get("http://localhost:8090/api/sex").then((response) => {
                    console.log(response.data)
                    let data = response.data
                    this.polar1 = {
                        title: {
                            text: 'bilibili用户性别比例',
                            left: 'center'
                        },
                        tooltip: {
                            trigger: 'item',
                            formatter: '{a} <br/>{b} : {c} ({d}%)'
                        },
                        legend: {
                            type: 'scroll',
                            orient: 'vertical',
                            right: 10,
                            top: 20,
                            bottom: 20,
                            data: data.legendData,
                            selected: {}
                        },
                        series: [
                            {
                                name: '姓名',
                                type: 'pie',
                                radius: '55%',
                                center: ['40%', '50%'],
                                data: data.seriesData,
                                emphasis: {
                                    itemStyle: {
                                        shadowBlur: 10,
                                        shadowOffsetX: 0,
                                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                                    }
                                }
                            }
                        ]
                    }

                })
            },
            liveMan() {
                this.axios.get("http://localhost:8090/api/live-room").then((response) => {
                    console.log(response.data)
                    let data = response.data
                    this.polar1 = {
                        title: {
                            text: 'bilibili用户开直播用户比例',
                            left: 'center'
                        },
                        tooltip: {
                            trigger: 'item',
                            formatter: '{a} <br/>{b} : {c} ({d}%)'
                        },
                        legend: {
                            type: 'scroll',
                            orient: 'vertical',
                            right: 10,
                            top: 20,
                            bottom: 20,
                            data: data.legendData,
                            selected: {}
                        },
                        series: [
                            {
                                name: '姓名',
                                type: 'pie',
                                radius: '55%',
                                center: ['40%', '50%'],
                                data: data.seriesData,
                                emphasis: {
                                    itemStyle: {
                                        shadowBlur: 10,
                                        shadowOffsetX: 0,
                                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                                    }
                                }
                            }
                        ]
                    }
                })
            },
            vip() {
                this.axios.get("http://localhost:8090/api/vip").then((response) => {
                    console.log(response.data)
                    let data = response.data
                    this.polar1 = {
                        title: {
                            text: 'bilibili用户VIP比例',
                            left: 'center'
                        },
                        tooltip: {
                            trigger: 'item',
                            formatter: '{a} <br/>{b} : {c} ({d}%)'
                        },
                        legend: {
                            type: 'scroll',
                            orient: 'vertical',
                            right: 10,
                            top: 20,
                            bottom: 20,
                            data: data.legendData,
                            selected: {}
                        },
                        series: [
                            {
                                name: '姓名',
                                type: 'pie',
                                radius: '55%',
                                center: ['40%', '50%'],
                                data: data.seriesData,
                                emphasis: {
                                    itemStyle: {
                                        shadowBlur: 10,
                                        shadowOffsetX: 0,
                                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                                    }
                                }
                            }
                        ]
                    }

                })
            },
            birthday() {
                this.axios.get("http://localhost:8090/api/birthday").then((response) => {
                    let data = response.data
                    this.polar1 = {
                        title: {
                            text: 'bilibili用户生日分布',
                            left: 'center'
                        },
                        tooltip: {
                            trigger: 'item',
                            formatter: '{b} : {c}人'
                        },
                        xAxis: {
                            type: 'category',
                            data: data['xs']
                        },
                        yAxis: {
                            type: 'value'
                        },
                        series: [{
                            data: data['ys'],
                            type: 'bar',
                            showBackground: true,
                            backgroundStyle: {
                                color: 'rgba(220, 220, 220, 0.8)'
                            }
                        }]
                    }
                })
            },
            level() {
                this.axios.get("http://localhost:8090/api/level").then((response) => {
                    let data = response.data
                    this.polar1 = {
                        title: {
                            text: 'bilibili用户等级分布',
                            left: 'center'
                        },
                        tooltip: {
                            trigger: 'item',
                            formatter: '{b} : {c}人'
                        },
                        xAxis: {
                            type: 'category',
                            data: data['xs']
                        },
                        yAxis: {
                            type: 'value'
                        },
                        series: [{
                            data: data['ys'],
                            type: 'bar',
                            showBackground: true,
                            backgroundStyle: {
                                color: 'rgba(220, 220, 220, 0.8)'
                            }
                        }]
                    }
                })
            }
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 100px;
    }

    .echarts {
        margin: 0 auto;
    }

    #container {
        width: 900px;
        height: 100%;

        margin: 0 auto;

        position: relative;
        top: 50%;
        /*transform: translateY(-50%);*/

        display: flex;
        flex-direction: row;
    }

    #left {
        width: 200px;
        background: darkgray;

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    #left input {
        width: 180px;
        margin-bottom: 20px;

        display: block;
        overflow: fragments;
    }

    #left input:focus {
        background: red;
    }

    #right {
        flex: 1;

        background: skyblue;
    }
</style>
