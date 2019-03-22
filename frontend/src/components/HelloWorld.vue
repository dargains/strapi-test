<template>
  <div class="hello">
    <h1>Strapi test</h1>
    <ul>
      <ImageItem v-for="image in images" :key="image.title" :title="image.title" :description="image.description" :source="image.image.url"/>
    </ul>
  </div>
</template>

<script>
import ImageItem from './ImageItem';
import Axios from 'axios';
const apiUrl = process.env === 'production' ? 'https://strapi-test.azurewebsites.net/' : 'http://localhost:1337';
export default {
  name: 'HelloWorld',
  components: {
    ImageItem
  },
  mounted() {
    Axios(`${apiUrl}/images`).then(response => {
      response.data.forEach(item => {
        item.image.url = `${apiUrl}${item.image.url}`
      });
      this.$store.commit('writeImages', response.data);
    });
  },
  computed: {
    images() {
      return this.$store.state.images;
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
li + li {
  margin-top: 1px solid lightgrey;
}
a {
  color: #42b983;
}
</style>
