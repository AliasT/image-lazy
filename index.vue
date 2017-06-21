<template>
  <img :src="img" ref="img"/>
</template>

<script>
  // pixel:一像素的图片
  import pixel from '@/something/white.gif'
  export default {
    name: 'm-image',
    props: ['src', 'blur'],   
    data() {
      return {
        img: this.src || pixel
      }
    },
    watch: {
      src(newValue) {
        // 添加blur选项会给图片带来透明度动画效果
        if(this.blur) {
          const { img } = this.$refs
          const _img = new Image()
          _img.onload = (e) => {
            img.style.transition = "opacity,background, .3s ease-out"
            img.style.background = 'rgba(255, 255, 255, .3)'
            img.style.opacity = 0
            setTimeout(() => {
              img.style.opacity = '1'
              img.src = newValue
            }, 300)
          }
          _img.src = newValue
        } else {
          this.img = newValue
        }
      }
    },
    mounted() {
      this.$refs.img.onerror = () => this.img = pixel
    }
  }
</script>
