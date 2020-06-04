<template>
  <div class="hello">
    <ul>
      <li v-for="car of cars" v-bind:key="car.id">
        <img :src="car.acf.photo" alt />
        <h2>{{ car.title.rendered}}</h2>
        <p class="container" v-html="car.content.rendered"></p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      cars: []
    };
  },
  created: function() {
    this.$http.get("wp/v2/cars").then(
      response => {
        this.cars = response.data;
      },
      error => {
        alert(error);
      }
    );
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-direction: column;
}
li {
  display: inline-block;
  margin: 0 10px;
}
li img {
  width: 600px;
  margin: 0 auto;
}
a {
  color: #42b983;
}
.container {
  width: 600px;
  margin: 0 auto 60px auto;
}
</style>
