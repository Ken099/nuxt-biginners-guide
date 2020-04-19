<template>
  <section class="container">
    <h3>{{user.id}}</h3>
    <img
      :src="user.profile_image_url"
      width="120"
      :alt="user.id"
    >
    <p>{{user.descriptiion || "No description"}}</p>
    <p>
      <nuxt-link to="/">トップへ戻る</nuxt-link>
    </p>
    <h3>{{user.id}}の投稿一覧</h3>
    <ul>
      <li
        v-for="item in items"
        :key="item.id"
      >
        <h4>{{item.title}}</h4>
        <div>{{item.body.slice(0,130)}}...</div>
        <p><a
            :href="item.url"
            target="_blank"
            rel="noopener noreferrer"
          > {{item.url}} </a></p>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  async asyncData({ route, app }) {
    console.log(route);
    const user = await app.$axios.$get(
      `https://qiita.com/api/v2/users/${route.params.id}`
    );
    const items = await app.$axios.$get(
      `https://qiita.com/api/v2/items?query=user:${route.params.id}`
    );
    return {
      user,
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

