<template>
  <div>
    <div class="clearfix recommend-header">
      <h3 class="fl title">推荐商品</h3>
      <div class="fr">
        <i class="icon-font icon-left pagination-item" :class="{'disabled': activeIndex === 0}" @click="prev"></i>
        <i class="icon-font icon-right pagination-item" :class="{'disabled': activeIndex === pageSize}" @click="next"></i>
      </div>
    </div>
    <div class="recommend-content">
      <ul class="clearfix" :style="listWrapper">
        <li class="goods-list" v-for="(item, index) in data" :key="index" :class="{'last-child' : (index + 1) % 4 === 0 }">
          <a :href="item.href">
            <img :src="item.goodsUrl" alt="">
            <div class="goods-name"> {{ item.goodsName }} </div>
            <div class="goods-desc"> {{ item.goodsDesc }} </div>
            <div class="goods-price">
              <i>￥</i>
              {{ item.goodsPrice }}
              <span class="lower" v-if="item.lower">起</span>
              <span class="goods-oldprice" v-if="item.oldPrice"> {{ item.oldPrice }} </span>
            </div>
          </a>
          <div class="goods-new" v-if="item.newProduct">新品</div>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  name: 'recommend-list',
  props: {
    data: {
      type: Array,
      default () {
        return []
      }
    }
  },
  data () {
  	return {
  		activeIndex: 0
  	};
  },
  computed: {
    listWrapper() {
      return {
        width: `${ (this.data.length) * 250 }px`,
        transform: `translateX(-${this.activeIndex * 1240}px)`,
        transitionDuration: '.3s'
      };
    },
    pageSize () {
    	return Math.floor(this.data.length / 5);
    }
  },
  methods: {
  	prev () {
     if (this.activeIndex === 0) return;
     this.activeIndex -= 1;
  	},
  	next () {
    if (this.activeIndex === this.pageSize) return;
    this.activeIndex += 1;
  	}
  }
};

</script>
<style lang="less">
.recommend-header {
  margin: 30px auto 10px;

  .title {
    font-style: 30px;
    font-weight: 400;
  }

  .pagination-item {
    display: inline-block;
    width: 24px;
    height: 24px;
    line-height: 24px;
    text-align: center;
    cursor: pointer;
    font-style: 12px;
    color: #00c3f5;
    border: 1px solid #00c3f5;

    &.disabled {
      color: #efefef;
      border-color: #dcdcdc;
    }
  }
}

.recommend-content {
  width: 1240px;
  background-color: #fff;
  overflow: hidden;

  .goods-list {
    position: relative;
    float: left;
    width: 220px;
    margin: 8px 15px;
    padding: 34px 0 15px;
    background-color: #fff;
    cursor: pointer;
    transition: all .3s ease;
    overflow: hidden;
    text-align: center;

    img {
      height: 180px;

      &:hover {
      	transform: scale(1.2); 
      	transition: all .3s;
      }
    }

    &.last-child {
      margin-right: 0;
    }
  }

  .goods-img {
    height: 230px;
    margin-top: 30px;
  }

  .goods-name {
    margin-top: 70px;
    margin-bottom: 2px;
    color: #555757;
    font-size: 14px;
  }

  .goods-desc {
    font-size: 12px;
    color: #999;
  }

  .goods-price {
    position: relative;
    display: inline-block;
    padding-left: 14px;
    font-size: 16px;
    color: #c00;
    margin-top: 8px;

    i {
      position: absolute;
      left: 0;
      top: 2px;
      font-style: normal;
      font-size: 12px;
    }

    .lower {
      font-size: 16px;
    }

    .goods-oldprice {
      text-decoration: line-through;
      color: #666;
      font-size: 14px;
      margin-left: 8px;
    }
  }

  .goods-new {
    position: absolute;
    left: 30px;
    top: 30px;
    width: 60px;
    height: 60px;
    line-height: 60px;
    text-align: center;
    border-radius: 50%;
    background: linear-gradient(120deg, #2e74f6, #56bdf9);
    color: #fff;
  }

  .empty {
    width: 335px;
    margin: 170px auto 380px;

    .empty-bg {
      background: url('../assets/images/xiongmao.png') no-repeat;
      width: 105px;
      height: 135px;
      margin-right: 30px;
    }

    .empty-desc {
      width: 200px;
    }

    .title {
      font-style: 18px;
      color: #00c3f5;
      margin: 15px auto;
    }
  }
}

</style>
