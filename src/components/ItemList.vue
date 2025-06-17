<script setup lang="ts">
import { ref } from 'vue'

interface Item {
  name: string
  price: number
}

const items = ref<Item[]>([
  { name: 'たまご', price: 100 },
  { name: 'りんご', price: 160 }
])
const newItemName = ref<string>('')
const newItemPrice = ref<number>(0)

const addItem = () => {
  if (newItemName.value === '') {
    alert('名前を入力してください。')
    return
  }
  if (newItemPrice.value <= 0) {
    alert('価格は0より大きい整数値で入力してください。')
    return
  }
  items.value.push({ name: newItemName.value, price: newItemPrice.value })
  newItemName.value = ''
  newItemPrice.value = 0
}

</script>

<template>
  <div>
    <div>Itemlist</div>
    <ul>
      <il v-for="item in items" :key="item.name" :class="{over500: item.price >= 500}">
        <div>名前：{{ item.name }}</div>
        <div>{{ item.price }}円</div>
        <div v-if="item.price >= 10000">高額商品</div>
      </il>
    </ul>
    <div>
      <label>
        名前
        <input v-model="newItemName" type="text" />
      </label>
      <label>
        価格
        <input v-model="newItemPrice" type="number" />
      </label>
      <button @click="addItem">追加する</button>
    </div>
  </div>
</template>

<style>
.over500 {
  color: red;
}
</style>
