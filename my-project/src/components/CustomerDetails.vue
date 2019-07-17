<template>
  <div class="customerDetails container">
  	<router-link to="/" class="btn btn-default">返回</router-link>
 	<h1 class="page-header">{{customer.name}}
 		<span class="pull-right">
 			<router-link to="/" class="btn btn-primary" :to="'/edit/'+customer.id">编辑</router-link>
 			<button class="btn btn-danger" @click="deleteCustomer(customer.id)">删除</button>
 		</span>
 	</h1>
 	<ul class="list-group">
 		<li class="list-group-item"><span class="glyphicon glyphicon-phone-alt"></span>{{customer.phone}}</li>
 		<li class="list-group-item"><span class="glyphicon glyphicon-envelope"></span>{{customer.email}}</li>
 	</ul>
	<ul class="list-group">
 		<li class="list-group-item"><span class="glyphicon glyphicon-font"></span>{{customer.education}}</li>
 		<li class="list-group-item"><span class="glyphicon glyphicon-home"></span>{{customer.graduateschool}}</li>

		<li class="list-group-item"><span class="glyphicon glyphicon-road"></span>{{customer.profession}}</li>
 		<li class="list-group-item"><span class="glyphicon glyphicon-user"></span>{{customer.profile}}</li> 		
 	</ul> 	
  </div>
</template>

<script>
export default {
  name: 'customerDetails',
  data () {
    return {
      customer:""
    }
  },
  methods:{
		fetchCustomers(id){
    		this.axios.get('http://localhost:3000/users/'+id).then((response) => {
 		 	this.customer = response.data
			})
    	},
    	deleteCustomer(id){
    		this.axios.delete('http://localhost:3000/users/'+id)
    		.then((response)=>this.$router.push({path:'/',query:{alert:'用户删除成功'}}))
    	}  	
  },
  created(){
  	this.fetchCustomers(this.$route.params.id)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	
</style>