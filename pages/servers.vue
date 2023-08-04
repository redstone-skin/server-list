<template>
  <div>
    <ContentList path="/detail">
      <template #default="{ list }">
        <NuxtLink v-for="server in list" :key="server._path" :to="server._path"  target="_blank">
          <ServerItem v-if="!server.hidden" class="mb-1" :name="server.name" :server="server.address"></ServerItem>
        </NuxtLink>
      </template>
      <template #not-found>
        <p>No articles found.</p>
      </template>
    </ContentList>
  </div>
</template>

<script lang="ts" setup>
import ServerItem from "@/components/content/ServerItem.vue";
</script>
