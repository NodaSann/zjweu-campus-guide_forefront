<template>
  <view class="links-container">
    <!-- 半透明背景 -->
    <view class="mask" @click="closePopup"></view>
    
    <!-- 弹窗内容 -->
    <view class="popup-content">
      <view class="popup-header">
        <text class="popup-title">相关链接</text>
        <text class="close-btn" @click="closePopup">×</text>
      </view>
      
      <scroll-view scroll-y="true" class="links-scroll">
        <view class="links-section">
          <view class="links-list">
            <view class="link-item" v-for="(item, index) in linkItems" :key="index" @click="openLink(item.url)">
              <view class="link-icon" :style="{ backgroundColor: item.bgColor }">
                <text class="iconfont">{{ item.icon }}</text>
              </view>
              <text class="link-text">{{ item.text }}</text>
            </view>
          </view>
        </view>
      </scroll-view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      linkItems: [
        { 
          icon: '🏫', 
          text: '学校官网', 
          bgColor: '#6A87AD', 
          url: 'https://www.university.edu.cn' 
        },
        { 
          icon: '📝', 
          text: '校园服务', 
          bgColor: '#9CB4CC', 
          url: 'https://service.university.edu.cn' 
        },
        { 
          icon: '📚', 
          text: '教务网站', 
          bgColor: '#B6DCFE', 
          url: 'https://jwc.university.edu.cn' 
        }
      ]
    }
  },
  methods: {
    closePopup() {
      uni.navigateBack();
    },
    openLink(url) {
      // 在小程序中可以使用以下方式打开网页
      // #ifdef MP
      uni.navigateTo({
        url: `/pages/webview/webview?url=${encodeURIComponent(url)}`
      });
      // #endif
      
      // 在H5中直接打开链接
      // #ifdef H5
      window.open(url, '_blank');
      // #endif
      
      // 在APP中使用系统浏览器打开
      // #ifdef APP-PLUS
      plus.runtime.openURL(url);
      // #endif
    }
  }
}
</script>

<style>
.links-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 999;
  display: flex;
  justify-content: center;
  align-items: center;
}

.mask {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.popup-content {
  position: relative;
  width: 80%;
  max-height: 70%;
  background-color: #fff;
  border-radius: 15rpx;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  z-index: 1000;
  box-shadow: 0 0 20rpx rgba(0, 0, 0, 0.2);
}

.popup-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30rpx;
  border-bottom: 1rpx solid #eee;
}

.popup-title {
  font-size: 36rpx;
  font-weight: bold;
  color: #333;
}

.close-btn {
  font-size: 48rpx;
  color: #999;
  line-height: 1;
}

.links-scroll {
  flex: 1;
  max-height: calc(70vh - 100rpx);
}

.links-section {
  padding: 30rpx;
}

.links-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.link-item {
  width: 30%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 40rpx;
}

.link-icon {
  width: 100rpx;
  height: 100rpx;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 15rpx;
  color: white;
  font-size: 48rpx;
}

.link-text {
  font-size: 28rpx;
  color: #333;
  text-align: center;
}

/* 适配小屏幕设备 */
@media screen and (max-width: 375px) {
  .link-item {
    width: 45%;
  }
}
</style>