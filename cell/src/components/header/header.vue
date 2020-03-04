<template>
  <div>
    <div class="header">
      <div class="content-wrapper">
        <!-- 商家图片 -->
        <div class="avatar">
          <img width="64" height="64" :src="seller.avatar" alt="商家图片" />
        </div>
        <!-- 内容区 -->
        <div class="content">
          <div class="title">
            <span class="brand"></span>
            <span class="name">{{seller.name}}</span>
          </div>
          <div class="description">{{seller.description}}/{{seller.deliveryTime}}分钟送达</div>
          <div v-if="seller.supports" class="support">
            <span class="icon" :class="classMap[seller.supports[0].type]"></span>
            <span class="text">{{seller.supports[0].description}}</span>
          </div>
          <!-- 弹出层 -->
          <div v-if="seller.supports" class="support-count" @click="detailShow">
            <span class="count">{{seller.supports.length}}个</span>
            <span class="icon-keyboard_arrow_right"></span>
          </div>
        </div>
      </div>
      <!-- 商家介绍 -->
      <div class="bulletin-wrapper">
        <span class="bulletin-title"></span>
        <span class="bulletin-text">{{seller.bulletin}}</span>
        <i></i>
      </div>

      <div class="background">
        <img :src="seller.avatar" width="100%" height="100%" />
      </div>
      <!-- 弹出层详情 -->

      <div class="detail" v-show="showDetail">
        <div class="detail-wrapper clearfix">
          <div class="detail-main">
            <h1 class="name">{{seller.name}}</h1>
            <div class="star-wrapper">
              <star :size="48" :score="seller.score"></star>
            </div>
            <div class="title">
              <div class="line"></div>
              <div class="text">优惠信息</div>
              <div class="line"></div>
            </div>
            <ul v-if="seller.supports" class="supports">
              <li v-for="(item,i) in seller.supports" :key="i" class="support-item">
                <span class="icon" :class="classMap[item.type]"></span>
                <span class="text">{{item.description}}</span>
              </li>
            </ul>
            <div class="title">
              <div class="line"></div>
              <div class="text">商家公告</div>
              <div class="line"></div>
            </div>
            <div class="bulletin">
              <p class="content">{{seller.bulletin}}</p>
            </div>
          </div>
        </div>
        <div class="detail-close">
          <i class="icon-close" @click="detailClose">x</i>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import star from "@/components/star/star";
export default {
  props: {
    seller: {
      type: Object
    }
  },
  data() {
    return {
      showDetail: false
    };
  },
  components: {
    star
  },
  methods: {
    detailShow() {
      this.showDetail = true;
    },
    detailClose() {
      this.showDetail = false;
    }
  },
  created() {
    this.classMap = ["decrease", "discount", "special", "invoice", "guarantee"];
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
 @import "../../common/stylus/icon.styl"
.header {
  position: relative;
  overflow: hidden;
  color: #fff;
  background-color: rgba(7, 17, 27, 0.5);
}

.clearfix {
  display: inline-block;
}

.clearfix:after {
  content: '.';
  display: block;
  clear: both;
  visibility: hidden;
}

.content-wrapper {
  padding: 24px;
  position: relative;
}

.avatar {
  display: inline-block;
  vertical-align: top;
}

.avatar img {
  border-radius: 2px;
}

.content {
  display: inline-block;
  margin-left: 16px;
  font-size: 14px;
}

.title {
  margin: 2px 0 8px 0;
}

.brand {
  width: 30px;
  height: 18px;
  display: inline-block;
  background-image: url('./brand@2x.png');
  background-size: 30px 18px;
  vertical-align: top;
}

.name {
  margin-left: 6px;
  font-size: 16px;
  line-height: 18px;
  font-weight: bold;
}

.description {
  margin-bottom: 10px;
  line-height: 12px;
  font-size: 12px;
}

.support .icon {
  display: inline-block;
  width: 12px;
  height: 12px;
  vertical-align: top;
  margin-right: 4px;
  background-size: 12px 12px;
  background-repeat: no-repeat;
}

.support .icon.decrease {
  background-image: url('./decrease_1@2x.png');
}

.support .icon.discount {
  background-image: url('./discount_1@2x.png');
}

.support .icon.guarantee {
  background-image: url('./guarantee_1@2x.png');
}

.support .icon.invoice {
  background-image: url('./invoice_1@2x.png');
}

.support .icon.special {
  background-image: url('./special_1@2x.png');
}

.support .text {
  line-height: 12px;
  font-size: 10px;
}

.support-count {
  position: absolute;
  right: 12px;
  bottom: 14px;
  padding: 0 8px;
  height: 24px;
  line-height: 24px;
  border-radius: 14px;
  background-color: rgba(0, 0, 0, 0.2);
  text-align: center;
}

.support-count .count {
  font-size: 10px;
  vertical-align: top;
}

.support-count .icon_arrow_right {
  margin-left: 2px;
  line-height: 24px;
  font-size: 10px;
}

.support-count .icon-keyboard_arrow_right:before {
  content: '\e909';
}

.bulletin-wrapper {
  height: 28px;
  line-height: 28px;
  padding: 0 22px 0 12px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  background-color: rgba(7, 17, 27, 0.2);

  .bulletin-title {
    display: inline-block;
    width: 22px;
    height: 12px;
    vertical-align: top;
    margin-top: 8px;
    background-image: url('./bulletin@2x.png');
    background-size: 22px 12px;
    background-repeat: no-repeat;
  }

  .bulletin-text {
    vertical-align: top;
    font-size: 10px;
    margin: 0 4px;
  }
}

.background {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  z-index: -1;
  filter: blur(5px);
}

.detail {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background: rgba(7, 17, 27, 0.8);
  z-index :999;
  

  .detail-wrapper {
    min-height: 100%;
    width: 100%;

    .detail-main {
      margin-top: 64px;
      padding-bottom: 64px;

      .name {
        line-height: 16px;
        text-align: center;
        font-size: 16px;
        font-weight: 700;
      }

      .star-wrapper {
        margin-top: 18px;
        padding: 2px 0;
        text-align: center;
      }

      .title {
        display: flex;
        width: 80%;
        margin: 28px auto 24px auto;

        .line {
          flex: 1;
          position: relative;
          top: -6px;
          border-bottom: 1px solid rgba(255, 255, 255, 0.2);
        }

        .text {
          padding: 0 12px;
          font-weight: 700;
          font-size: 14px;
        }
      }

      .supports {
        width: 80%;
        margin: 0 auto;

        .support-item {
          padding: 0 12px;
          margin-bottom: 12px;
          font-size: 0;

          &:last-child {
            margin-bottom: 0;
          }

          .icon {
            display: inline-block;
            width: 16px;
            height: 16px;
            vertical-align: top;
            margin-right: 6px;
            background-size: 16px 16px;

            &.decrease {
              background-image: url('./decrease_1@2x.png');
            }

            &.discount {
              background-image: url('./discount_1@2x.png');
            }

            &.guarantee {
              background-image: url('./guarantee_1@2x.png');
            }

            &.invoice {
              background-image: url('./invoice_1@2x.png');
            }

            &.special {
              background-image: url('./decrease_1@2x.png');
            }
          }

          .text {
            font-size: 12px;
            line-height: 16px;
          }
        }
      }

      .bulletin {
        width: 80%;
        margin: 0 auto;

        .content {
          font-size: 12px;
          padding: 0 12px;
          line-height: 24px;
        }
      }
    }
  }

  .detail-close {
    margin: -64px auto 0 auto;
    position: relative;
    width: 32px;
    height: 32px;
    clear: both;
    font-size: 32px;
  }
}
</style>