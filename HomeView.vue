<template>
  <v-container>
    <v-row>
      <v-col cols="12">
              <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Pretraga vozača"
                single-line
                hide-details
                ></v-text-field>
      </v-col>
    </v-row>
        <v-row>
          <v-col
            v-for="vozac in vozaci"
            :key="vozac.FirstName"
            cols="4"
          >
            <v-card height="200">
              <v-card-text>
                <h2>{{vozac.FirstName}}</h2>
                <h3>{{vozac.LastName}}</h3>
              </v-card-text>
            </v-card>
          </v-col>
        </v-row>
        <v-col cols="12">
          <v-row>
          <v-pagination
            v-model="page"
            :length="6"
            ></v-pagination>
        </v-row>
        </v-col>
      </v-container>
</template>

<script>


export default {
  name: 'HomeView',
  

  data(){
    return{
      vozaci:[],
      page:1,
      ukupnoVozaca:0,
      search:''
    }
  },

  created(){
    console.log('created')
    this.getData();
  },

  methods:{
    getData(){
        let api="https://api.sportsdata.io/nascar/v2/json/drivers?key=036c8f2fea974ebd86b8ef179ebcc3ac"
        this.axios.get(api).then((response) => {
        console.log(response.data)
        this.vozaci=response.data
        this.ukupnoVozaca=response.data.lenght
        
      })
    }
  }
}
</script>
