<script setup>
import { ref } from 'vue'

const message = ref('')

const submitMessage = () => {
  const value = message.value.trim()

  if (!value) {
    window.alert('Please enter text before submitting.')
    return
  }

  window.alert(value)
}
</script>

<template>
  <section class="card form-card">
    <label for="user-message">Enter a message</label>
    <input
      id="user-message"
      v-model="message"
      type="text"
      placeholder="Type something..."
    />
    <button type="button" @click="submitMessage">Submit</button>
  </section>
</template>
