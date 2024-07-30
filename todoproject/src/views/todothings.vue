<script>

let id = 1

export default {
  
  data() {
    return {
      todolistThings: [
        {thingname : 111, id : 1, done : true}
      ],
      keyword: '',
      filtodolistThings: [],
      showing: 0
    }
  },


  methods: {

    clickbox(thing) {
      // thing.done === true? thing.done = false : this.done = true
      thing.done = !thing.done
    },
    addNewThing() {
      this.todolistThings.push({ id: id++, thingname: this.keyword , done: false })
      this.keyword = ''
    },
    removeTodo(todolistThings) {
      this.todolistThings = this.todolistThings.filter((t) => t.done ===false )
    },
 
  
    showCompleted() {
      this.showing = 1
      console.log("gg");
    }
  },
  computed: {
    sumNotDoThingNumber() {
      return this.todolistThings.filter( thing  =>  thing.done === false).length
    },
    flterall() {
      return this.todolistThings
    },
    flterdone() {
      return this.todolistThings.filter((thing) => thing.done === true)
      // return this.todolistThings = this.todolistThings.filter((thing) =>  {  thing.done === true })
    },
    flternotdone() {
      return this.todolistThings.filter((thing) =>  { return thing.done === false })
    },
    
    currentTodoList() {
      switch (this.showing) {
        case 0:
          return this.todolistThings

        case 1:
          return this.todolistThings.filter((thing) => thing.done === true)
      
        default:
          return this.todolistThings.filter((thing) => thing.done === false)
          break;
      }
    }
  }
}
</script>

<template>
  <div class="about1">
    <div>
      <h1>todos</h1>
    </div>
    
    <div>
     <div>
      <input v-model="keyword" type="text" placeholder="What needs to be done?"  @keydown.enter="addNewThing"/>
      <button @click.prevent="addNewThing()">添加</button>
     </div>
      
      <br>
      <ul>
        <li v-for="thing in currentTodoList" :key="thing.id">
          <input type="checkbox" key="thing.id" @click="clickbox(thing)" :checked="thing.done"></input>
          <input type="text" v-model="thing.thingname"/>
          <button @click="removeTodo(thing)">x</button>
        </li>
      </ul>
      
    <div>
      <p>{{ sumNotDoThingNumber }}  items left</p>
      <button @click="showing = 0">all</button>
      <button @click="showing = 3">active</button>
      <button @click="showing= 1">completed</button>
      <button @click="removeTodo">clear completed</button>
    </div>
  </div>
  <div>
 
  </div>
  </div>
  
</template>

<style>
@media (min-width: 1024px) {
  .about1 {
    min-height: 100vh;
    display: flex;
    align-items: center;
    flex-direction: column;
  }
}
</style>
