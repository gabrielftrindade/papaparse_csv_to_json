<template>
  <div id="app">
    <div class="call-button-container">
      <button @click="onPickFile()">Exportar CSV</button>
      <input type="file" accept=".csv" style="display: none" ref="fileInput" @change="handleFileUpload( $event )"/>
    </div>
    <div class="call-button-container">
      <h1>Resposta:</h1>     
    </div>
    <div>
      <h5>{{resposta}}</h5>
    </div>
  </div>
</template>

<script>
  import Papa from 'papaparse'

  export default {
    name: 'App',
    data: () => ({
      file: null,
      content: [],
      resposta: ''
    }),
    methods: {
      onPickFile () {
        this.$refs.fileInput.click()
      },

      handleFileUpload (event) {
        this.file = event.target.files[0]
        console.log(this.file)
        this.parseFile()
      },

      parseFile () {
        Papa.parse(this.file, {
          header: true,
          skipEmptyLines: true,
          encoding: 'ISO-8859-1',
          complete: function (results) {
            this.content = results.data
            this.resposta = JSON.stringify(this.content)
          }.bind(this)
        })
      }
    }
  }
</script>

<style>
.call-button-container {
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 60px;
}
</style>
