<template>
  <div>
    <div v-if="ex.rules"  class="italic whitespace-pre-line">{{ ex.rules }}</div>

    <div class="flex items-center justify-between">
      <h2>
        Упражнение {{ ex.exercise_number }}
      </h2>
      <button @click="showAnswer = !showAnswer">✔️</button>
    </div>

    <div class="py-1 italic">{{ ex.exercise_text }}</div>
    <ul>
      <template v-for="(task, taskIndex) in ex.tasks">
        <task-item :key="taskIndex" :task="task" :answer="answer.tasks[taskIndex]"
                   :show-answer="showAnswer"/>
      </template>
    </ul>

  </div>
</template>

<script lang="ts">
import {Vue, Component, Prop} from "nuxt-property-decorator";
import {Context} from "@nuxt/types";

@Component({})
export default class ExerciseItem
  extends Vue {
  @Prop() ex!: GrammarExercises.Exercise;
  @Prop() answer!: GrammarExercises.Exercise;
  showAnswer = false;

}
</script>

<style scoped lang="scss">

</style>
