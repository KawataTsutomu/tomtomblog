<template>
  <v-app>
    <Header />
    <v-main>
      <v-container>
        <v-row>
          <v-col v-for="content in contents " :key="content.id">
            <v-card class="mx-auto" width="content.ogimage.width" height="content.ogimage.height">
              <v-img
                class="white--text align-end"
                height="200px"
                src="content.ogimage.url"
              >
              </v-img>
              <!-- 記事タイトル -->
              <nuxt-link :to="'article/' + content.id">
                <h2>{{ content.title }}</h2>
              </nuxt-link>
              <!-- タグ -->
              <div></div>
              <!-- 作成日 -->
              <div></div>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  // 記事一覧のJSONをmicroCMSより取得
  async asyncData() {
    const { data } = await axios.get(
      "https://tomtomblog.microcms.io/api/v1/blog",
      {
        headers: { "X-MICROCMS-API-KEY": process.env.API_KEY }
      }
    )
    return data
  },
}

</script>

<style>
  img {
      width: 160px;
      margin-top: 10px;
    }


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
