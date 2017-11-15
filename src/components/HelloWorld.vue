<template>
  <div class="hello">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)">{{item.label}}</li>
    </ul>
  </div>
</template>

<script>
import Store from ".././store"
console.log(Store)
export default {
  data:function () {
    return {
      title: 'this is a todoList',
      items:Store.fetch(),
      newItem:"",
    }
  },
  watch:{
    items:{
      handler:function(items){
      console.log(items)
      Store.save(items)
      },
      deep:true
    }
  },
  methods:{
    toggleFinish(item){
     item.isFinished=!item.isFinished;
    },
    addNew:function(){
      this.items.push({
        label:this.newItem,
          isFinished:false
      });
      this.newItem="";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.finished{
  text-decoration:underline;
}

</style>
