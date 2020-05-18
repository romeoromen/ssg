<template>
  <div>
    <h2>{{item.title}}</h2>
    <template>
      <img :src="item.image.url">
    </template>
    <div v-html="$md.render(item.body)"></div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  async asyncData({params}) {
    const { data } = await axios.get(
      `https://wiz_uchida.microcms.io/api/v1/posts/${params.id}`,
      {
        headers: { "X-API-KEY": process.env.API_KEY }
      }
    );
    return {
      item: data
    };
  }
};
</script>
