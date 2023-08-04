<template>
  <!--footer-->
  <div class="black py-8">
    <div class="container mx-auto flex justify-center items-center">
        <div class="text-md font-bold">© {{ year }} 红石皮肤站</div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

const year = ref(new Date().getFullYear())

</script>
