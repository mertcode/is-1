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
            <SelectBox v-model="userSelections.location" :data="inputs.location"/>
            <TextBox v-model="userSelections.name" :data="inputs.name"/>
            <TextBox v-model="userSelections.email" :data="inputs.email"/>
            <TextBox v-model="userSelections.phone" :data="inputs.phone"/>
            <SelectBox v-model="userSelections.nationality" :data="inputs.nationality"/>
          </div> 
          <div class="form-row my-2" v-if="advancedSearch">
            <TextBox v-model="userSelections.passportNumber" :data="inputs.passportNumber"/>
            <SelectBox v-model="userSelections.gender" :data="inputs.gender"/>
            <TextBox v-model="userSelections.mac" :data="inputs.mac"/>
            <SelectBox v-model="userSelections.connectionStatus" :data="inputs.connectionStatus"/>
            <TextBox v-model="userSelections.date" :data="inputs.date"/>
          </div>

          <div class="d-flex align-items-center justify-content-end mt-4">
            <button type="button" class="btn btn-light d-flex align-items-center justify-content-center" @click="clear">
              <svg width="1.5em" height="1.5em" viewBox="0 0 16 16" class="bi bi-x mr-1" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
              </svg>
              Clear
            </button>

            <button type="button" class="btn btn-light ml-2 d-flex align-items-center justify-content-center" @click="submit">
              <svg width="1em" height="1em" viewBox="0 0 16 16" class="bi bi-search mr-2" fill="currentColor" xmlns="http://www.w3.org/2000/svg">
                <path fill-rule="evenodd" d="M10.442 10.442a1 1 0 0 1 1.415 0l3.85 3.85a1 1 0 0 1-1.414 1.415l-3.85-3.85a1 1 0 0 1 0-1.415z"/>
                <path fill-rule="evenodd" d="M6.5 12a5.5 5.5 0 1 0 0-11 5.5 5.5 0 0 0 0 11zM13 6.5a6.5 6.5 0 1 1-13 0 6.5 6.5 0 0 1 13 0z"/>
              </svg>
              Search
            </button>
          </div>

        </form>

        <div class="d-flex align-items-center justify-content-center mt-2" v-if="submitted">
          <ul class="list-group">
            <li class="list-group-item">Location is {{userSelections.location}}</li>
            <li class="list-group-item">Name is {{userSelections.name}}</li>
            <li class="list-group-item">Email is {{userSelections.email}}</li>
            <li class="list-group-item">Phone is {{userSelections.phone}}</li>
            <li class="list-group-item">Nationality is {{userSelections.nationality}}</li>
            <li class="list-group-item">Passport Number is {{userSelections.passportNumber}}</li>
            <li class="list-group-item">Gender is {{userSelections.gender}}</li>
            <li class="list-group-item">Mac is {{userSelections.mac}}</li>
            <li class="list-group-item">Connection status is {{userSelections.connectionStatus}}</li>
            <li class="list-group-item">Date is {{userSelections.date}}</li>
          </ul>
        </div>

      </div>
    </template>
  </div>

</template>

<script>

  import SelectBox from './components/SelectBox' 
  import TextBox from './components/TextBox' 
  import axios from 'axios'

  export default {
    name: "App",
    components: {
      SelectBox,
      TextBox,
    },
    data(){
      return {
        loading: false,
        advancedSearch: false,
        inputs: {},
        submitted: false,
        userSelections: {
          location: '',
          name: '',
          email: '',
          phone: '',
          nationality: '',
          passportNumber: '',
          gender: '',
          mac: '',
          connectionStatus: '',
          date: ''
        }
      }
    },
    methods: {

      getData(){
        return axios.get('http://localhost:8080/filters.json').then(res => {
            this.inputs.location = res.data[0]
            this.inputs.name = res.data[1]
            this.inputs.email = res.data[2]
            this.inputs.phone = res.data[3]
            this.inputs.nationality = res.data[4]
            this.inputs.passportNumber = res.data[5]
            this.inputs.gender = res.data[6]
            this.inputs.mac = res.data[7]
            this.inputs.connectionStatus = res.data[8]
            this.inputs.date = res.data[9]
        })
      },
      submit(){
        this.submitted = true
      },
      clear() {
        this.userSelections = {}
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

