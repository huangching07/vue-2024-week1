<script setup>
import { ref } from 'vue'
const data = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    desc: '香濃奶茶搭配QQ珍珠',
    price: 50,
    stock: 20
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    desc: '清新冬瓜配上新鮮檸檬',
    price: 45,
    stock: 18
  },
  {
    id: 3,
    name: '翡翠檸檬',
    desc: '綠茶與檸檬的完美結合',
    price: 55,
    stock: 34
  },
  {
    id: 4,
    name: '四季春茶',
    desc: '香醇四季春茶，回甘無比',
    price: 45,
    stock: 10
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    desc: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50,
    stock: 25
  },
  {
    id: 6,
    name: '檸檬冰茶',
    desc: '檸檬與冰茶的清新組合',
    price: 45,
    stock: 20
  },
  {
    id: 7,
    name: '芒果綠茶',
    desc: '芒果與綠茶的獨特風味',
    price: 55,
    stock: 18
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    desc: '抹茶與鮮奶的絕配',
    price: 60,
    stock: 20
  }
])

const editItem = ref({
  id: null,
  name: ''
})

const increaseStock = (id) => {
  const itemIndex = data.value.findIndex((item) => item.id === id)
  data.value[itemIndex].stock++
}

const decreaseStock = (id) => {
  const itemIndex = data.value.findIndex((item) => item.id === id)
  if (data.value[itemIndex].stock > 0) {
    data.value[itemIndex].stock--
  }
}

const editItemName = (id) => {
  const itemIndex = data.value.findIndex((item) => item.id === id)
  editItem.value.id = data.value[itemIndex].id
  editItem.value.name = data.value[itemIndex].name
}

const confirmEdit = () => {
  const itemIndex = data.value.findIndex((item) => item.id === editItem.value.id)
  data.value[itemIndex].name = editItem.value.name
  resetEditItem()
}

const cancelEdit = () => {
  resetEditItem()
}

const resetEditItem = () => {
  editItem.value.id = null
  editItem.value.name = ''
}
</script>

<template>
  <table>
    <thead>
      <tr>
        <th scope="col">品項</th>
        <th scope="col">描述</th>
        <th scope="col">價格</th>
        <th scope="col">庫存</th>
        <th scope="col"></th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in data" :key="item.id">
        <td>
          <span v-if="editItem.id != item.id">{{ item.name }}</span>
          <input type="text" v-else v-model="editItem.name" />
        </td>
        <td>
          <small>{{ item.desc }}</small>
        </td>
        <td>{{ item.price }}</td>
        <td>
          <button type="button" @click="decreaseStock(item.id)">-</button>
          {{ item.stock }}
          <button type="button" @click="increaseStock(item.id)">+</button>
        </td>
        <td>
          <button type="button" v-if="editItem.id !== item.id" @click="editItemName(item.id)">
            編輯
          </button>
          <div v-else>
            <button type="button" @click="confirmEdit">確認</button>
            <button type="button" @click="cancelEdit">取消</button>
          </div>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped></style>
