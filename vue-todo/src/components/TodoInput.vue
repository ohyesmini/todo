<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>
    <!-- use the modal component, pass in the prop -->
    <modal v-if="showModal" @close="showModal = false">
        <!--
      you can use custom content here to overwrite
      default content
    -->
      <h3 slot="header">
        warning!!
        <i class="closeModalBtn fas fa-times" @click="showModal=false"></i>
      </h3>
       <h3 slot="body">
        plz insert sth
      </h3>
       
    </modal>

  </div>
</template>

<script>
import Modal from './common/Modal.vue'
export default {
  data: function(){
    return{
      newTodoItem: "",
      showModal: false
    }
  },

  methods: {
    addTodo: function(){
      console.log(this.newTodoItem);
      //save
      if(this.newTodoItem != ''){
        
        this.$emit('addItem', this.newTodoItem)
        this.clearInput();
      }else{
        this.showModal = !this.showModal;


      }
    },
    clearInput: function(){
      //initial input box
      this.newTodoItem = '';
    }
  },
  components:{
    Modal: Modal
  }
  



}
</script>


<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}

.closeModalBtn {
  color: #42b983;
  vertical-align: middle;
}
</style>
