<template>
  <input type="file" ref="file" @change="handleFileUpload" />
  <button @click="submitFile">Submit</button>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      file: ''
    }
  },
  methods: {
    handleFileUpload() {
      this.file = this.$refs.file.files[0]
    },
    submitFile() {
      let formData = new FormData()
      formData.append('file', this.file)

      this.axios.post('http://localhost:8888/upload',
        formData,
        {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        }
      ).then(function(response) {
        console.log(response)
        console.log('Success')
      }).catch(function(error) {
        console.log(error)
        console.log('Failure')
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
