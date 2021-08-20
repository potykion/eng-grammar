<template>
  <div class="border rounded p-2 mb-2">
    <ul>
      <li class="flex space-x-2">
        <!-- ~135 вмещается на одну строку => doneTask.length / 135 + 1 = кол-во строк, занимаемое инпутом -->
        <textarea ref="task-textarea" :rows="doneTask.length / 135 + 1" class="w-4/5 flex-grow" v-model="doneTask"/>

<!--        <button v-if="!showAnswer" @click="showAnswer = !showAnswer">✔️</button>-->
      </li>
      <li v-if="showAnswer" :class="['italic', doneTask === answer ? 'text-green-400' : 'text-red-400' ]">
        {{ answer }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import {Vue, Component, Prop} from "nuxt-property-decorator";
import {Context} from "@nuxt/types";

@Component({})
export default class TaskItem extends Vue {
  @Prop() task!: string;
  @Prop() answer!: string;

  doneTask = this.task;

  @Prop({default: false}) showAnswer!: boolean;

  // mounted() {
  //
  //
  //   const taskTextarea = this.$refs["task-textarea"] as HTMLElement;
  //
  //
  //
  //   taskTextarea.setAttribute(
  //     "style",
  //     "height:24px;overflow-y:hidden;"
  //   );
  //   taskTextarea.addEventListener(
  //     "input",
  //     function () {
  //       this.style.height = "auto";
  //       this.style.height = (this.scrollHeight) + "px";
  //     },
  //     false
  //   );
  // }
}
</script>

<style scoped lang="scss">

</style>
