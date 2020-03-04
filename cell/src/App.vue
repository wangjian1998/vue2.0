<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <!-- <div class="content">
     我是主要内容
    </div>-->
    <keep-alive>
    <router-view :seller="seller"></router-view>
    </keep-alive>
    
  </div>
</template>

 <script>
import header from "./components/header/header.vue";

const ERR_OK = 0;
export default {
  data() {
    return {
      seller: {}
    };
  },
  created() {
    this.axios.get("/api/seller").then(response => {
      response = response.data;
      if (response.errno === ERR_OK) {
        this.seller = response.data;
      }
    });
  },
  components: {
    "v-header": header
  }
};
</script> 

<style>
.tab {
  display: flex;
  height: 40px;
  line-height: 40px;
  width: 100%;
  border-bottom: 1px solid rgba(7, 17, 21, 0.1);
}

.tab-item {
  flex: 1;
  text-align: center;
}

.tab-item > a {
  display: block;
  font-size: 14px;
  color: rgb(77, 85, 93);
}

.tab-item > a.active {
  color: rgb(240, 20, 20);
}
</style>
