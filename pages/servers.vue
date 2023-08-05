<template>
  <div>
    <NuxtLink
      v-for="server in serverList"
      :key="server.path"
      :to="server.path"
      target="_blank"
    >
      <ServerItem
        v-if="!server.hide"
        class="mb-1"
        :name="server.name"
        :server="server.address"
      ></ServerItem>
    </NuxtLink>
  </div>
</template>

<script lang="ts" setup>
import ServerItem from "@/components/content/ServerItem.vue";

const serverList = ref<
  {
    path: string;
    name: string;
    address: string;
    hide: boolean;
  }[]
>([]);

const loadServers = async () => {
  const contentQuery = queryContent("detail");
  serverList.value = (await contentQuery.find())
    .map((item) => {
      return {
        path: item._path as string,
        name: item.name,
        address: item.address,
        hide: item.hide,
      };
    })
    .sort(() => {
      // random sort
      return Math.random() > 0.5 ? 1 : -1;
    });
};

loadServers();
</script>