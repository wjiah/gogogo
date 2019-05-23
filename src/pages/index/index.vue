<template>
  <div>
    <!-- 焦点图 -->
    <swiper class="banner" indicator-dots indicator-color="rgba(255, 255, 255, 0.6)" indicator-active-color="#fff">
      <swiper-item v-for="list in banner" :key="goods_id">
        <image :src="list.image_src"></image>
      </swiper-item>
    </swiper>
    <!-- 导航条 -->
    <div class="navs">
      <image :src="item.image_src" v-for="(item,i) in cart" :key="i"></image>
    </div>
    <!-- 楼层 -->
    <div class="floors" v-for="(item,i) in floor" :key="i">
      <div class="floor">
        <div class="title">
          <image :src="item.floor_title.image_src"></image>
        </div>
        <div class="items">
          <image v-for="(lastitem,key) in item.product_list" :key="key" :src="lastitem.image_src"></image>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import request from '../../utils/request.js'

export default {
  data () {
    return {
      banner: [],
      cart: [],
      floor: []
    }
  },
  mounted () {
    this.getBanner()
    this.getCart()
    this.getFloor()
  },
  methods: {
    // 轮播图
    async getBanner () {
      const {message} = await request({
        url: 'api/public/v1/home/swiperdata'
      })
      this.banner = message
    },
    // 导航菜单
    async getCart () {
      const {message} = await request({
        url: 'api/public/v1/home/catitems'
      })
      this.cart = message
    },
    // 楼层
    async getFloor () {
      const {message} = await request({
        url: 'api/public/v1/home/floordata'
      })
      this.floor = message
    }
  }
}
</script>

<style scoped lang="less">

  .banner {
    width: 100%;
    height: 340rpx;

    image {
      width: 100%;
      height: 340rpx;
    }
  }

  .navs {
    display: flex;
    justify-content: space-between;
    padding: 30rpx 44rpx;

    image {
      width: 128rpx;
      height: 140rpx;
    }
  }

  .floors {

    .title {
      width: 750rpx;
      height: 60rpx;
      padding-top: 20rpx;
      background-color: #f4f4f4;
      image{
         height:100%
      }
    }

    .items {
      padding: 20rpx 16rpx;
      overflow: hidden;

      image {
        width: 232rpx;
        height: 188rpx;
        margin-right: 10rpx;
        margin-bottom: 10rpx;
        float: left;
      }

      image:nth-child(2n+1) {
        margin-right: 0;
      }

      image:first-child {
        height: 386rpx;
        margin-right: 10rpx;
      }
    }
  }
</style>
