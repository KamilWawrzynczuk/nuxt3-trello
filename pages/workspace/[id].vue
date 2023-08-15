<script>
import { workspaceList } from '../../store/global.js'
import { UseDraggable } from '@vueuse/components'
import { ref } from 'vue'

export default {
  setup() {
    return {
      workspaceList
    }
  },
  components: {
    UseDraggable
  },
  data: () => ({
    newColumnName: '',
    workspaceName: '',
    boardList: [],
    board: {
      name: '', 
      columns: [
        {
          columnName: 'Fluffy',
          newItemName: '',
          items:[ {
            id: 1234,
            name: 'Punch Deaf'
            },]
        },
        {
          columnName: 'Killer',
          newItemName: '',
          items:[ 
            {
            id: 12345,
            name: 'Suck kick'
            },
            ]
        },
        {
          columnName: 'Puschek',
          newItemName: '',
          items:[
            {
            id: 123456,
            name: 'Blow middle'
            }]
        }
       
        
    ]
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
      
    },
    migrateItem({cardId, targetColumn, originalColumn}) {
      // move item to new list
        this.board.columns.find(column => column.columnName === targetColumn).items.push(
          this.board.columns.find(column=> column.columnName === originalColumn).items.find(item => item.id === cardId)
        )
      // remove item from old list

       const parentColumn = this.board.columns.find(column => column.columnName === originalColumn)
       parentColumn.items = parentColumn.items.filter(item => item.id !== cardId)
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
          
            <li  v-for="item in column.items" :key="item.id" class="base-card" style=" list-style: none;">
              <UseDraggable :initialValue="{ x: 50, y: 10 }" v-slot="{ x, y }" style="position: fixed">
                <BaseCard :data="item" :migrateList="board.columns" :parentColumn="column.columnName" @migrate-item="migrateItem" :position="{x,y}"/>
              </UseDraggable>
            </li>
         
        </ul>
      </section>
    </div>
  </section> 
</main>
</template>

<style>



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