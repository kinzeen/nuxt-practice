<template>
  <article class="section">
    <section class="header">
      <section class="hero is-light">
        <div class="hero-body">
          <div v-for="tag in doc.tags" :key="tag.index">
            <!-- TODO:タグごとのページ一覧を表示 <a :href="'/tags/' + tag"> -->
            <a href="#">
              <span v-if="tag === 'tech'" class="tag is-info">{{ tag }}</span>
              <span v-else-if="tag === 'note'" class="tag is-primary">
                {{ tag }}
              </span>
              <span v-else class="tag is-Light">{{ tag }}</span>
            </a>
          </div>
          <p class="title">
            {{ doc.title }}
          </p>
          <p>作成日：{{ doc.createdAt }}</p>
        </div>
      </section>
      <div class="media">
        <div class="media-left">
          <figure class="image is-48x48">
            <img :src="doc.top_image" />
          </figure>
        </div>
      </div>
    </section>
    <div class="content">
      <section class="section">
        <nuxt-content :document="doc" />
      </section>
    </div>
  </article>
</template>
<script>
export default {
  async asyncData({ $content, params }) {
    const doc = await $content('articles', params.slug || 'index').fetch()
    return { doc }
  },
}
</script>
