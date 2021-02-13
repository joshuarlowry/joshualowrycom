<template>
  <div class="post-container">
    <router-link v-for="page in pages" :to="page.path" class="post-card">
        <div class="page-detail">
          <h3 class="page-title">{{ page.title }}</h3>
          <p class="page-description">{{ page.frontmatter.description }}</p>
        </div>
    </router-link>
  </div>
</template>
<script>
export default {
  data() {
    return {
      pages: []
    }
  },
  mounted() {
    this.$site.pages.forEach(page => {
      if (page.path.startsWith('/Projects/')) {
        this.pages.push(page)
      }
    })
  }
}
</script>

<style scoped>
.post-container {
    display: flex;
    flex-wrap: wrap;
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