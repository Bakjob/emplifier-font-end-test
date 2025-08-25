<template>
  <div class="cv-upload">
    <h2>Upload your CV</h2>
    <input type="file" @change="onFileChange" />
    <button @click="submitCv" :disabled="!file">Send CV</button>
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
  if (!file.value) return

  const formData = new FormData()
  formData.append('cv', file.value)

  try {
    const res = await fetch('https://localhost:8000/upload-cv', {
      method: 'POST',
      body: formData
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

