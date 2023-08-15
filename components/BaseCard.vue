<template lang="">
          <section class="base-card">
            <h4 style="margin-top: 0">{{ data.name }}</h4>
            <p>Migrate to list</p>
            <!-- <pre> {{data}} </pre> -->
             <!-- <pre> {{migrateList}} </pre> -->
             <!-- <pre>{{parentColumn}}</pre> -->
             <!-- <p> {{migrateListTarget}} </p> -->
            <select name="migrate-list" id="migrate-list" style="padding: 5px; width: 100%; margin-bottom: 10px"  v-model="migrateListTarget">
              <option v-for="column in filteredMigrateList" :key="`migrate-${column.columnName}`" :value="column.columnName">{{ column.columnName }}</option>
            </select>
            <button style="padding: 10px 5px" @click="migrateCard()">Migrate</button>
        </section>
</template>
<script setup>
import {ref, watchEffect} from 'vue'

const migrateListTarget = ref('')
const initialX = ref(0)

onMounted(()=>{
   initialX.value  = props.position.x;
})

 const props = defineProps({
    data: Object,
    migrateList: Array,
    parentColumn: String,
    position: Object,

 })

 watchEffect(()=>{

   if(props.position.x - initialX.value > 250) {
        emits('migrate-item', {
            cardId: props.data.id,
            targetColumn: "Killer",
            originalColumn: props.parentColumn
        })
   } else if (props.position.x - initialX.value > 500) {
      emits('migrate-item', {
            cardId: props.data.id,
            targetColumn: "Puschek",
            originalColumn: props.parentColumn
        })
   }
 })

 const emits = defineEmits({
    'migrate-item': null
 })

 const filteredMigrateList = computed(()=>{
    return props.migrateList.filter(item => item.columnName !== props.parentColumn)
 })

 const migrateCard = () => {
    const targetColumn = migrateListTarget.value;
    const originalColumn = props.parentColumn;

    if(targetColumn !== originalColumn) {
        emits('migrate-item', {
            cardId: props.data.id,
            targetColumn,
            originalColumn
        })
    }
 }
</script>
<style lang="css" scoped>
.base-card{
  border: 1px solid #222;
  padding: 10px;
  list-style: none;
  background-color: #fff;
  margin-bottom: 10px;
}
</style>

