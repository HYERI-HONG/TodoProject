<template>
  <div>
    <!-- ul>li*3 + tab -->
      <ul>
        <li v-for="(todoItem, index) in todoItems" v-bind:key="todoItem.item" class="shadow">
           <i class="checkBtn fa fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" 
           @click="toggleComplete(todoItem)"></i>
           <!-- v-bind:class -> boolean값이 true일 경우 class 추가-->
            <span v-bind:class="{textCompleted: todoItem.completed}" >{{todoItem.item}}</span>
            <span type="button" class="removeBtn" @click="removeTodo(todoItem.item, index)">
                <i class="fa fa-trash-alt"></i>
            </span>
        </li>
      </ul>
  </div>
</template>

<script>
export default {
  data : function(){
    return {
      todoItems : []
    }
  },
  methods : {
    removeTodo : function(todoItem, index){
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);  //배열 api, 특정 index값에서 n개 지우기
    },
    toggleComplete: function(todoItem){
      todoItem.completed = !todoItem.completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    }
  },
  created: function(){
    if(localStorage.length > 0){
      for(var i = 0 ; i < localStorage.length ; i++)
        if(localStorage.key(i) != 'loglevel:webpack-dev-server'){
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
    }
  }

}
</script>

<style scoped>
ul {
    list-style-type:none;
    padding-left:0;
    margin-top:0;
    text-align:left;
}

li {
    display:flex;
    min-height:50px;
    height:50px;
    line-height:50px;
    margin:.5rem 0;
    padding:0 .9rem;
    background:#fff;
    border-radius:5px;
}

.checkBtn {
    line-height:45px;
    color:#62acde;
    margin-right:5px;
}

.checkBtnCompleted {
  color : #b3adad;
}

.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}

.removeBtn {
    margin-left:auto;
    color:#de4343;
}
</style>
