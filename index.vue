<template>
  <img :src="img" ref="img" @load="load($event)" alt="加载失败"/>
</template>

<script>
  // 使用一像素的图片占位，而不用通过在dom里操作背景
  import pixel from '@/assets/m.gif'
  export default {
    name: 'm-image',
    props: ['src', 'blur'],   
    data() {
      return {
        img: this.src || pixel
      }
    },
    methods: {
      load(evt) {
        console.log(evt.target)
        const { img } = this.$refs
        img.style.transition = "background, opacity 1s ease-out"
        img.style.background = 'rgba(255, 255, 255, .3)'
        evt.target.style.opacity = 1
      }
    },
    watch: {
      src(newValue) {
        this.img = newValue
      }
    },
    mounted() {
      this.$refs.img.onerror = () => this.img = pixel
    }
  }
</script>

<style lang="scss" scoped>
  img {
    opacity: 0;
  }
</style>
