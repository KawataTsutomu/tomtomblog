<template>
  <div>
    <h1>test-blog</h1>
    <div v-for="(item,key) in items" :key="key">
       <h2>{{ item.title }}</h2>
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
  // 記事一覧のJSONをmicroCMSより取得
  async asyncData() {
    const { data } = await axios.get(
      "https://tomtomblog.microcms.io/api/v1/article",
      {
        headers: { "X-MICROCMS-API-KEY": process.env.API_KEY }
      }
    );
    return {
      items: data.contents
    };
  }
}
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
  h2 {
    display: block;
    font-size: 1.6em;
    text-align: center;
    font-weight: bold;
    border: solid #ddd;
    border-width: 0 0 1px 0;
  }
</style>
