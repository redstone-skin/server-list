<template>
  <div>
    <NarBar></NarBar>
    <div class="mt-12 container mx-auto px-2">
      <ContentDoc v-slot="{ doc }">
        <div class="py-6">
          <!--服务器信息-->
          <div>
            <div class="text-4xl">{{ doc.name }}</div>
            <!--info-->
            <div class="mt-10 flex flex-wrap">
              <div
                v-for="item in toInfoItems(doc)"
                :key="item.label"
                class="flex flex-row items-center h-10 md:w-1/3 sm:w-1/2 w-full text-sm"
              >
                <div class="min-w-fit">{{ item.label }}：</div>
                <NuxtLink 
                  v-if="item.link"
                  :href="item.value"
                  target="_blank"
                  class="text-ellipsis overflow-hidden whitespace-nowrap"
                  >{{ item.value }}</NuxtLink
                >
                <div
                  v-else
                  class="text-ellipsis overflow-hidden whitespace-nowrap"
                >
                  {{ item.value }}
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="markdown-body">
          <ContentRenderer :value="doc" />
        </div>
        <!--免责声明-->
        <div class="mt-4 border-l-4 border-l-black pl-4 dark:border-l-white">
          <div class="text-2xl">
            免责声明
          </div>
          <div class="mt-2">
            本站与服务器无任何合作关系，本站仅提供服务器信息查询服务，不提供任何游戏服务，本站不对服务器的安全性、合法性、真实性负责，不承担任何法律责任。
          </div>
        </div>
      </ContentDoc>
    </div>
    <FootBar></FootBar>
  </div>
</template>
<script setup lang="ts">

const checkUrlPrefix = (str: string) => {
  return str.startsWith("http:") || str.startsWith("https:");
}


const toInfoItems = (doc: any) => {
  const items = [];
  if (doc.team) {
    items.push({
      label: "运营团队",
      value: doc.team,
    });
  }
  if (doc.version) {
    items.push({
      label: "版本",
      value: doc.version,
    });
  }
  if (doc.address) {
    items.push({
      label: "IP",
      value: doc.address,
    });
  }
  if (doc.group) {
    items.push({
      label: "QQ 群",
      value: doc.group,
    });
  }
  if (doc.website) {
    items.push({
      label: "网站",
      value: doc.website,
      link: checkUrlPrefix(doc.website),
    });
  }
  if (doc.download) {
    items.push({
      label: "客户端下载地址",
      value: doc.download,
      link: checkUrlPrefix(doc.download),
    });
  }
  items.push({
    label: "红石账号登录",
    value: doc.yggdrasil ? "支持" : "不支持",
  });

  return items;
};
</script>

<style>
@import "@/assets/css/github-markdown.css";
body {
  background-color: #fff;
  color: rgba(0, 0, 0, 0.8);
}
.dark-mode body {
  background-color: #091a28;
  color: #ebf4f1;
}
.sepia-mode body {
  background-color: #f1e7d0;
  color: #433422;
}
ul {
  list-style: disc;
  padding-left: 2em;
}
</style>
