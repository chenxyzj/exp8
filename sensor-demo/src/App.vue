<!--
 * @Author: chenxyzj 26920259+chenxyzj@users.noreply.github.com
 * @Date: 2022-11-16 04:22:54
 * @LastEditors: chenxyzj 26920259+chenxyzj@users.noreply.github.com
 * @LastEditTime: 2022-11-19 06:37:36
 * @FilePath: /exp8/sensor-demo/src/App.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->

<script>
import axios from 'axios'
export default {
  data() {
    return {
      sensorId: 1,
      sensorData: null
    }
  },
  methods: {
    async fetchData() {
      try{

        const res = await axios(
          `https://chenxyzj-didactic-fiesta-4qr77gjj64gf7v4x-8000.preview.app.github.dev/api/sensors/${this.sensorId}/`,{
            method:"GET",
          }
          )
          console.log(res);
          this.sensorData = res.data
        }catch(e) {
          this.sensorData = e.message
        }
    }
  },
  mounted() {
    this.fetchData()
  },
  watch: {
    sensorId() {
      this.fetchData()
    }
  }
}
</script>

<template>
  <p>sensor id: {{ sensorId }}</p>
  <button @click="sensorId++">Fetch next sensor</button>
  <p v-if="!sensorData">Loading...</p>
  <pre v-else>{{ sensorData }}</pre>
</template>