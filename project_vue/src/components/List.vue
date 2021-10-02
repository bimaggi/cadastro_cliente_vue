<template>
  <div class="list">
    <h1>Lista de clientes</h1>
    <table>
      <thead>
        <th>Nome Completo</th>
        <th>Email</th>
        <th>CPF/CNPJ</th>
        <th>É pessoa Jurídica</th>
        <th>Ações</th>
      </thead>
      <tbody>
        <p v-if="!clients.length">Não há clientes cadastrados</p>
        <ListItem 
          v-for="(client,index) of clients" 
          :key="index" 
          :client="client"
          @delete="emitDelete(index)"
          @edit="emitEdit(index)"
        />
      </tbody>
    </table>
  </div>
</template>

<script>
import ListItem from './ListItem.vue';

export default {
  name: 'List',
  components:{
    ListItem
  },
  props:{
    clients:{
      type:Array,
      required:true
    }
  },
  methods:{
    emitDelete(index){
      this.$emit("delete",index)
    },
    emitEdit(index){
      this.$emit("edit",index)
    }
  }
}
</script>

<style scoped>
.list{
  width: 90%;
  margin: auto;
  background:white;
  color: rgb(7, 7, 29);
  border-radius: 5px;
  padding-bottom: 4%;
}
h1{
  text-align: center;
  padding-top: 1%;
}
table{
  width: 90%;
  margin: auto;
}
thead{
  background: rgb(7, 7, 29);
  color: white;
  font-size: 1.2rem;
}
tbody{
  background: white;
}
p{
  text-align: center;
  font-size: 1.2rem;
}

</style>
