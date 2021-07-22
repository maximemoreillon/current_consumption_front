<template>
  <div class="instantaneous_view">
    <div class="meter">

      <template >
        <div
          class="phase"
          v-bind:style="{height: height(current_consumption.phase_1), backgroundColor: '#4286f4'}"
          v-if="current_consumption">
          {{current_consumption.phase_1}}A
        </div>
        <div
          class="phase"
          v-bind:style="{height: height(current_consumption.phase_2), backgroundColor: '#12ba77'}"
          v-if="current_consumption">
          {{current_consumption.phase_2}}A
        </div>
      </template>


    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {

  },
  data(){
    return {
      current_consumption: null,
      max_current: 30,
    }
  },
  methods: {
    height(phase){
      return  `${100 * phase/this.max_current}%`
    },

  },
  sockets: {
    connect() {
      this.$socket.client.emit('get_current_consumption', {});
    },
    current_consumption(message) {
      this.current_consumption = message
    }
  },
  mounted(){
    this.$socket.client.emit('get_current_consumption', {});
  }

}
</script>

<style scoped>

.instantaneous_view {
  
  height: 80vh;
  display: flex;
  align-items: stretch;
  justify-content: center;
}
.meter {

  padding: 2px;
  border: 2px solid #dddddd;
  width: 400px;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: flex-end;
}

.phase {
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  color: white;
  transition: height 0.25s;
}
</style>
