<script setup>
import ServerCard from "./components/ServerCard.vue";
import { ref } from "vue";
import { ofetch } from "ofetch";

const data = ref({});
const protocols = ref(['tcp', 'udp']);

const fetchData = async () => {
  data.value = await ofetch('https://zsc-proxy.sonyaumg.workers.dev/connect/serverlist.php');
};

fetchData();

/*
data.value = {
  "status": "ok",
  "data": [
    {
      "id": 2880,
      "connect_key": "teisupe",
      "サーバー名": "低スペノートで作ったサーバー",
      "server_name": "低スペノートで作ったサーバー",
      "mcinfo": {
        "version": "Purpur 1.21",
        "motd": "§f[§d1.21.0~§f]§aSimple Voice Chat対応§fサバイバルサーバー(24H?)",
        "players": "0/10",
        "favicon": "data:image/jpeg;base64,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"
      },
      "is_public": true,
      "protocol": "tcp",
      "created_at": "2025-03-17 07:35:37",
      "updated_at": "2025-03-17 07:35:37"
    }
  ]
}
*/
</script>

<template>
  <Suspense>
    <template #default>
      <div>
        <h1 class="text-center font-bold text-2xl m-2">Connect Server List</h1>
        <main class="p-5">
          <div class="flex mb-2 gap-2">
            <div class="flex flex-col">
              <label class="text-sm">プロトコルで絞り込む</label>
              <select v-model="protocols" class="text-black border rounded-lg" required>
                <option value="all" selected>全て</option>
                <option value="tcp" key="tcp">
                  TCP (Java版)
                </option>
                <option value="udp" key="udp">
                  UDP (統合版)
                </option>
              </select>
            </div>
            <div class="ml-auto flex flex-col text-xs">
              <p>※更新されない場合は5分後に再度試してください。</p>
              <p class="text-blue-400 hover:text-blue-500"><a rel="noopener noreferer" target="_blank" href="https://github.com/sonyakun/connect-server-list">ソースコードはこちら</a></p>
            </div>
          </div>
          <div v-if="data.data && data.data.length">
            <div class="flex flex-col gap-2">
              <div v-for="d in data.data" :key="d.id">
                <ServerCard :data="d"
                  v-if="d.is_public && protocols.includes(d.protocol) || protocols.includes('all')" />
              </div>
            </div>
          </div>
        </main>
      </div>
    </template>
    <template #fallback>
      <div>読み込んでいます...</div>
    </template>
  </Suspense>
</template>
