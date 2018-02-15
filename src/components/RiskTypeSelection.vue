<template>
    <div class="view overlay">
      <h1>BriteCore</h1>
      <h2>Select Risk Type </h2>
      <select class="form-control" v-on:change="riskTypeChanged">
        <option value="0">Select</option>
        <option v-bind:value="item.id" v-for="item in items">{{item.name}}</option>
      </select>
    </div>
</template>
<script>

export default {
  name: 'risktypeselection',
  data () {
    return {
      items: [],
      source: ''
    }
  },
  methods: {
    riskTypeChanged: function (e) {
      for (var i = 0; i < this.items.length; i++) {
        if (this.items[i].id === e.target.value) {
          this.source = this.items[i]
        }
      }
      this.$emit('riskTypeChanged', e.target.value)
    }
  },
  created: function () {
    this.$http.get('api/risktypes/')
      .then(response => {
        this.items = response.data
      }).catch(error => {
        console.log(error)
      })
  }
}
</script>
<style scoped>
</style>
