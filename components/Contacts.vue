<template>
<div class="dasboard">
  <h1 class="subheading">Dashboard</h1>
  <v-container class="my-5 ">
    <v-card class="" flat v-for="person in profile" :key="person.id">
    <NuxtLink :to="`/contact/${person.id}/`" class="link">
     
      <v-layout class="">
        <v-avatar class="ma-2">
      <v-img
        src="https://cdn.vuetifyjs.com/images/john.jpg"
        alt="John"
      ></v-img>
      
    </v-avatar>

        <v-flex  xs12 md6 class="mb-3">
          
          <div class="caption blue--text font-weight-light">Name</div>
          <div class="mr-4">{{ person.name }}</div>
          

        </v-flex>
        <v-flex xs12 md6>
 
          <div class="caption blue--text font-weight-light">Phone no.</div>
          <div class="">{{ person.phone }}</div>

        </v-flex>
        <v-flex xs12 md6>
          <div class="caption blue--text font-weight-light ">Email</div>
          <div class="">{{ person.email }}</div>
        </v-flex>
        <v-flex xs12 md6>
          <div class="caption blue--text font-weight-light mr-3 ">Job Description</div>
          <div class="mr-4">{{ person.description }}</div>
        </v-flex>

        <v-flex xs12 md6 class="mt-2" @click.prevent="deleteContact(person.id)">
          <v-btn class="mr-4 "><v-icon color="error">mdi-delete</v-icon></v-btn>
        </v-flex>
      </v-layout>
      <v-divider></v-divider>
   
    </NuxtLink>
  
    </v-card>
  </v-container>
</div>
  </template>
  <script>
    export default {
      data () {
        return {
          profile:[],
          desserts: [
            {
              name: 'Frozen Yogurt',
              calories: 159,
            },
            {
              name: 'Ice cream sandwich',
              calories: 237,
            },
            {
              name: 'Eclair',
              calories: 262,
            },
            {
              name: 'Cupcake',
              calories: 305,
            },
            {
              name: 'Gingerbread',
              calories: 356,
            },
            {
              name: 'Jelly bean',
              calories: 375,
            },
            {
              name: 'Lollipop',
              calories: 392,
            },
            {
              name: 'Honeycomb',
              calories: 408,
            },
            {
              name: 'Donut',
              calories: 452,
            },
            {
              name: 'KitKat',
              calories: 518,
            },
          ],
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
    methods:{
      deleteContact(id){
        console.log(id)
        this.$apollo.mutate({
          mutation:require('../gql/mutation/profileMutation').ProfileDeleteMutation,
          variables:{
            id:id
          }
 
        }).then(rs=>
          console.log(rs),
          this.$router.go('/')
        ).catch(e=>console.log(e))
      }
    }
  }
  </script>
  <style scoped>
.top{
  display: flex;
  
}
.link{
  color: inherit;
  text-decoration: none;
}
  </style>