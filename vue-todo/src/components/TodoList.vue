<template>
  <div>
      <ul>
        <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
          <i class="fas fa-check"  v-bind:class="{checkBtnCompleted : todoItem.completed}" v-on:click="toggleComp(todoItem, index)"></i>
          {{ todoItem.item }}
          <span v-bind:class="{textCompleted : todoItem.completed}" v-on:click="removeTodo(todoItem, index)">
            <i class="fas fa-trash-alt"></i>
          </span>
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  data: function(){
    return{
      todoItems: []
    }
  },
  methods:{
    removeTodo: function(item, idx){
      localStorage.removeItem(item);
      this.todoItems.splice(idx, 1);
    },
    toggleComp:function(item, idx){
      console.log(item,idx);
      item.completed = !item.completed;
      localStorage.removeItem(item.item);
      localStorage.setItem(item.item, JSON.stringify(item))
    },
  },
  created: function(){
    if(localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++){
        this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
      }
    }
  }
}
</script>

<style>

</style>