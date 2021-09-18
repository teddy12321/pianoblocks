<template>
    <div id="app1">
        <rect-am :data="data" />
    </div>
</template>

<script>
// import ResponsiveLineChart from "./components/ResponsiveLineChart.vue";
import RectAm from './components/Rect.vue';

export default {
    name: 'App',
    components: {
        // ResponsiveLineChart,
        RectAm,
    },
    data() {
        return {
            data: [10, 40, 15, 25, 50],
        };
    },
    methods: {
        addData() {
            // add random value from 0 to 50 to array
            this.data = [...this.data, Math.round(Math.random() * 50)];
        },
        filterData() {
            this.data = this.data.filter((v) => v <= 35);
        },
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    max-width: 1020px;
    margin: 100px auto;
    padding: 0 20px;
}

#app1 {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    max-width: 800px;
    margin: 100px auto;
    padding: 0 20px;
}

#head {
    z-index: 10;
    background: gold;
}

svg {
    /* important for responsiveness */
    display: block;
    fill: none;
    stroke: none;
    width: 100%;
    height: 140%;
    overflow: visible;
    background: #eee;
    z-index: 1;
}

.buttons {
    margin-top: 2rem;
}
</style>
