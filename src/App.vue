<template>
  <v-app>
    <v-main>
      <v-alert v-show="added"
              border="right"
              dense
                outlined
            prominent
            text
            type="success"
           
            >account added successfully
            </v-alert>
     
     <div>
    
       <span  v-for="(tab,index) in tabs" :key="index" 
       @click="selectedtab=tab" :class="[selectedtab==tab ? act:'']"> 
         {{tab}} </span>
       
     </div>
        <v-container v-show="selectedtab=== 'acdetails'">

             <Accounts  :accounts=accounts @delete-account="remove"></Accounts>
             
          </v-container>
          <!--<HelloWorld />-->
          <v-form  ref="form" v-show="selectedtab=== 'acform'">
            <v-container>
              <v-row>
                <v-col cols="10" md="4">
                  <v-text-field v-model="account" :counter="16" 
                  :rules="[()=> !!account || 'this filed is required',
                  ()=> account.length<=16 || 'account should be less than 16 characters']"
                  label="account" required>
                  </v-text-field>
                 
                </v-col>
              </v-row>
              <v-row>
                 <v-col cols="10" md="4">
                  <v-text-field   v-model="username" 
                  
                  label="Name" required>
                  </v-text-field>
                 </v-col>
              </v-row>
              <v-row>
                  
                  <v-col cols="10" md="4">
                  <v-text-field   v-model="password"  label="password" required>
                  </v-text-field>
                </v-col>
              
              </v-row>
              <v-row>
                <v-col >
                  <v-btn @click="submit">submit</v-btn>
                </v-col>
              </v-row>
            </v-container>
          </v-form>
          
           
    </v-main>
  
  </v-app>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Accounts from './components/accounts.vue'
export default {
  name: 'App',
  data:function(){

    return {
      selectedtab:'acform',
      tabs:['acform','acdetails'],
      accounts:[],
      account:'',
    username:'',
    password:'',
    id:0,
    added:false,
    act:'activ'
    
    }

  },
  components: {
    //HelloWorld
    Accounts
  },
  methods:{
    remove(item){ 
      for(var i=0;i<this.accounts.length;i++){
          if(this.accounts[i].id==item.id){
                 this.accounts.splice(i,1);
                 break;
          }
      }
    },
    
    submit(){
      if(this.$refs.form.validate()){
       this.added=true
      this.accounts.push({id:this.id++,
        account:this.account,
      username:this.username,
      password:this.password.substring(this.password.length-3,this.password.length)
      })
      }
      this.account=""
    this.username=""
    this.password=""
    setTimeout(()=>this.added=false,2000)
   
    
    }
    
  }
  
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.activ{

color: darkred;

}
</style>
