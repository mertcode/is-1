<template>
  <div id="app">

    <template v-if="!loading">
      <div class="container-fluid my-3">

        <div class="d-flex align-items-center justify-content-between">
          <h5>Guests</h5>
          <button type="button" 
            :class="['btn', advancedSearch ? 'btn-secondary' : 'btn-light']"
            @click="advancedSearch = !advancedSearch"
          >
            Advanced Search
          </button>
        </div>

        <form>

          <div class="form-row my-2">
            <component
              v-for="(filter, index) in defaultInputGroup" 
              :key="index"
              :is="filter.type"
              :data="filter"
              v-model="selections[filter.name]"
            >
            </component>
          </div> 

          <div class="form-row my-2" v-if="advancedSearch">
            <component
              v-for="(filter, index) in advancedInputGroup" 
              :key="index"
              :is="filter.type"
              :data="filter"
              v-model="selections[filter.name]"
            >
            </component>
          </div>

          <FormActions @clear="clear" @submit="submit"/>

          <div class="d-flex align-items-center justify-content-center mt-5" v-if="submitted">
            <pre>
              {{selections}}
            </pre>
          </div>

        </form>
    
      </div>
    </template>
  </div>

</template>

<script>

  import axios from 'axios'
  import FormActions from '@/components/FormActions'
  import Select from '@/components/Select'
  import TextBox from '@/components/TextBox'
  import Date from '@/components/Date'

  export default {
    name: "App",
    components: {
      FormActions,
      Select,
      TextBox,
      Date
    },
    data(){
      return {
        loading: false,
        advancedSearch: false,
        defaultInputGroup: [],
        advancedInputGroup: [],
        selections: {},
        submitted: false,
      }
    },
    methods: {

      getData(){
        return axios.get('http://localhost:8080/filters.json').then(res => {
          this.defaultInputGroup = [
            res.data[0], 
            res.data[1], 
            res.data[2], 
            res.data[3], 
            res.data[4]
          ].map(item => {
            return this.formatData(item)
          })

          this.advancedInputGroup = [
            res.data[5], 
            res.data[6], 
            res.data[7], 
            res.data[8],
            res.data[9],
          ].map(item => {
            return this.formatData(item)
          })
        })
      },
      formatData(array){
        let component = ''

        switch(array.type) {
          case 'select':
            component = 'Select'
            break;
          case 'text':
            component = 'TextBox'
            break;
          case 'date':
            component = 'Date'
            break;
          default:
            break;
        }

        return Object.assign({}, array, { type: component })
      },
      submit(){
        this.submitted = true

        // Burada bir API post işlemi gerçekleştirdiğimizi ve Vuex kullandığımızı düşünelim.
        // Örnek:
        // axios.post('${process.env.BASE_URL}/api/fakeApiEndPoint/...', this.selections).then(res => this.$store.dispatch('....', res.data....))

      },
      clear() {
        this.submitted = false 
      }
    },
    created(){

      this.loading = true

      this.getData().then(() => {
        this.loading = false
      })

    }
  }

</script>

