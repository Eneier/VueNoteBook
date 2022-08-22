<template>
  <div class="container" id="nav">
    <!--    <link type="text/css" rel="stylesheet" href="//unpkg.com/bootstrap/dist/css/bootstrap.min.css"/>-->
    <!--    <link type="text/css" rel="stylesheet" href="//unpkg.com/bootstrap-vue@latest/dist/bootstrap-vue.css"/>-->
    <router-link to="/">Home</router-link>
    |
    <router-link to="/about">About</router-link>
    <br><br>
    <div class="card">
      <h1>{{ title }}</h1>
      <div class="form-control">
        <input
            type="text"
            :placeholder="myPlaceHolder"
            v-model="inputValue"
            @keypress.enter="addNotes"
        />
      </div>
      <div>
        <button class="btn" @click="addNotes">New note</button>
      </div>
      <ul class="list" v-if="notes.length !== 0">
        <li class="list-item" v-for="(note, i) in notes">
          {{ note }}
          <div>
            <button class="btn danger" @click="removeNotes(i)"> Delete</button>
          </div>
        </li>
        <hr/>
        <li class="list-item">
          <strong>Total notes: {{ total }} </strong>
        </li>
      </ul>
      <div v-else="notes.length === 0">
        <hr/>
        There is no notes. Add please
      </div>
    </div>

  </div>
  <router-view/>
</template>

<script>

export default {
  data() {
    return {
      title: 'Notebook List',
      myPlaceHolder: 'enter note title',
      inputValue: '',
      notes: ['Note 1', 'Note 2'],
    }
  },
  computed: {
    total() {
      console.log('total');
      return this.notes.length;
    },
    // headStyle() {
    //   return {
    //     color: this.inputValue.length > 5 ? 'darkred' : 'darkblue',
    //     fontSize: this.inputValue.length > 5 ? '40px' : '20px',
    //   }
    // }
  },
  watch: {
    inputValue(value) {
      (value.length > 50) ? this.inputValue = '' : this.inputValue;
    }
  },
  methods: {
    // inputChangeHandler(event) {
    //   this.inputValue = event.target.value;
    // },
    addNotes() {
      if (this.inputValue !== '') {
        this.notes.push(this.inputValue);
        this.inputValue = ''
      }
    },
    removeNotes(i) {
      this.notes.splice(i, 1);
    },
  }
}

</script>

<style src="./styles/main.css">

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #42b983;
  background: #2c3e50;
}


#nav {
  padding: 30px;


}

#nav a {
  font-weight: bold;
  color: #000000;

}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
