<template>
  <Wrapper
    :title="props.data.name"
    @clickMore="moreHandler"
    @clickTitle="titleHandler"
    class="ml-[5vw]"
  >
    <BetterScroll
      :config="{ scrollX: true, scrollY: false, click: true }"
      :dep="props.data"
    >
      <div
        @click="clickHandler(item)"
        v-for="item in props.data.children"
        :key="item.id"
        class="mt-[3vw] mr-[5vw]"
      >
        <img
          class="w-[34vw] h-[34vw] rounded-[5vw]"
          :src="item.imageUrl"
          alt=""
        />
        <div class="w-[34vw] h-[4.5vw] overflow-hidden text-[3vw]">
          {{ item.title }}
        </div>
      </div>
    </BetterScroll>
  </Wrapper>
</template>

<script setup>
import { defineProps } from "vue";
import { useRouter } from "vue-router";
import BetterScroll from "@/components/BetterScroll.vue";
import Wrapper from "@/components/Wrapper.vue";

const props = defineProps({
  data: {
     type: Array,
    required: true,
  },
});
const router = useRouter();

const clickHandler = (item) => {
  // 跳转到播放新歌曲页面，并传递 id
  router.push({ path: "/songlist", query: { a: item.id } })
   .then(() => {
      console.log("Navigation successful");
    })
    .catch(err => {
      console.error("Navigation error:", err);
    });
};
const moreHandler = () => {
  console.log("推荐歌单的更多被点击了");
};

const titleHandler = () => {
  console.log("推荐歌单的标题被点击了");
};
</script>
