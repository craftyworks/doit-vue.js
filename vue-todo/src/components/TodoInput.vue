<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo" placeholder="Type what you have to do">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>

    <modal v-if="showModal" v-on:close="showModal = false">
      <h3 slot="header">경고</h3>
      <p slot="body">
        할 일을 입력하세요.
      </p>
      <span slot="footer" v-on:click="showModal = false">
        <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
      </span>
    </modal>
  </div>
</template>

<script>
  import Modal from './common/Modal.vue'

  export default {
    components: {
      'Modal': Modal
    },
    props: ['editTodoItem'],
    data: function () {
      return {
        showModal: false,
        newTodoItem: ''
      }
    },
    methods: {
      addTodo: function () {
        if (this.newTodoItem.trim() != "") {
          let value = this.newTodoItem.trim()
          this.$emit('add', value)
          this.clearInput()
        } else {
          this.showModal = true
        }
      },
      clearInput: function () {
        this.newTodoItem = ''
      }
    },
    watch: {
      editTodoItem: function (value) {
        this.newTodoItem = value
      }
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
    background: linear-gradient(to right, #6578FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: middle;
  }
</style>
