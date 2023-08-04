<template>
  <div class="flex flex-row bg-black text-white px-2 py-1 cursor-pointer">
    <!--服务器图标-->
    <div class="flex-shrink-0">
      <img :src="icon" alt="服务器图标" class="w-16 h-16" />
    </div>
    <!--服务器名称以及 motd-->
    <div
      class="flex flex-col flex-1 ml-2 overflow-hidden text-ellipsis whitespace-nowrap"
    >
      <div>{{ props.name }}</div>
      <div class="text-sm" v-html="motd"></div>
    </div>
    <div class="flex flex-col flex-shrink-0">
      <div class="text-sm"><span class="font-bold text-green-300">{{ onlinePlayers }}</span> 玩家在玩</div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from "vue";
import unknownIcon from "@/assets/icon/unknown_icon.png";

const props = defineProps({
  server: {
    type: String,
    required: false,
    default: "play.hypixel.net",
  },
  icon: {
    type: String,
    required: false,
    default: "",
  },
  name: {
    type: String,
    required: false,
    default: "服务器名称",
  },
});

const pingIcon = ref(unknownIcon);

const icon = computed(() => {
  console.log(props.icon);
  console.log(pingIcon);
  if (props.icon) {
    return props.icon;
  } else {
    return pingIcon.value;
  }
});

const handleServerInfo = async () => {
  const res = await fetch(`https://api.mcsrvstat.us/2/${props.server}`);
  const data = await res.json();
  if (data.online) {
    motd.value = data.motd.html.join("<br>");
    pingIcon.value = data.icon;
    onlinePlayers.value = data.players.online;
  } else {
    motd.value = "服务器离线";
  }
};

const motd = ref("正在获取服务器信息...");
const onlinePlayers = ref(0);

handleServerInfo();
</script>
