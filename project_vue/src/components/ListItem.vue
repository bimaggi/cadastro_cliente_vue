<template>
    <tr>
			<td>{{fullName}}</td>
			<td>{{client.email}}</td>
			<td>{{document}}</td>
			<td>{{parseIsLegalPerson}}</td>
			<td class="btn">
				<button class="edit" @click="emitEdit">Editar</button>
				<button class="del" @click="emitDelete">Deletar</button>
			</td>
		</tr>
</template>

<script>
export default{
	props:{
		client:{
			type:Object,
			required:true
		}
	},
	computed:{
		fullName(){
			return `${this.client.firstName} ${this.client.lastName}`
		},
		document(){
			return this.client.isLegalPerson ? this.client.cnpj : this.client.cpf
		},
		parseIsLegalPerson(){
			return this.client.isLegalPerson ? 'Sim' : 'Não'
		}
	},
	methods:{
		emitDelete(){
			this.$emit("delete")
		},
		emitEdit(){
			this.$emit("edit")
		}
	}
}

</script>
<style scoped>

td{
	background: rgba(7, 7, 29, 0.137);
	padding: 3px;
	text-align: center;
	font-size: 1.1rem;
}
.btn{
	display: flex;
	justify-content: space-around;
	padding: 5px;
}
.edit{
	background: rgba(7, 7, 29, 0.137);
	font-size: .9rem;
}
.del{
	background: red;
	color: white;
	font-size: .9rem;
}

</style>


