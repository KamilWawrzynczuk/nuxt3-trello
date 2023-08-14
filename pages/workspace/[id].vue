<script>
import { workspaceList } from '../../store/global.js'

export default {
  setup() {
    return {
      workspaceList
    }
  },
  data: () => ({
    newColumnName: '',
    workspaceName: '',
    boardList: [],
    board: {
      name: '', 
      columns: []
    },
  }),
  methods: { 
    createColumn() {
      if(this.newColumnName) {
        this.board.columns.push({
        columnName: this.newColumnName,
        newItemName: '',
        items:[]
      })

      this.newColumnName = ''
      }
    
    },
    createCard(column){
      if(column.newItemName) {
        column.items.push({
        id: 123,
        name: column.newItemName
      })
      }

      column.newItemName = ' '
      
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
  <main class="workspace-page">
  <h1>{{ workspaceName }} workspace {{ $route.params.id }}</h1>
  <section>
    <input type="text" @keydown.enter="createColumn" v-model="newColumnName" placeholder="New column title" style="display: block; width: 100%; padding: 5px; font-smooth: 0.9rem; margin-bottom: 10px;" />
    <button @click="createColumn" style="margin-bottom: 15px;">Create Column</button>
    <div class="column-grid">
      <section class="board-column" v-for="column in board.columns">
         <h3 style="margin-top: 5px;">{{ column.columnName  }}</h3>
        <input type="text" v-model="column.newItemName" @keyup.enter="createCard(column)"  style="padding: 5px; font-size: 0.9rem; margin-bottom: 10px;" placeholder="New Card Item">
        <button @click="createCard(column)" style="margin-bottom: 15px;">Create Cart</button>
        <ul style="margin: 0; padding: 0">
          <li v-for="item in column.items" :key="item.id" class="base-card">{{ item.name }}</li>
        </ul>
      </section>
    </div>
  </section> 
</main>
</template>

<style>

.base-card{
  border: 1px solid #222;
  padding: 10px;
  list-style: none;
  background-color: #fff;
}

.workspace-page{
  padding: 30px;
}
.workspace-page h1 {
  margin-top: 0;
}

.column-grid {
  display: grid;
  grid-template-columns: repeat(v-bind(board.columns.length), 1fr);
} 

.board-column {
  background-color: #eee; 
      display: flex;
      flex-direction: column;
      border: 1px solid black;
      height: 80vh;
      margin-right: 10px;
      padding: 10px;
}

</style>