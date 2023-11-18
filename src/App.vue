<script setup>
import Carousel from "./components/Carousel.vue"
import axios from "axios"
import { ref } from 'vue'
const getData = () => {
  return axios.get('https://download.kstore.space/download/4587/slide.json').then(({ data }) => data)
}
const list = ref([])
getData().then(data => {
  list.value = data.items ?? []
  console.log('list', list.value)
})
// list.value = [
//   {
//     "img": "https://images-eds-ssl.xboxlive.com/image?url=7flt5HU26ZSS3Tgted_TMty0wzqMQYpm03yD7eAPRtQBYO5dMlD18uZxNDuKXvpqoI2X0OvZgygt.WB6VC5szV7uS0xVVn0SZTEvbOvDQQQ0K.n0.Z2jUKeIYLLYVuLzNXmIFaEaUWPyEKgHtMGgOkpKlkfQzsNWbSQoN0adDYSpfFyCRQ9dXLUeFv_MvHqlI7zLcqfWAvzNk4K.ouWWZ0U2NyjX6ygCnxzancC2gV8-&h=900",
//     "href": "https://apps.microsoft.com/store/collections/ConnectAndStayInformed",
//     "desc": "This is the first picture"
//   },
//   {
//     "img": "https://images-eds-ssl.xboxlive.com/image?url=7flt5HU26ZSS3Tgted_TMty0wzqMQYpm03yD7eAPRtQBYO5dMlD18uZxNDuKXvpqkavwZIxg5NJS_jlxqlgqIFF.zli67C1nSZwDGVK8ULXXzeE.FgyEm6NMJ6MQOywgoWIXOiPeR8.guOX3VXMRDW3qNFfn5hWguh5PAy7Ac6xL8KBz7ScmHPJSNVh5gcx7&h=900",
//     "href": "https://apps.microsoft.com/store/detail/forza-motorsport-standard-edition/9PLKVSWR299F",
//     "desc": "This is the second picture"
//   },
//   {
//     "img": "https://images-eds-ssl.xboxlive.com/image?url=7flt5HU26ZSS3Tgted_TMty0wzqMQYpm03yD7eAPRtQBYO5dMlD18uZxNDuKXvpqf6eGleh8erTqCx5sLMHgqImmJ5Ic6M00dTGbVwVkSWxJySpOG2hgYon3ME2OSth.55sMpepOo8uRk4e8Ks83E4h9yxpXNjm6Hv1UgglL4ztyt_FQMO9Y0Kn5PxjIgilP&h=900",
//     "href": "https://apps.microsoft.com/store/detail/microsoft-365/CFQ7TTC0K5BF",
//     "desc": "This is the third picture"
//   },
//   {
//     "img": "https://images-eds-ssl.xboxlive.com/image?url=7flt5HU26ZSS3Tgted_TMty0wzqMQYpm03yD7eAPRtQBYO5dMlD18uZxNDuKXvpqtv0y2TDA8Dc5Il1K8jJv.Y1KQEEnlt63blKqmpYy39sy2lJLpRLJ_SWLhxitLBnZ6UkpZjKDrk4qlh1FcLmtg44T57e9MbTvX7ci105CN9z6zrGr91LpxhDE5qCB84ac6JjSihEZPH5DYDj.ZUwc7y6xKhewu2WwnCCwQQZ0N9M-&h=900",
//     "href": "https://apps.microsoft.com/store/collections/BestEntertainmentApps",
//     "desc": "This is the fourth picture"
//   }
// ]
getData()
</script>

<template>
  <div class="app">
    Carousel

    <Carousel :list="list">
    </Carousel>
  </div>
</template>

<style scoped lang="scss">
.app {
  margin:0 auto;
  text-align: center;
}

@media (min-width: 1200px) {
  .app {
    width: 900px;
  }
}
</style>