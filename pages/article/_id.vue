<template>
  <div>
      <h1>{{ item.title }}</h1>
      <div class="line-numbers language-js" v-html="$md.render(item.body)"></div>
      <nuxt-link :to="'/'">
        <h2>戻る</h2>
      </nuxt-link>
  </div>
</template>

<script>
import axios from "axios";
import Prism from '~/plugins/prism.js'

export default {
  data() {
    return {
      items: []
    };
  },
  mounted() {
    Prism.highlightAll()
  },
  async asyncData({ params }) {
    const { data } = await axios.get(
      `https://tomtomblog.microcms.io/api/v1/blog/${params.id}`,
      {
        headers: { "X-MICROCMS-API-KEY": process.env.API_KEY }
      }
    );
    return {
      item: data
    };
  },

};
</script>
<style>
  h1 {
    display: block;
    font-size: 3em;
    text-align: center;
    font-weight: bold;
    border-top: solid 3px #364e96;
    border-bottom: solid 3px #364e96;
  }
</style>
