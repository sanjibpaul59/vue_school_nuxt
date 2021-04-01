<template>
  <div class="container">
      <article>
          <h1 class="title"> {{blog.title}} </h1>
          <h2> {{blog.id}} </h2>
          <p> {{blog.content}} </p>
      </article>

      <aside>
          <h3>Blogs you might like</h3>
          <ul>
              <li v-for="related in relatedBlogs" :key="related">
                  <nuxt-link :to="{name: 'blogs-id', params: {id: related.id} }">
                      {{related.title}}
                  </nuxt-link>
              </li>
          </ul>
      </aside>
  </div>
</template>

<script>
export default {
    data(){
        return{
            id: this.$route.params.id,
        }
    },
    computed: {
        blog(){
            return this.$store.state.blogs.all.find(blog => blog.id === this.id)
        },
        relatedBlogs(){
            return this.$store.state.blogs.all.filter(blog => blog.id != this.id)
        }
    },
    head(){
        return{
            title: this.blog.title,
            meta: [
                {name: 'twitter:title', content: this.blog.title},
                {
                    name: 'twitter:description',
                    content: this.blog.content
                }
            ]
        }
    }

}
</script>

<style scoped>
.container{
    display: flex;
    justify-content: space-between;
    line-height: 1.5;
}
article *{
    margin-bottom: 1rem;
}
aside {
    min-width: 280px;
    max-width: 280px;
}
.title{
    font-size: 2rem;
}

</style>