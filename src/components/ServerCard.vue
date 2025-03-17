<script setup>
import MCTextComponent from './MCTextComponent.vue'

defineProps({
  data: {
    type: Object,
    required: true,
  },
})

function parsePlayers(players) {
  const parsedPlayers = players.split("/")
  return {
    maxPlayers: parsedPlayers[1],
    players: parsedPlayers[0]
  }
}

function copyIPAddress(connect_key) {
  const input = document.getElementById(`copyipaddress-${connect_key}`);
  input.select();
  try {
    const successful = document.execCommand('copy');
    if (successful) {
      input.setSelectionRange(0, input.value.length);
    }
  } catch (err) {}
}
</script>

<template>
  <div class="flex flex-col gap-2 p-3 w-full text-white bg-gray-500 rounded-lg">
    <div class="flex gap-2">
      <img :src="data.mcinfo.favicon" class="rounded-lg" width="68" />
      <div class="flex flex-col w-full">
        <div class="flex">
          <p class="font-bold text-lg">{{ data.server_name }}</p><span class="ml-auto">{{
            parsePlayers(data.mcinfo.players).players }}人がプレイ中 (一度に入室できるプレイヤー数: {{
              parsePlayers(data.mcinfo.players).maxPlayers }}人)</span>
        </div>
        <MCTextComponent :text="data.mcinfo.motd" class="text-gray-300" />
      </div>
    </div>
    <div class="flex">
      <input class="text-blue-300 hover:text-blue-400" readonly :value="`${data.connect_key}.zcnc.me`" :id="`copyipaddress-${data.connect_key}`" @click="copyIPAddress(data.connect_key)" v-if="data.protocol === 'tcp'" />
      <span class="rounded-full bg-blue-300 px-2">{{ data.protocol }}</span>
    </div>
  </div>
</template>