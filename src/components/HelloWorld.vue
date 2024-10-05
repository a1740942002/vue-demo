<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

defineProps({
  msg: String
})

const post = ref({}) // 使用 ref 來追蹤 post 的狀態
const message = ref('')

onMounted(async () => {
  try {
    const response = await axios.get(
      'https://jsonplaceholder.typicode.com/posts/1'
    )
    post.value = response.data // 更新 post 的值
  } catch (error) {
    console.error('Error fetching post:', error)
  }
})

const handleSubmit = () => {
  sendMessage(message.value)
}
</script>

<template>
  <div>
    <div class="post">
      <p>{{ post.title }}</p>
      <p>{{ post.body }}</p>
    </div>
    <input type="text" :value="message" @input="updateMessage" />
    <button @click="handleSubmit">送出</button>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
