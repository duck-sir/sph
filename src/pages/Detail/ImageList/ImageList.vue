<template>
  <div class="swiper-container">
    <div class="swiper-wrapper">
      <div class="swiper-slide" v-for="img in skuImageList" :key="img.id">
        <img :src="img.imgUrl"  :class="{active:img.isDefault == 1}" @click="getBigImg(img.id)"/>
      </div>
    </div>
    <div class="swiper-button-next"></div>
    <div class="swiper-button-prev"></div>
  </div>
</template>

<script>
import Swiper from 'swiper'
export default {
  name: 'ImageList',
  props: ['skuImageList'],
  computed:{
  },
  watch: {
    skuImageList: {
      immediate: true,
      handler() {
        this.$nextTick(() => {
          var mySwiper = new Swiper('.swiper-container', {
            // direction: 'vertical', // 垂直切换选项
            // loop: true, // 循环模式选项
            // autoplay: true,
            // // 如果需要分页器
            // pagination: {
            //   el: '.swiper-pagination',
            //   clickable: true,
            // },
            slidesPerView: 3,
  grid: {
    fill: 'column',
    rows: 2,
  },

            // 如果需要前进后退按钮
            navigation: {
              nextEl: '.swiper-button-next',
              prevEl: '.swiper-button-prev',
            },

            // 如果需要滚动条
            // scrollbar: {
            //   el: '.swiper-scrollbar',
            // },
          })
        })
      },
    },
  },
  methods:{
    getBigImg(id){
      let bigUrl = ''
      this.skuImageList.forEach(item => {
        if(item.id == id){
          bigUrl = item.imgUrl
        }
      });
      this.$bus.$emit('getBigImg',bigUrl)
      this.$store.commit('detail/CHANGEISDEFAULT',id)
    }
  }
}
</script>

<style lang="less" scoped>
.swiper-container {
  height: 56px;
  width: 412px;
  box-sizing: border-box;
  padding: 0 12px;

  .swiper-slide {
    width: 56px;
    height: 56px;

    img {
      width: 100%;
      height: 100%;
      border: 1px solid #ccc;
      padding: 2px;
      width: 50px;
      height: 50px;
      display: block;

      &.active {
        border: 2px solid #f60;
        padding: 1px;
      }

      // &:hover {
      //   border: 2px solid #f60;
      //   padding: 1px;
      // }
    }
  }

  .swiper-button-next {
    left: auto;
    right: 0;
  }

  .swiper-button-prev {
    left: 0;
    right: auto;
  }

  .swiper-button-next,
  .swiper-button-prev {
    box-sizing: border-box;
    width: 12px;
    height: 56px;
    background: rgb(235, 235, 235);
    border: 1px solid rgb(204, 204, 204);
    top: 0;
    margin-top: 0;
    &::after {
      font-size: 12px;
    }
  }
}
</style>
