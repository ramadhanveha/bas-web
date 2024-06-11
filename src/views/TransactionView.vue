<script setup>
import { reactive,inject } from 'vue';
import { VNumberInput } from 'vuetify/labs/VNumberInput'
const data = reactive({
    account_id: "",
    bank_id:"",
    amount:0,
    pesanLogin: "",
    snackbar: false,
    transaction_date:"",
    accounts:[],
    banks:[],
})

const myAxios = inject('myAxios')

myAxios.get("/account/get").then((response) => {
  data.accounts = response.data.data
}).catch((error) => {
  console.error("Failed to fetch accounts:", error);
});

myAxios.get("/bank/get").then((response) => {
  data.banks = response.data.data
  console.log(data.banks)
}).catch((error) => {
  console.error("Failed to fetch accounts:", error);
});

console.log(data.accounts)
const submit = () => {
    console.log("login clicked",data);
    myAxios.post("/transaction/transfer-bank",{
      account_id:data.account_id,
      bank_id:data.bank_id,
      amount:data.amount,
      transaction_date:data.transaction_date,
    }).then((res) => {
      if(res.status==200){
        data.pesanLogin="transfer success"
      }
      data.snackbar= true
    }, (err) => {
      data.pesanLogin = "transfer failed"
      data.snackbar = true
    })
     
}
</script>

<template>
  <v-card class="pa-3">
    <div>
      <div>
        <label for="account_id">account_id</label>
        <select v-model="data.account_id" style="width: 100%; border: 1px solid #ccc; padding: 8px; border-radius: 4px;" id="account_id" >
          <option v-for="account in data.accounts" :key="account.AccountID" :value="account.AccountID">
            {{ account.Username }}
          </option>
        </select>
      </div>
      <div>
        <label for="bank_id">bank_id</label>
        <select v-model="data.bank_id" style="width: 100%; border: 1px solid #ccc; padding: 8px; border-radius: 4px;" id="bank_id" >
          <option v-for="bank in data.banks" :key="bank.Bank_code" :value="bank.Bank_code">
            {{ bank.Name }}
          </option>
        </select>
      </div>
      <div>
        <label for="amount">amount</label>
        <v-number-input id="amount" v-model="data.amount"/>
      </div>
      <div>
        <label for="transaction_date">Transaction date</label>
        <v-text-field id="transaction_date" model-value="2024-05-03T00:00:00+07" v-model="data.transaction_date" />
      </div>
      <v-btn @click="submit">
        Button
      </v-btn>
    </div>
  </v-card>
  <v-snackbar v-model="data.snackbar">
    {{ data.pesanLogin }}
    <template v-slot:actions>
      <v-btn color="pink" variant="text" @click="data.snackbar = false">
        Close
      </v-btn>
    </template>
  </v-snackbar>
</template>
  <script>
    
  </script>