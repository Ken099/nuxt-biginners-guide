<template>
  <section class="container">
    <h3>Nuxt.js のタグがつけられた投稿一覧</h3>
    <ul>
      <li
        v-for="item in items"
        v-bind:key="item.id"
      >
        <h4>
          <span>{{item.title}}</span>
          <small>by {{item.user.id}}</small>
          <small>
            <span>by </span>
            <nuxt-link :to="`/users/${item.user.id}`">
              {{item.user.id}}
            </nuxt-link>
          </small>
        </h4>
        <div>{{item.body.slice(0,130)}}……</div>
        <p><a v-bind:href="item.url">{{item.url}}</a></p>
      </li>
    </ul>
  </section>
</template>

<script>
import AppLogo from "~/components/AppLogo.vue";

export default {
  components: {
    AppLogo
  },

  async asyncData({ app }) {
    const items = await app.$axios.$get(
      "https://qiita.com/api/v2/items?query=tag:nuxt.js"
    );
    return {
      items
    };
  }
};
</script>

<style>
.container {
  min-height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
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
</style>

