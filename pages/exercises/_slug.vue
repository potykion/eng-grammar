<template>
  <div>
    <h1>{{ exerciseInfo.topic }}</h1>
    <template v-for="(ex, exerciseIndex) in exercises">
      <exercise-item  :key="exerciseIndex" :ex="ex" :answer="keys[exerciseIndex]"></exercise-item>
      <hr>
    </template>
  </div>
</template>

<script lang="ts">
import {Vue, Component, Prop} from "nuxt-property-decorator";
import {Context} from "@nuxt/types";
import ExerciseItem from "~/components/exercise-item.vue";

@Component({
  components: {ExerciseItem},
  async asyncData({$content, params}: Context) {
    const grammarExercisesToc = await $content("exercises/grammar-exercises-toc").fetch();

    // const exercises = await $content(`exercises/${params.slug}`).fetch();
    const exercises = await $content("exercises").fetch();

    const keys = await $content("keys").fetch();

    return {grammarExercisesToc, exercises, keys};
  }
})
export default class ExercisePage extends Vue {
  grammarExercisesToc!: GrammarExercises.TocItem[];
  exercises!: GrammarExercises.Exercise[];
  keys!: GrammarExercises.Answer[];


  get exerciseInfo(): GrammarExercises.TocItem {
    return this.grammarExercisesToc.find(toc => toc.slug === this.$route.params.slug)!;
  }

}
</script>

<style scoped>

</style>
