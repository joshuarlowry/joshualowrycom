<template>
  <div class="post-container">
    <div v-for="page in pages" class="post-card">
        <div class="page-detail">
          <h3 class="page-title">
            <router-link :to="page.path">{{ page.title }}</router-link>
          </h3>
          <p class="page-description">{{ page.frontmatter.description }}</p>
          <p class="page-published">{{ page.frontmatter.date }}</p>
        </div>
    </div>
  </div>
</template>
<script>
export default {
  computed: {
      pages() {
        return this.$site.pages
            .filter(x => x.path.startsWith('/Legacy/'))
            .sort((a,b) => new Date(a.frontmatter.date) - new Date(b.frontmatter.date));
      }
  }
}
</script>

<style scoped>
.post-container {
    display: flex;
    flex-wrap: wrap-reverse;
    justify-content: center;
    width: 100%;
}
.post-card {
    margin: 1ch;
    flex-grow: 1;
    min-width: 375px;
    flex-basis: min-content;
    padding-left: 2ch;
    padding-right: 2ch;
    border: 1px solid #ccc;
    border-radius: 3px;
}


</style>