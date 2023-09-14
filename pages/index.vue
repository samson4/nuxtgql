<template>
  <v-row justify="center w-100" >
    <v-col cols="12" sm="12" md="12">

      <v-card  class="logo py-4 w-75 ">
        <v-card-title class="headline">
          Welcome to the Vuetify + Nuxt.js template
        </v-card-title>
        <Contacts/>
        <v-card-actions>
          <v-spacer />
          
          <v-btn
          @click="createContact"
         
          rounded
            color="primary"
          ><v-icon>mdi-plus</v-icon>
            Create Contact
          </v-btn>
        </v-card-actions>
        <div class="text-center">
    <v-dialog
      v-model="dialog"
      width="auto"
    >
      <v-card>
        <v-sheet width="300" class="ma-3 pa-3">
    <v-form >
      <v-text-field
        v-model="name"
        label="Name"
        required
      ></v-text-field>
      <v-text-field
        v-model="email"
        label="Email "
      ></v-text-field>
      <v-text-field
        v-model="phone"
        label="Phone number"
        required
      ></v-text-field>
      <v-text-field
        v-model="description"
        label="description"
      ></v-text-field>
    </v-form>
  </v-sheet>
        <v-card-actions>
          <v-btn color="primary" block @click="createuser">Submit</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import gql from "graphql-tag";
import ProfileMutation from '../gql/mutation/profileMutation'
const Add_Profile = gql`
mutation ProfileMutation($objects:[profile_insert_input!]!) {
  insert_profile(objects:$objects ) {
    returning {
      id
      name
      phone
      email
      description
    }
  }
}

`;
export default {
  name: 'IndexPage',
 
  data(){
    return{
      profile:[],
      dialog: false,
      name:'',
      email:'',
      phone:'',
      description:''
    }
  },
  methods:{
  createContact(){
    this.dialog=true
    },
    createuser(){
      this.$apollo.mutate({
  mutation:require('../gql/mutation/profileMutation').ProfileMutation,
  variables:{
    objects:{
    name:this.name,
    phone:this.phone,
    email:this.email,
    description:this.description,
    }
   
  }
}).then(rs=>
  console.log(rs.data),
  this.$router.go('/')
).catch(e=>console.log(e))
    }
  },

  mounted(){
    this.$apollo.query({
      query:require(`~/gql/queries/profile`).MyQuery
    }).then(rs=>{
      console.log(rs.data.profile)
      this.profile = rs.data.profile
      console.log(this.profile)
    }).catch(e=>{
      console,log(e)
    })
  },




}
</script>
