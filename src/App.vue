<template>
  <div class='dbTable'>
    <table>
      <tbody>
        <tr v-for="(item) in this.data" v-bind:key="item.authorName">
          <td>{{ item.date }}:</td>
          <td>{{ item.authorName }}:</td>
          <td>{{ item.authorUrl }}:</td>
          <td>{{ item.content }}:</td>
          <!-- <td>{{ value }}</td> -->
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'app',
  data () {
    return {
      data: []
    }
  },
  mounted () {
    return new Promise((resolve, reject) => {
      axios({ url: 'http://localhost:3000/data', method: 'GET' })
        .then(resp => {
          this.data = resp.data

          for (let i = 0; i < this.data.length; i++) {
            const dateInData = new Date(Date.parse(this.data[i].date))
            this.data[i].date = dateInData.toLocaleString()
            resolve(resp)
          }
        })
        .catch(err => {
          console.log(err)
          reject(err)
        })
    })
  }
}

</script>

<style lang="scss">
// #app {
// font-family: Avenir, Helvetica, Arial, sans-serif;
// -webkit-font-smoothing: antialiased;
// -moz-osx-font-smoothing: grayscale;
// text-align: center;
// color: #2c3e50;
// }
</style>
