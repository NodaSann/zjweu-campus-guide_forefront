<template>
  <view class="guide-container">
    <!-- 顶部标题 -->
    <view class="guide-header">
      <text class="guide-title">校园指南</text>
    </view>
    
    <!-- 指南列表 -->
    <view class="guide-list">
      <view class="guide-item" v-for="(item, index) in guideItems" :key="index" @click="navigateToDetail(item)">
        <view class="guide-icon">
          <text class="icon-light">💡</text>
        </view>
        <view class="guide-content">
          <text class="guide-name">{{ item.name }}</text>
        </view>
        <text class="guide-arrow">》</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      guideItems: [
        { id: 1, name: '水院导航', icon: '💡', path: '/pages/campus/detail', type: 'navigation' },
        { id: 2, name: '作息时间', icon: '💡', path: '/pages/campus/detail', type: 'schedule' },
        { id: 3, name: '快递收发', icon: '💡', path: '/pages/campus/detail', type: 'express' },
        { id: 4, name: '综合楼', icon: '💡', path: '/pages/campus/detail', type: 'building' },
        { id: 5, name: '教学楼', icon: '💡', path: '/pages/campus/detail', type: 'classroom' },
        { id: 6, name: '食堂', icon: '💡', path: '/pages/campus/detail', type: 'canteen' },
        { id: 7, name: '门禁', icon: '💡', path: '/pages/campus/detail', type: 'access' },
        { id: 8, name: '水电充值', icon: '💡', path: '/pages/campus/detail', type: 'utility' }
      ]
    }
  },
  methods: {
    navigateToDetail(item) {
      uni.navigateTo({
        url: `${item.path}?id=${item.id}&type=${item.type}`
      })
    }
  }
}
</script>

<style>
.guide-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #f5f5f5;
  padding: 20rpx;
}

/* 顶部标题 */
.guide-header {
  padding: 20rpx;
  text-align: center;
  background-color: #6A87AD;
  border-radius: 15rpx;
  margin-bottom: 20rpx;
}

.guide-title {
  font-size: 36rpx;
  font-weight: bold;
  color: white;
}

/* 指南列表 */
.guide-list {
  background-color: #fff;
  border-radius: 15rpx;
  overflow: hidden;
  box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.guide-item {
  display: flex;
  align-items: center;
  padding: 30rpx 20rpx;
  border-bottom: 1px solid #eee;
  transition: background-color 0.3s;
}

.guide-item:active {
  background-color: #f8f8f8;
}

.guide-item:last-child {
  border-bottom: none;
}

.guide-icon {
  width: 60rpx;
  height: 60rpx;
  border-radius: 50%;
  background-color: #9CB4CC;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 20rpx;
}

.icon-light {
  color: white;
  font-size: 36rpx;
}

.guide-content {
  flex: 1;
}

.guide-name {
  font-size: 30rpx;
  color: #333;
  font-weight: 500;
}

.guide-arrow {
  color: #B6DCFE;
  font-size: 30rpx;
}
</style>