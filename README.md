## Usage

Install ApexCharts, and it globally

```js
// Vue3
import { createApp } from 'vue'
import App from './App.vue'
import VueApexCharts from "vue3-apexcharts";

const app = createApp(App);
app.use(VueApexCharts);
app.mount('#app');
```

Then use it inside your component

```vue
<script setup>
import { Status } from '@gramyhostujemy/vue-components';
</script>

<template>
  <div>
    <Status
      :server="{
        game: 'cstrike',
        name: 'DUST2 ONLY',
        ip: '127.0.0.1',
        port: 27015,
        mode: 'Counter-Strike',
        map: 'de_dust2',
        players_num: 1,
        players_max: 31,
        logs: [{
          data: [
            ['2022-11-06 18:48:00', 0],
            ['2022-11-06 18:49:00', 5],
            ['2022-11-06 18:50:00', 3],
            ['2022-11-06 18:51:00', 18],
            ['2022-11-06 18:52:00', 5],
            ['2022-11-06 18:53:00', 0],
            ['2022-11-06 19:04:00', 20], 
            ['2022-11-06 19:12:00', 12], 
            ['2022-11-06 19:22:00', 32], 
            ['2022-11-06 19:24:00', 1], 
            ['2022-11-06 19:32:00', 1], 
          ]
        }],
      }"
    />
  </div>
</template>
```
