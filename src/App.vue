<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
  
      <li v-for="item in items" v-bind:class="{finish:item.isF}" v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store.js'
export default {
  data: function () {
    return {
      title: '这是测试--todolist',
      items: Store.fetch(),
      newItem: ''
    }
  },
  methods: {
    toogleFinish: function (item) {
      item.isF = !item.isF
    },
    addNew: function () {
      this.items.push({
        label: this.newItem,
        isF: false
      })
      this.newItem = ''
    }
  },
  watch: {
    items: {
      handler: function (items) {
        Store.save(items)
      },
      deep: true
    }

  }
}
</script>

<style>
.finish {
  text-decoration: underline;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
