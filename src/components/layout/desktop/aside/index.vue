<script lang="ts" setup>
  import { useRoute } from 'vue-router'
  import { computed } from 'vue'
  import { ASIDE_ELEMENT_ID } from '/@/constants/element-anchor'
  import { isArticleDetail } from '/@/transforms/route'
  import AsideSearch from './search.vue'
  import AsideStatistic from './statistic.vue'
  import AsideArticle from './article.vue'
  import AsideTag from './tag.vue'
  import AsideAnchor from './anchor.vue'
  import AsideCalendar from './calendar.vue'

  const route = useRoute()
  const isArticlePage = computed(() => isArticleDetail(route.name))
</script>

<template>
  <aside :id="ASIDE_ELEMENT_ID" class="desktop-aside" v-disabled-wallflower>
    <div class="module">
      <aside-search />
    </div>
    <div class="module">
      <aside-statistic />
    </div>
    <div class="module">
      <aside-article />
    </div>
    <div class="module">
      <aside-calendar />
    </div>
    <div class="aside-sticky-box">
      <div class="module">
        <client-only v-if="isArticlePage">
          <aside-anchor class="sticky-module" />
        </client-only>
        <aside-tag class="sticky-module" v-else />
      </div>
    </div>
  </aside>
</template>

<style lang="scss" scoped>
  @use '/src/styles/base/variables' as *;
  @use '/src/styles/base/functions' as funs;
  @use '/src/styles/base/mixins' as mix;

  .desktop-aside {
    display: block;
    padding: 0;
    width: $aside-width;

    .module {
      margin-bottom: $gap-lg;
      @include mix.radius-box($radius-sm);
      @include mix.common-bg-module();

      .sticky-module {
        max-height: calc(100vh - 250px - #{$header-height + $gap-lg * 4});
      }
    }

    .aside-sticky-box {
      position: sticky;
      top: $header-height + $gap-lg;
      width: $aside-width;
    }
  }
</style>
