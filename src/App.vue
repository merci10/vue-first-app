<template>
  <div id="app">
    <MyHeader></MyHeader>
    <p v-if="msg.length > 0">
      {{ msg }}
    </p>
    <p v-else>
      no text
    </p>
    <input type="text" v-model="msg">
    <button type="button" @click="clear()">clear</button>
  </div>
</template>

<script>
import MyHeader from './components/MyHeader'

export default {
  components: {
    MyHeader
  },
  data() {
    return {
      msg: 'Hello World!'
    }
  },
  methods: {
    clear() {
      this.msg = ''
    }
  },
  created() {
    fetch('http://www.geonames.org/postalCodeLookupJSON?postalcode=104-0045&country=JP')
    .then(response => {
      console.log(response)
      return response.json()
    })
    .then(json => {
      console.log(json)
      this.msg = json.postalcodes[0].placeName
    })
    .catch(() => {
    });
  }
}
</script>