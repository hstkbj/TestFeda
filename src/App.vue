<template>
  <div>
    <h1>Test FedaPay</h1>
    <button class="btn btn-primary"  id="pay-btn">Payer 1000</button>
  </div>
</template>

<script>
/* global FedaPay */
export default {
  name: 'App',
  data(){
    return{
      
    }
  },
  mounted(){
    if (window.FedaPay) {
      console.log("FedaPay est chargé :", window.FedaPay);
    } else {
      console.error("FedaPay n'est pas chargé !");
    }
    this.testfunction()
  },
  methods:{
    testfunction(){
        FedaPay.init("#pay-btn",{
          public_key: 'pk_sandbox_L4pS0w5ats9iXVhDv44P3OkY',
          transaction: {
            amount: 1000,
            description: 'Acheter mon produit'
          },
          customer: {
            email: 'johndoe@gmail.com',
            lastname: 'Doe',
            firstname: 'John',
          },
          onComplete:({reason,transaction})=>{
            console.log(reason, transaction)

            if (transaction.status === "approved") {
              console.log(transaction.status)
            }
          }
        })
    }
  }
 
}
</script>

<style>

</style>
