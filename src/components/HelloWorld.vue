<template>
  <h1>{{ msg }}</h1>
  <h1>{{ obj.name }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <n-button type="primary" @click="obj.name += '捏'">捏一下</n-button>
  </div>

  <n-carousel :space-between="20" draggable>
    <img class="carousel-img" src="https://naive-ui.oss-cn-beijing.aliyuncs.com/carousel-img/carousel1.jpeg">
    <img class="carousel-img" src="https://naive-ui.oss-cn-beijing.aliyuncs.com/carousel-img/carousel2.jpeg">
    <img class="carousel-img" src="https://naive-ui.oss-cn-beijing.aliyuncs.com/carousel-img/carousel3.jpeg">
    <img class="carousel-img" src="https://naive-ui.oss-cn-beijing.aliyuncs.com/carousel-img/carousel4.jpeg">
  </n-carousel>
</template>

<script setup lang="ts">

import { onMounted } from 'vue';
import { ref, reactive } from 'vue'


defineProps<{ msg: string }>()

const count = ref(0)

const obj = reactive({ name: '桃子' })

/**
 * 字符串转大写
 * @param {string} str 需要大写的字符串
 * @return {string} 返回的大写字符串
 */
const upper = function (str: string): string {
  return str.toUpperCase()
}


onMounted(() => {
  (async function fetchData() {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');
      const data = await response.json();
      console.log(data.title);
      obj.name = upper(data.title)
    } catch (error) {
      console.error(error);
    }
  })()

})

</script>



<style lang="less" scoped>
.card {
  button{
    color: aqua
  }
  color: #888;
}

.carousel-img {
  width: 100%;
  height: 240px;
  object-fit: cover;
}
</style>
