<template>
  <div>
    <h2>キャリア</h2>
    <div v-for="item in items" :key="item" class="item-box">
      <nuxt-link :to="'posts/' + item.id">
        <h2>
          {{ item.title }}
        </h2>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {

  data() {
    return {
      items: []
    };
  },

  async asyncData({params}) {
    const { data } = await axios.get(
      `https://wiz_uchida.microcms.io/api/v1/posts?filters=careers[equals]${params.id}`,
      {
        headers: { 'X-API-KEY': process.env.API_KEY }
      }
    )
    return {
      items: data.contents
    }
  },
}
</script>
