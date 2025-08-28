<template>
  <div class="cv-upload">
    <button @click="submitCv">Send CV</button>
  </div>
</template>

<script setup>
// import composition API helpers
import { ref } from 'vue'

// hold the file
const file = ref(null)

// triggered when user picks a file
function onFileChange(event) {
  file.value = event.target.files[0]
}

// submit file to your API
async function submitCv() {
  console.log('submitting cv')

  try {
    const res = await fetch('http://localhost:8000/upload-cv', {
      method: 'POST',
    })

    if (!res.ok) {
      throw new Error('Failed to upload CV')
    }

    const data = await res.json()
    console.log('Upload successful:', data)
  } catch (err) {
    console.error('Error uploading CV:', err)
  }
}
</script>

<style scoped>
.cv-upload {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  max-width: 300px;
}
</style>

