# Papaparse

>https://gist.github.com/gabrielftrindade/7da84c9622ad89f378c9337cd6361f20

<img width="813" alt="image" src="https://user-images.githubusercontent.com/70534046/175168032-55d0908a-4cd6-47dd-96c6-7d8d02de1d1c.png">

## 1. Install Papaparse
```
npm install papaparse --save
```

## 2. Import Papaparse
```
import Papa from 'papaparse'
```

## 3. Criar o botão
```javascript
<button @click="onPickFile()">Exportar CSV</button>
<input type="file" accept=".csv" style="display: none" ref="fileInput" @change="handleFileUpload( $event )"/>
```
## 4. Criar as funções
```javascript
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
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```
