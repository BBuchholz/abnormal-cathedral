<script>
// ALL OF THIS IS BEING ADAPTED FROM https://ourcodeworld.com/articles/read/106/how-to-choose-read-save-delete-or-create-a-file-with-electron-framework
// import { fs } from 'fs'
// import { remote } from 'remote'
import { dialog } from 'electron'

const props = defineProps({
  title: {
    type: String,
    default: 'CRUD STUFF',
  },
})

// const contentEditor = ref('')
const actualFile = ref('')

const selectFile = async () => {
  try {
    dialog.showOpenDialog((fileNames) => {
      if (fileNames !== undefined) {
        actualFile.value = fileNames[0]
        readFile(fileNames[0])
      }
    })
  }
  catch (error) {
    console.error(error)
  }
}
</script>

<template>
  <div>
    <div style="text-align:center;">
      <input v-model="actualFile" type="text" placeholder="Please select a file">
      <button style="margin-left: 20px" @click="selectFile">
        Select File
      </button>
    </div>
    <br><br>
    <textarea v-model="contentEditor" cols="60" rows="10" /><br><br>
    <button style="margin-left: 20px" @click="saveChanges">
      Save Changes
    </button>
    <button style="margin-left: 20px" @click="deleteFile">
      Delete file
    </button>
  </div>
  <hr>
  <div style="text-align:center;">
    <p>
      The file content will be the same as the editor.
    </p>
    <button style="margin-left: 20px" @click="createFile">
      Create a file
    </button>
  </div>
</template>
