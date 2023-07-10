<template>
  <div class='dbTable'>
    <table>
      <tbody>
        <tr v-for="(item) in this.data" v-bind:key="item.authorName">
          <td>{{ item.authorName }}:</td>
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
      // chengedDate: []
    }
  },
  // components: {},
  created () {
    return new Promise((resolve, reject) => {
      axios({ url: 'http://localhost:3000/data', method: 'GET' })
        .then(resp => {
          console.log('mounted')
          this.data = resp.data
          console.log(this.data[0])
          // this.chengedDate =

          // for (const item in this.data) {
          //   item.date = item.date.toLocaleDateString('ru-RU', { hour: '2-digit', minute: '2-digit' })
          // }
          // console.log(this.data)

          // for ( let item in this.data) {

          // }
          // this.changeDate()
          resolve(resp)
        })
        .catch(err => {
          reject(err)
        })
    })
  },
  mounted () {
    for (const item in this.data) {
      item.date = item.date.toLocaleDateString('ru-RU', { hour: '2-digit', minute: '2-digit' })
    }
    console.log('created')
    console.log(this.data[0])
  }

  // methods: {
  //   changeDate () {
  //     for (const item in this.data) {
  //       item.date = item.date.toLocaleDateString('ru-RU', { hour: '2-digit', minute: '2-digit' })
  //     }
  //     console.log(this.data)
  //     // this.data
  //   }
  // }
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
