<template>
  <div class="home">
    <div v-if="dataCollection.loaded">

      <LineChart
        v-if="dataCollection.loaded"
        v-bind:data="dataCollection"/>

    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import LineChart from '@/components/charts/LineChart.vue'

export default {
  name: 'Home',
  components: {
    LineChart
  },
  data(){
    return {
      dataCollection: {
        loaded: false,
        labels: [], // filled by API call

        datasets: [
          {
            label: 'Phase 1',
            data: [], // filled by API call
            borderColor: '#4286f4',
            fill: false,
            pointRadius: 0,
            pointHitRadius: 3,
            pointHoverRadius: 3,
            borderWidth: 2,
          },
          {
            label: 'Phase 2',
            data: [], // filled by API call
            borderColor: '#12ba77',
            fill: false,
            pointRadius: 0,
            pointHitRadius: 3,
            pointHoverRadius: 3,
            borderWidth: 2,
          },
          {
            label: 'Total',
            data: [], // filled by API call
            borderColor: '#c00000',
            fill: false,
            pointRadius: 0,
            pointHitRadius: 3,
            pointHoverRadius: 3,
            borderWidth: 2,
          },
        ],
      }
    }
  },
  mounted(){
    this.dataCollection.loaded = false;
    this.axios.get(`${process.env.VUE_APP_API_URL}/data`)
    .then(response => {
      //console.log(response.data[0])
      // Empty array
        this.dataCollection.labels.splice(0,this.dataCollection.labels.length)
        this.dataCollection.datasets[0].data.splice(0,this.dataCollection.datasets[0].data.length)
        this.dataCollection.datasets[0].data.splice(0,this.dataCollection.datasets[1].data.length)
        this.dataCollection.datasets[2].data.splice(0,this.dataCollection.datasets[1].data.length)
        // repopulate
        response.data.forEach(entry => {
          this.dataCollection.datasets[0].data.push(Number(entry.phase_1))
          this.dataCollection.datasets[1].data.push(Number(entry.phase_2))
          this.dataCollection.datasets[2].data.push(Number(entry.total))
          this.dataCollection.labels.push(new Date(entry.time))
        })

        this.dataCollection.loaded = true;

    })
    .catch(error => {console.log(error)})
  }
}
</script>
