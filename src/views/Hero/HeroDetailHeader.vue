<template>
  <v-row class="hero-detail-header my-5">
    <v-col cols="12">

      <div class="d-flex justify-content-center mv-3">
        <div class="hero-detail-avatar" :class="heroClass"></div>
      </div>

      <div class="text-center">

        <h1 v-diablo:bone class="text-truncate">{{ detail.name }}</h1>

        <div class="text-monospace">

          <small>
            <span>{{ detail.level }}</span>

            <span class="text-info" v-if="detail.paragonLevel">
              <span class="text-white"> · </span>
              ({{ detail.paragonLevel }})
            </span>

            <span> · {{classToName(detail.classSlug)}}</span>

            <span v-if="detail.seasonal" class="text-success"> · Seasonal </span>

            <span v-if="detail.hardcore" class="text-danger"> · Hardcore </span>

          </small>

          <div>
            <small class="text-muted">
              Season created:
            </small>
            <span class="p-1 bg-secondary rounded">{{ detail.seasonCreated }}</span>
          </div>

        </div>

        <hr>

      </div>

    </v-col>

  </v-row>
</template>

<script>
import heroName from '@/mixins/heroName'
export default {
  name: 'HeroDetailHeader',
  mixins: [heroName],
  props: {
    detail: {
      type: Object,
      required: true
    }
  },
  computed: {
    heroClass () {
      const gender = this.detail.gender === 0 ? 'male' : 'female'
      return `hero-${this.detail.classSlug} ${gender}`
    }
  }
}
</script>

<style lang="stylus" scoped>
  .hero-detail-avatar
    width 138px
    height 105px
    background-size 280px
  .text-bone
    color #e8dcc2
</style>
