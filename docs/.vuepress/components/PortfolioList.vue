<template>
  <div class="post-container">
    <router-link v-for="page in pages" :to="page.path">
      <div class="post-card">
        <!--<img class="article-image" src={{ page.frontmatter.heroimage}} />-->
        <div class="page-detail">
          <h3 class="page-title">{{ page.title }}</h3>
          <p class="page-description">{{ page.frontmatter.description }}</p>
        </div>
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
      if (page.frontmatter.type === 'portfolio') {
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
  width: 100%;
}
.post-card {
  width: 350px;
  height: 150px;
  margin: 10px;
  border: 1px solid #ccc;
  border-radius: 3px;
  padding: 10px;
  display: flex;
  align-items: center;
}
.article-image {
  height: 100%;
}
.description {
  width: 100%;
  display: flex;
  justify-content: center;
}
</style>