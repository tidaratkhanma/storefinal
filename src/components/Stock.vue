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
      <table>
        <tr>
          <td> <input class="input is-focused" type="text" placeholder="ชื่อสินค้า"  v-model="data.name" ></td>  &nbsp; &nbsp; &nbsp; &nbsp;
          <td> <input class="input is-focused" type="text" placeholder="จำนวน"  v-model="data.number"></td>&nbsp; &nbsp; &nbsp; &nbsp;
          <td> <input class="input is-focused" type="text" placeholder="ราคา"  v-model="data.price"></td> &nbsp; &nbsp; &nbsp; &nbsp;
          <td> <a class="button is-primary is-outlined" @click="insert()">+ADD</a> </td>
        </tr>
      </table>
    </div>
  <div class="column"></div>
</div>

<img width="25%" src="../assets/store.png"> </br>
<div class="columns">
  <div class="column"></div>
      <table class="table is-fullwidth" >
        <thead>
                <tr>
                      <th scope="col">Name</th>
                      <th scope="col">Number</th>
                      <th scope="col">Price</th>
                      <th scope="col">Update</th>
                      <th scope="col">Delete</th>
                  </tr>
        </thead>
        <tbody v-for =" (stock,key) in showstock"  >
          <tr  v-if = "sw !== key" >
            <td> {{stock.name}}</td>
            <td>  {{stock.number}}</td>
            <td>  {{stock.price}}</td>
            <td> <a class="button is-primary is-outlined" @click="swap(key)">Update</a> </td>
            <td> <a class="button is-primary is-outlined" @click="Delete(key)">Delete</a> </td>
         </tr>

            <tr  v-else >
              <td>  <input class="input is-focused" type="text"   v-model="stock.name" ></td>
              <td>   <input class="input is-focused" type="text"  v-model="stock.number" ></td>
              <td>  <input class="input is-focused" type="text"   v-model="stock.price" ></td>
              <td> <a class="button is-primary is-outlined" @click="Update(key,stock.name,stock.number,stock.price)">Save</a> </td>
              <td> <a class="button is-primary is-outlined" @click="cancle(key)">Cancle</a> </td>
           </tr>
            </tbody>
      </table>

    </div>
  <div class="column"></div>
</div>

  </div>
</template>

<script>
import firebase from 'firebase'
var config = {
  apiKey: 'AIzaSyDgYgfnjiyffPJzD4Pqjt3f-nXfTGW6_Ko',
  authDomain: 'store-a7427.firebaseapp.com',
  databaseURL: 'https://store-a7427.firebaseio.com',
  projectId: 'store-a7427',
  storageBucket: 'store-a7427.appspot.com',
  messagingSenderId: '356296828842'
  }
  firebase.initializeApp(config)
export default {
  name: 'HelloWorld',
  data () {
    return {
      data: {
        name: '',
        number: '',
        price: ''
      },
      showstock: '',
      sw: ''
    }
  },
  created: function () {
    this.pullData()
  },
  methods: {
    pullData: function () {
      let that = this
      firebase.database().ref('/stock/').once('value').then(function (snapshot) {
        that.showstock = snapshot.val()
      })
    },
     insert () {
      firebase.database().ref('stock').push(this.data)
      this.data.name = ''
      this.data.number = ''
      this.data.price = ''
      this.pullData()
    },
    Update (key, name, number, price) {
      firebase.database().ref('/stock/').child(key).update({
        name: name,
        number: number,
        price: price
      })
      this.pullData()
      this.checkEdit = ''
      this.sw = 'update'
    },
    Delete (key) {
      firebase.database().ref('stock').child(key).remove()
      this.pullData()
    },
    swap: function (key) {
      this.sw = key
    },
    cancel () {
      this.sw = ''
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
