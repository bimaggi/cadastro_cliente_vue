<template>
  <div class="form">
    <h1>Cadastro de clientes</h1>
    <form @submit.prevent="sendForm()">
      <input type="text" v-model="firstName" placeholder="Digite o primeiro nome">
      <input type="text" v-model="lastName" placeholder="Digite o ultimo nome">
      <input type="text" v-model="email" placeholder="Digite o email">
      <div class="radio">
        <div class="btnRadio">
        <input type="radio" v-model="isLegalPerson" id="cpf" name="cad" :value="false">
        <label for="">CPF</label>
        </div>
        <div class="btnRadio">
        <input type="radio" v-model="isLegalPerson" id="cpf" name="cad" :value="true">
        <label for="">CNPJ</label>
        </div>
      </div>
      <input type="text" v-model="cpf" v-if="shouldShowCpf" placeholder="Digite o CPF">
      <input type="text" v-model="cnpj" v-else placeholder="Digite o CNPJ">
      <button>Cadastrar</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'Form',
  props:{ 
    clientToEdit:{
      type:Object,
      required:false,
      default:null
    }
  },
  data(){
    return{
      firstName:"",
      lastName:"",
      email:"",
      cpf:"",
      cnpj:"",
      isLegalPerson: false,
      shouldShowCpf: true,
    }
  },
  watch:{
    isLegalPerson(value){
      this.shouldShowCpf = !value 
    },
    clientToEdit(value){
      if(value){
        this.firstName= value.firstName
        this.lastName= value.lastName
        this.email= value.email
        this.cpf= value.cpf
        this.cnpj= value.cnpj
        this.isLegalPerson= value.isLegalPerson
      }
    }
  },
  methods:{
    sendForm(){
      const { firstName, lastName, email, cpf, cnpj, isLegalPerson } = this
      if(this.clientToEdit){
        this.$emit("editClient",{firstName,lastName, email,cpf,cnpj,isLegalPerson})
      }else{
        this.$emit("newClient",{firstName,lastName, email,cpf,cnpj,isLegalPerson})
      }
       this.resetForm()
    },
    resetForm(){
      this.firstName=""
      this.lastName=""
      this.email=""
      this.cpf=""
      this.cnpj=""
      this.isLegalPerson= false
      this.shouldShowCpf= true
    }
  }
}
</script>

<style scoped>
.form{
  width: 60%;
  display: flex;
  flex-direction: column;
  margin: auto;
  text-align: center;
}
form{
  display: flex;
  flex-direction: column;
  width: 60%;
  margin: auto;
}
input{
  margin: 1%;
  padding: 10px;
  border-radius: 5px;
}
button{
  width: 20%;
  margin: auto;
  margin-top: 2%;
  padding: 5px;
  border-radius: 5px;
}
.radio{
  width: 60%;
  display: flex;
  justify-content: space-around;
  margin: auto;
}
.btnRadio{
  display: flex;
  padding: 5px;
  align-items: center;
}


</style>
