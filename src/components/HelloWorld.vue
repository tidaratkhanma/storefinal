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
</div>  <br><br><br>

<table class="table is-fullwidth" >
  <thead>
          <tr>
                <th scope="col">Name</th>
                <th scope="col">Number</th>
                <th scope="col">Price</th>
                <th scope="col"></th>
                <th scope="col">Update</th>
                <th scope="col">Delete</th>
            </tr>
  </thead>
  <tbody v-for =" (stock,key) in showstock"  >
    <tr  v-if = "sw !== key" >
      <td>  <img :src="stock.image"style="width: 100px; height: 100px;"></td>
      <td> </br> </br>{{stock.name}}</td>
      <td> </br></br> {{stock.number}}</td>
      <td> </br></br> {{stock.price}}</td>

      <td> </br></br><a class="button is-primary is-outlined" @click="swap(key)">Update</a> </td>
      <td> </br></br><a class="button is-primary is-outlined" @click="Delete(key)">Delete</a> </td>
   </tr>

      <tr  v-else >
        <td>  <input class="input is-focused" type="text"   v-model="stock.name" ></td>
        <td>   <input class="input is-focused" type="text"  v-model="stock.number" ></td>
        <td>  <input class="input is-focused" type="text"   v-model="stock.price" ></td>
        <td>
          <div class="file">
                <label class="file-label">
                <input class="file-input" type="file" name="resume"  @change="onFileChange($event.target.files[0])"required>  &nbsp; &nbsp; &nbsp; &nbsp;
                  <span class="file-cta">
                    <span class="file-icon">
                      <i class="fas fa-upload"></i>
                    </span>
                    <span class="file-label">
                      Choose a file…
                    </span>
                  </span>
                </label>
              </div>
        </td>
        <td> <a class="button is-primary is-outlined" @click="Update(key,stock.name,stock.number,stock.price)">Save</a> </td>
        <td> <a class="button is-primary is-outlined" @click="cancel()">Cancle</a> </td>
     </tr>
      </tbody>
</table>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      showstock: ''
    }
  },
  methods: {
    pullData: function () {
      let that = this
      firebase.database().ref('/stock/').once('value').then(function (snapshot) {
        that.showstock = snapshot.val()
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
