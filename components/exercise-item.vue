<template>
  <div>
    <div v-if="ex.rules" class="italic whitespace-pre-line">{{ ex.rules }}</div>

    <details :open="exerciseDone">
      <summary>
        <div class="inline-block" style="width: calc(100% - 16px)">
          <div class=" flex items-center justify-between">
            <h2 :class="['inline-block',  showAnswer ? 'line-through' : '']">
              Упражнение {{ ex.exercise_number }}
            </h2>
            <button @click="toggleExercise(ex.exercise_number)">
              <span v-if="!showAnswer">✔️</span>
              <span v-else>🔁</span>
            </button>
          </div>
        </div>
      </summary>

      <div>
        <div class="py-1 italic">{{ ex.exercise_text }}</div>

        <template v-for="(task, taskIndex) in ex.tasks">
          <task-item :key="taskIndex" :task="task" :answer="answer.tasks[taskIndex]"
                     :show-answer="showAnswer"/>
        </template>

      </div>

    </details>


  </div>
</template>

<script lang="ts">
import {Vue, Component, Prop} from "nuxt-property-decorator";
import {Context} from "@nuxt/types";
import {DoneExerciseRepo} from "~/logic/db";

@Component({})
export default class ExerciseItem
  extends Vue {
  @Prop() ex!: GrammarExercises.Exercise;
  @Prop() answer!: GrammarExercises.Exercise;
  showAnswer = false;
  exerciseDone = false;

  repo!: DoneExerciseRepo;

  toggleExercise(exerciseNumber: number) {
    if (!this.showAnswer) {
      this.showAnswer = true;
      this.repo.doExercise(exerciseNumber);
    } else {
      this.showAnswer = false;
      this.repo.undoExercise(exerciseNumber);
    }
  }

  mounted() {
    this.repo = new DoneExerciseRepo(localStorage);
    this.showAnswer = this.repo.isExerciseDone(this.ex.exercise_number);
    this.exerciseDone = !this.showAnswer;
  }
}
</script>

<style scoped lang="scss">

</style>
