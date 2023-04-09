<template>
    <div class="container">
        <div class="card mb-3">
            <div class="card-header">Filter</div>
            <div class="card-body">
                <div class="row">
                    <div class="col-md-6">
                        <input type="text" placeholder="Fruit name" class="from-control" v-model="fruit_name">
                    </div>
                    <div class="col-md-6">
                        <select class="form-control" name="family" v-model="selected_family">
                            <option value="" selected disabled>Select Family</option>
                            <option v-for="row in family" :key="row">{{ row }}</option>
                        </select>
                    </div>
                </div>
            </div>
        </div>
        <div class="card " v-for="fruit in filtered_fruits" :key="fruit.id" style="background-color: white; margin-bottom: 20px;">
            {{ fruit.name }} ({{ fruit.family }})
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import _ from 'lodash'

export default {
  name: 'FruitsList',
  data () {
    return {
      fruits: [],
      selected_family: '',
      fruit_name: '',
    }
  },
  props: {
    msg: String,
  },
  computed: {

    filtered_fruits () {

      var family = this.selected_family
      var fruit_name = this.fruit_name
      var fruits = _.cloneDeep(this.fruits)

      if (family !== '') {
        fruits = fruits.filter(f => f.family === family)
      }

      if (fruit_name !== '') {
        fruits = fruits.filter(f => f.name.toLowerCase().includes(fruit_name.toLowerCase()))
      }

      return fruits
    },

    family () {
      var fruit_family = []
      this.fruits.forEach(function (value) {
        if (!fruit_family.includes(value.family)) {
          fruit_family.push(value.family)
        }
      })
      return fruit_family
    },
  },
  async mounted () {
    const response = await axios.get('/fruits.json')
    this.fruits = response.data
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}
</style>
