<template>
  <div class="hello">
    <div class="tabs is-toggle  is-right">
  <ul>
    <router-link to="/">
    <li>
      <a>
        <span class="icon is-small"><i class="fas fa-film" aria-hidden="true"></i></span>
        <span>Order</span>
      </a>
    </li>
    </router-link>
    <router-link to="/Stock">
    <li>
      <a>
        <span class="icon is-small"><i class="far fa-file-alt" aria-hidden="true"></i></span>
        <span>Stock</span>
      </a>
    </li>
    </router-link>
  </ul>
</div>



<div class="columns">
  <div class="column"></div>
  <div class="column is-two-thirds">


  </div>
  <div class="column"></div>
</div>



  </div>
</template>

<script>
// import firebase from 'firebase'
// var config = {
//     apiKey: 'AIzaSyDgYgfnjiyffPJzD4Pqjt3f-nXfTGW6_Ko',
//     authDomain: 'store-a7427.firebaseapp.com',
//     databaseURL: 'https://store-a7427.firebaseio.com',
//     projectId: 'store-a7427',
//     storageBucket: 'store-a7427.appspot.com',
//     messagingSenderId: '356296828842'
//   }
//   firebase.initializeApp(config)
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    pullData: function () {
      let that = this
      firebase.database().ref('/student/').once('value').then(function (snapshot) {
        that.showstudent = snapshot.val()
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
