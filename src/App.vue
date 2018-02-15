<template>

  <div id="app">
    <div class="jumbotron">
    <div class="container">
      <header>
        <span>BriteCore</span>
      </header>
        <div class="container">
          <RiskTypeSelection v-on:riskTypeChanged="riskTypeChanged"></RiskTypeSelection>
          <RiskTypeList v-bind:source="source"></RiskTypeList>
        </div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import RiskTypeList from './components/RiskTypeList'
import RiskTypeSelection from './components/RiskTypeSelection'

export default {
  name: 'app',
  components: {
    RiskTypeSelection,
    RiskTypeList
  },
  data () {
    return {
      source: ''
    }
  },
  methods: {
    riskTypeChanged: function (source) {
      this.source = source
    }
  }
}
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

main {
  text-align: center;
  margin-top: 40px;
}

header {
  margin: 0;
  height: 56px;
  padding: 0 16px 0 24px;
  background-color: #35495E;
  color: #ffffff;
}

header span {
  display: block;
  position: relative;
  font-size: 20px;
  line-height: 1;
  letter-spacing: .02em;
  font-weight: 400;
  box-sizing: border-box;
  padding-top: 16px;
}
</style>
