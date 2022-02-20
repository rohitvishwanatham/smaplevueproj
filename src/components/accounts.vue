<template>
  <v-container>
    <v-data-table
    :headers="headers"
    :items="accounts"
    >
   
     <template v-slot:item.actions="{ item}">
      
      <v-icon
      
        small
        @click="remove(item)"
      >
        mdi-delete
      </v-icon>
     </template>
        
    </v-data-table>
   <!-- <v-row>
        <v-col>
            <p>account</p>
        </v-col>
        <v-col>
            <p>username</p>
        </v-col>
        <v-col>
            <p>password</p>
        </v-col>
    </v-row>
    <v-row v-for="(act,index) in accounts" :key="index">
       
      <v-col>
        <p>{{ act.account }}</p>
      </v-col>
      <v-col>
        <p>{{ act.username }}</p>
      </v-col>
      <v-col>
        <p>{{ act.password }}</p>
      </v-col>
      <v-col>
          <v-btn @click="remove(index)">delete</v-btn>
           <v-btn>edit</v-btn>
      </v-col>
    
      
      
    </v-row>-->
  </v-container>
</template>
<script>
export default {
  name: "Accounts",
  data(){
      return {
          headers:[
              {text:'account' ,value:'account'},
              {text:'username' ,value:'username'},
              {text:'password' ,value:'password'},
              {text:'Actions' ,value:'actions',sortable:false}
              
          ]
      }
  },
  props: {
    accounts:{
        type:Array,
        
    }
  },
  methods:{
      remove(id){
        this.$emit('delete-account',id);
      }
  }
 

};
</script>