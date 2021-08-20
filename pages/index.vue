<template>
  <div>
    <h1>Contents</h1>
    <ul>
      <li v-for="toc in grammarExercisesToc">
        <nuxt-link :to="`/exercises/${toc.slug}`" >{{ toc.topic }}</nuxt-link>
      </li>

    </ul>
  </div>
</template>

<script lang="ts">

import {Component, Vue} from "nuxt-property-decorator";


@Component({
  layout: "default",
  async asyncData({$content}) {
    const grammarExercisesToc = await $content("exercises/grammar-exercises-toc").fetch();
    return {grammarExercisesToc};
  }
})
export default class IndexPage extends Vue {
  grammarExercisesToc!: GrammarExercises.TocItem[];
}

</script>

<style scoped>

</style>
