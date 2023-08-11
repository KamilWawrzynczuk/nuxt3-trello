<script>
import { workspaceList } from '../../store/global.js'

export default {
  setup() {
    return {
      workspaceList
    }
  },
  data: () => ({
    workspaceName: '',
    boardList: [],
    board: {
      name: 'Cherries', 
      columns: []
    },
    newCardItem: '',
  }),
  methods: {
    createColumn() {
      this.board.columns.push({
        items:[]
      })
    },
    createCard(column){
      column.items.push({
        id: 123,
        name: this.newCardItem
      })
    }
  },
  mounted() {
     this.workspaceName = this.workspaceList.find(workspace =>
        workspace.id === Number(this.$route.params.id)
     ).name
  }
}
</script>

<template>
  <h1>{{ workspaceName }} workspace {{ $route.params.id }}</h1>
<section>
  <h2> {{  board.name }}</h2>
   <button @click="createColumn()">Create Column</button>
  <div class="column-grid">
    <section class="board-column" v-for="column in board.columns">
      <input type="text" v-model="newCardItem">
      <button @click="createCard(column)">Create Cart</button>
      <ul>
        <li v-for="item in column.items" :key="item.id">{{ item.name }}</li>
      </ul>
    </section>
  </div>
 
</section> 
</template>

<style>

.column-grid {
  display: grid;
  grid-template-columns: repeat(v-bind(board.columns.length), 1fr);
} 

.board-column {
      border: 1px solid black;
      height: 80vh;
      width: 100px;
      margin-right: 10px;
}
</style>