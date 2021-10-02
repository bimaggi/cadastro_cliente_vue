<template>
  <div id="app">
    <Form 
      @newClient="newClient" 
      :client-to-edit="clientToEdit"
      @editClient="editClient"
    />
    <List 
      :clients="clients" 
      @delete="deleteClient"
      @edit="setClientToEdit"
    />
  </div>
</template>

<script>
import Form from './components/Form.vue';
import List from './components/List.vue';

export default {
  name: 'App',
  components: {
    Form,
    List
  },
  data(){
    return{
      clients:[],
      clientToEdit:null
    }
  },
  methods:{
    newClient(client){
      this.clients.push(client)
    },
    deleteClient(index){
      this.clients.splice(index,1)
    },
    setClientToEdit(index){
      this.clientToEdit = { ...this.clients[index], index }
    },
    editClient(client){
      this.clients.splice(this.clientToEdit.index,1,client)
      this.clientToEdit = null
    }
  }
}
</script>

<style>
body{
  background:rgb(7, 7, 29);
  color: white;
}

</style>
