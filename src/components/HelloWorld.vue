<template>
  <div class='container' >
    <!-- form -->
    <div class="columns is-centered">
    <!-- <table >
      <tr>
        <td align='right'>Book Title</td><td> : <input type='text' v-model='Book.title'></td>
      </tr>
      <tr>
        <td align='right'>Book Author</td><td>: <input type='text' v-model='Book.author'></td>
      </tr>
        <tr>
          <td align='right'>Book Type</td><td>: <input type='text' v-model='Book.type'></td>
        </tr>
        <tr>
          <td align='right'>Price</td><td>: <input type='text' v-model='Book.price'></td>
        </tr>
    </table>
    <div class="columns is-centered"><button class="button is-success is-outlined" @click="add()">ลงทะเบียนหนังสือ</button></div> -->
    <div class="column is-6 box">
      <div class="columns">
        <div class="column is-4 ">
          <label class="title is-4 right">
            Book Title
          </label>
        </div>
        <div class="column is-8">
          <input type='text' v-model='Book.title' class="input">
        </div>
      </div>
      <div class="columns">
        <div class="column is-4">
          <label class="title is-4">
            Book Author
          </label>
        </div>
        <div class="column is-8">
          <input type='text' v-model='Book.author' class="input">
        </div>
      </div>
      <div class="columns">
        <div class="column is-4">
          <label class="title is-4">
            Book Type
          </label>
        </div>
        <div class="column is-8">
          <div class="select">
            <select v-model='Book.type'>
                <option>Education</option>
                <option>Novel</option>
                <option>Fashion</option>
              </select>
            </div>
        </div>
      </div>
      <div class="columns">
        <div class="column is-4">
          <label class="title is-4">
            Price
          </label>
        </div>
        <div class="column is-8">
          <input type='text' v-model='Book.price' class="input">
        </div>
      </div>
      <br>
      <div class="columns is-centered">
        <button class="button is-danger is-outlined is-large" @click="add()">ลงทะเบียนหนังสือ</button>
      </div>
      <br>
    </div>
  </div>
  <br>
  <div class="columns is-centered">
    <table class="table">
      <tr>
        <th>Title</th> <th>Type</th> <th>Price</th> <th>Author</th>
      </tr>
      <tr class="" v-for="book in Books">
        <td>{{book.title}}</td>
        <td>{{book.type}}</td>
        <td>{{book.price}}</td>
        <td>{{book.author}}</td>
        <td> <button type="button" name="button" class="button is-danger is-small" @click="del(book)">ลบ</button> </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import Firebase from 'firebase'
// Initialize Firebase
var config = {
  apiKey: 'AIzaSyDnMDoxHSK2KhHrTg4KG02vEnFDUunvYmA',
  authDomain: 'assignment-se.firebaseapp.com',
  databaseURL: 'https://assignment-se.firebaseio.com',
  projectId: 'assignment-se',
  storageBucket: 'assignment-se.appspot.com',
  messagingSenderId: '629128946105'
}
let app = Firebase.initializeApp(config)
let db = app.database()
let BooksRef = db.ref('Books')
export default {
  name: 'HelloWorld',
  firebase: {
    Books: BooksRef
  },
  data () {
    return {
      Book: {
        title: '',
        author: '',
        type: '',
        price: ''
      }
    }
  },
  methods: {
    add () {
      BooksRef.push(this.Book)
      this.Book.title = ''
      this.Book.author = ''
      this.Book.type = ''
      this.Book.price = ''
    },
    del (book) {
      BooksRef.child(book['.key']).remove()
    }
  }
}
</script>

<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
#fs{
  width:300px;
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
