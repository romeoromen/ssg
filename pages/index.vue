<template>
  <div class="container">
    <logo />
    <div class="items">
      <!-- itemsをforでまわし、itemにそれぞれのデータが入ります。 -->
      <div v-for="item in items" :key="item" class="item">
        <nuxt-link :to="'careers/' + item.id">
          <h2>
            {{ item.name }}
          </h2>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import axios from 'axios'
export default {
  components: {
    Logo
  },
  data () {
    return {
      items: []
    }
  },
  async asyncData() {
    const { data } = await axios.get('https://wiz_uchida.microcms.io/api/v1/careers', {
      headers: { 'X-API-KEY': process.env.API_KEY }
    })
    return {
      items: data.contents
    }
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
.items {
  width: 100%;
  display: flex;
  justify-content: center;
}
.item {
  width: calc(50% - 20px);
}
</style>
