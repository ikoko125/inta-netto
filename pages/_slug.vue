<template>
 <article>
   <h1>{{article.title}}</h1>
   <p>{{article.date}}</p>
   <nuxt-content :document="article" />
 </article>
</template>
<script>
export default {
 async asyncData ({ $content, params }) {
   const article = await $content('article', params.slug || 'index').fetch()
   return { article }
 }
}
</script>