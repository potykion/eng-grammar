<template>
  <div>
    <header></header>

    <main>
      <Nuxt/>
    </main>
  </div>

</template>

<script lang="ts">

import {
  Component,
  Prop,
  Vue,
} from "nuxt-property-decorator"


@Component
export default class Default extends Vue {
}
</script>

<style>

main {
  @apply px-80;
}

h1 {
  @apply text-2xl font-bold;
}
h2 {
  @apply text-xl py-2 font-bold;
}

a {
  @apply underline text-blue-400;
}

ol {
  @apply list-decimal list-inside	;
}
ol > li {
  @apply py-1;
}
hr {
  @apply border-solid my-6;
}

</style>
