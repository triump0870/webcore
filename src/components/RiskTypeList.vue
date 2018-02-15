<template>
  <div class="risktype">
    <div class="container">
      <section class="form">
        <h2 v-if="form_name">{{form_name}} Risk Form</h2>
        <form method="post" @submit.prevent="postData">
          <div class="field" v-for="(item,val) in getFormData">
              <label>{{val}}</label>
              <div class="control">
                <input v-model="val" :id="val" class="input" :type="item.type">
              </div>
          </div>
          <div class="text-center">
            <button v-if="form_name" class="btn btn-default">Submit</button>
          </div>
        </form>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'risktypelist',
  props: ['source'],
  data () {
    return {
      items: [],
      form_name: '',
      form: {}
    }
  },
  methods: {
    updateRiskType: function (source) {
      if (source !== '0' || source === undefined) {
        console.log('called')
        this.$http.get('api/risktypes/' + source)
          .then(response => {
            this.items = response.data.risk_field_list
            this.form_name = response.data.name
            console.log('Items: ', this.items)
          }).catch(error => {
            console.log(error)
          })
      }
    },
    postData: function () {
      console.log('Data was posted')
    }
  },
  watch: {
    source: function (val) {
      this.updateRiskType(val)
    }
  },
  computed: {
    getFormData () {
      console.log('Length: ' + this.items)
      if (this.items > 0 || this.items !== undefined) {
        this.form = {}
        for (var i = 0; i < this.items.length; i++) {
          this.form[this.items[i].name] = this.items[i]
        }
        console.log('Form: ', this.form)
        return this.form
      }
    }
  }
}
</script>
<style scoped>
.item {
  padding: 10px;
}
</style>
