<template>
  <div>
    <ContentList path="/detail">
      <template #default="{ list }">
        <div v-for="server in servers" :key="server._path">
          <NuxtLink v-if="!server.hide" :to="server._path" target="_blank">
            <ServerItem
              class="mb-1"
              :name="server.name"
              :server="server.address"
            ></ServerItem>
          </NuxtLink>
        </div>
      </template>
      <template #not-found>
        <p>No articles found.</p>
      </template>
    </ContentList>
  </div>
</template>

<script lang="ts" setup>
import ServerItem from "@/components/content/ServerItem.vue";

const { data: servers } = useAsyncData(async () => {
  const res = (await queryContent("detail").find()).filter(
    (item: any) => !item.hide
  );
  return res;
});

const randSort = () => {
  servers.value?.sort(() => Math.random() - 0.5);
};

onMounted(() => {
  if (process.client) {
    randSort();
  }
});


</script>
