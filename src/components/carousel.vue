<template>
  <div ref="carousel" class="carousel" @mouseenter="handleStop" @mouseleave="handleStart">
    <div class="carousel-wrap" :style="{ transform: `translate(-${activeIndex * 100}%)` }">
      <div class="carousel-item" v-for="(item, index) in list" :key="index">
        <img :src="item.img" :alt="item.desc" :title="item.desc" @click="handleClickImg(item.href)" />
      </div>
    </div>
    <div class="btns">
      <span class="btn prev" @click="handlePrev">
        prev
      </span>
      <span class="btn next" @click="handleNext">
        next
      </span>
    </div>
    <div class="indictors">
      <span :class="['dot', activeIndex === index ? 'active' : '']" v-for="(_, index) of list.length"
        @click="handleChangeActive(index)">
      </span>
    </div>
  </div>
</template>

<script setup>
import { useSwipe, useThrottleFn } from '@vueuse/core'
import { ref, onMounted, onUnmounted, watch } from 'vue'
const carousel = ref(null)

const { isSwiping, direction } = useSwipe(carousel)
watch(isSwiping, useThrottleFn(() => {
  if (direction.value === "left") {
    handleNext()
  } else {
    handlePrev()
  }
}, 100))
const props = defineProps({
  list: {
    type: Array,
  },
  interval: {
    type: Number,
    default: 5000
  },
})
const activeIndex = ref(0)
let timer = null
const handleStart = () => {
  if (timer) return
  timer = setInterval(() => {
    activeIndex.value = (activeIndex.value + 1) % props.list.length
  }, props.interval)
}

const handleStop = () => {
  if (timer) {
    console.log('stop')
    clearInterval(timer)
  }
  timer = null
}

const handlePrev = () => {
  handleStop()
  activeIndex.value = (activeIndex.value - 1 + props.list.length) % props.list.length
  handleStart()
}

const handleNext = () => {
  handleStop()
  activeIndex.value = (activeIndex.value + 1) % props.list.length
  handleStart()
}
const handleChangeActive = (index) => {
  activeIndex.value = index
}
const handleClickImg = (url) => {
  // location.href = url
  window.open(url, '_blank')
}
onMounted(handleStart)
onUnmounted(handleStop)

</script>

<style scoped lang="scss">
.carousel {
  border-radius: 12px;
  position: relative;
  overflow: hidden;

  .carousel-wrap {
    display: flex;
    transition: transform .8s;

    .carousel-item {
      flex: 0 0 auto;
      width: 100%;
      padding-top: 56.25%;
      position: relative;

      img {
        cursor: pointer;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
    }
  }

  .btns {
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    left: 0;
    right: 0;

    .btn {
      border-radius: 12px;
      padding: 12px;
      cursor: pointer;
      background-color: rgba(#000, .3);
      color: #fff;
    }
  }

  .indictors {
    position: absolute;
    bottom: 20px;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;

    .dot {
      cursor: pointer;
      margin: 0 8px;
      border-radius: 50%;
      width: 18px;
      height: 18px;
      background-color: rgba(#000, .3);

      &.active {
        position: relative;
        background-color: #fff;
      }
    }
  }
}
</style>
