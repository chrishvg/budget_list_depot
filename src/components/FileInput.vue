<template>
  <usecsv-button importerKey="your-importer-key">
    <p class="text-md-center">Types: txt | csv | html | xml</p>
  </usecsv-button>
  <v-file-input
    @change="handleFileUpload"
    color="deep-purple-accent-4"
    counter
    label="File input"
    placeholder="Select your file"
    prepend-icon="mdi-paperclip"
    variant="outlined"
    style="height: 100vh"
    accept=".csv"
    >
    <template v-slot:selection="{ fileNames }">
        <template v-for="(fileName) in fileNames" :key="fileName">
        <v-chip
            color="deep-purple-accent-4"
            label
            size="small"
            class="me-2"
        >
            {{ fileName }}
        </v-chip>
        </template>
    </template>
  </v-file-input>
</template>
<script>
export default {
  data() {
    return {
      cleanObject: {
        label: "",
        data: []
      }
    }
  },
  methods: {
    handleFileUpload(event) {
      const file = event.target.files[0]
      let dataArray = null
      const reader = new FileReader()
      reader.onload = () => {
        const csvData = reader.result
        switch(file.type) {
          case "text/csv":
            this.parseCSV(csvData)
              .then(dataArray => {
                this.$emit('listMaterials', dataArray)
              })
              .catch(error => {
                console.error(error)
              })
          break;
        }
          
        this.$emit('listMaterials', dataArray)
      }

      reader.readAsText(file)
    },

    parseCSV(csvData) {
      return new Promise((resolve, reject) => {
        let arrayData = []
        const lines = csvData.split('\n')
        const size = lines.length;
        if (size === 0) {
          reject("No data found in the uploaded CSV file")
        }
        let group = ''
        for (let i = 1; i < size; i++) {
          const lineArray = lines[i].trim().split(',');
          const line = lineArray.map(value => value.replaceAll('"', ''))
          //0 Id
          //6 Size
          //7 Description
          //8 Count
          //10 Unit
          //11 Price
          if (line[11] === '') {
            if (line[7] !== '') {
              arrayData.push({
                id: line[0],
                size: line[6],
                description: line[7],
                count: line[8],
                unit: line[10],
                group: group
              });
            } else {
              group = line[0];
            }
          }
        }

        resolve(arrayData)
      })
    }
  },
}
</script>