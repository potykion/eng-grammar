<template>
  <li class="py-1">
    <ul>
      <li class="flex">
        <textarea ref="task-textarea" rows="1" class="w-4/5 flex-grow" v-model="doneTask"/>
        <button v-if="!showAnswer" @click="showAnswer = !showAnswer">✔️</button>
      </li>
      <li v-if="showAnswer" :class="['italic', doneTask === answer ? 'text-green-400' : 'text-red-400' ]">
        {{ answer }}
      </li>
    </ul>
  </li>
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

  mounted() {
    const taskTextarea = this.$refs["task-textarea"] as HTMLElement;
    taskTextarea.setAttribute(
      "style",
      "height:" + (taskTextarea.scrollHeight) + "px;overflow-y:hidden;"
    );
    taskTextarea.addEventListener(
      "input",
      function () {
        this.style.height = "auto";
        this.style.height = (this.scrollHeight) + "px";
      },
      false
    );
  }
}
</script>

<style scoped lang="scss">

</style>
