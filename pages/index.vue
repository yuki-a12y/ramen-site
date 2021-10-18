	
<template>
  <ul>
    <li v-for="article in blog" :key="article.slug">
      <nuxt-link :to="'/blog/' + article.slug">
        <time :datetime="article.createdAt">
          {{ $dateFns.format(new Date(article.createdAt), 'yyyy/MM/dd') }}
        </time>
        <p>{{ article.title }}</p>
      </nuxt-link>
    </li>
  </ul>
</template>
 
<script>
export default {
  async asyncData ({ $content }) {
    // 記事を全て取得（作成日で降順にソート）
    const blog = await $content('blog').sortBy('createdAt', 'desc').fetch()
    return {
      blog
    }
  }
}
</script>