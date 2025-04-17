<template>
  <view class="guide-container">
    <!-- 顶部标题 -->
    <view class="guide-header">
      <text class="guide-title">导览服务</text>
    </view>
    
    <!-- 导航标签栏 -->
    <view class="guide-tabs">
      <view class="campus-selector">
        <text class="campus-icon">📍</text>
        <text class="campus-text">钱塘校区</text>
      </view>
      <scroll-view class="category-list" scroll-x="true" show-scrollbar="false" enhanced="true" :scroll-with-animation="true">
        <view class="category-wrapper">
          <view class="category-item" :class="{ active: currentCategory === '出入口' }" @click="selectCategory('出入口')">出入口</view>
          <text class="category-divider">|</text>
          <view class="category-item" :class="{ active: currentCategory === '食堂' }" @click="selectCategory('食堂')">食堂</view>
          <text class="category-divider">|</text>
          <view class="category-item" :class="{ active: currentCategory === '景点' }" @click="selectCategory('景点')">景点</view>
          <text class="category-divider">|</text>
          <view class="category-item" :class="{ active: currentCategory === '学院' }" @click="selectCategory('学院')">学院</view>
          <text class="category-divider">|</text>
          <view class="category-item" :class="{ active: currentCategory === '超市' }" @click="selectCategory('超市')">超市</view>
          <text class="category-divider">|</text>
          <view class="category-item" :class="{ active: currentCategory === '校门' }" @click="selectCategory('校门')">校门</view>
          <text class="category-divider">|</text>
          <view class="category-item" :class="{ active: currentCategory === '快递' }" @click="selectCategory('快递')">快递</view>
        </view>
      </scroll-view>
    </view>
    
    <!-- 地图区域 -->
    <view class="map-container">
      <text class="map-placeholder">地图界面</text>
      <!-- 实际项目中这里应该是地图组件 -->
      <!-- <map :latitude="latitude" :longitude="longitude" :markers="markers"></map> -->
      
    </view>
    
    <!-- 底部导航栏 -->
    <view class="bottom-nav">
      <view class="route-selection">
        <view class="route-point">
          <text class="point-label">当前起点</text>
        </view>
        <view class="route-point">
          <text class="point-label">请选择终点</text>
        </view>
      </view>
      
      <view class="direction-icon">
        <text class="direction-arrow">↑↓</text>
      </view>
      
      <view class="plan-route-btn">
        <text>规划路线</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      // 地图相关数据
      latitude: 30.123456,
      longitude: 120.123456,
      markers: [],
      currentCategory: '出入口' // 默认选中的分类
    }
  },
  onLoad() {
    // 页面加载时初始化地图数据
    this.initMapData();
  },
  methods: {
    initMapData() {
      // 初始化地图数据
      // 实际项目中这里应该从服务器获取地图标记点等数据
      this.markers = [
        {
          id: 1,
          latitude: 30.123456,
          longitude: 120.123456,
          title: '图书馆'
        },
        {
          id: 2,
          latitude: 30.123556,
          longitude: 120.123556,
          title: '学生中心'
        }
      ];
    },
    // 选择分类
    selectCategory(category) {
      this.currentCategory = category;
      // 这里可以根据选中的分类加载对应的地图标记点
    }
  }
}
</script>

<style>
.guide-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  background-color: #f5f5f5;
}

/* 顶部标题 */
.guide-header {
  padding: 20rpx;
  text-align: center;
  background-color: #fff;
  border-bottom: 1px solid #eee;
}

.guide-title {
  font-size: 36rpx;
  font-weight: bold;
  color: #333;
}

/* 导航标签栏 */
.guide-tabs {
  background-color: #fff;
  padding: 20rpx;
  border-bottom: 1px solid #eee;
}

.campus-selector {
  display: flex;
  align-items: center;
  margin-bottom: 20rpx;
}

.campus-icon {
  margin-right: 10rpx;
  color: #6A87AD;
}

.campus-text {
  font-size: 28rpx;
  color: #333;
  font-weight: bold;
}

.category-list {
  white-space: nowrap;
}

.category-wrapper {
  display: inline-flex;
  align-items: center;
}

.category-item {
  display: inline-block;
  padding: 10rpx 20rpx;
  font-size: 28rpx;
  color: #666;
}

.category-item.active {
  color: #6A87AD;
  font-weight: bold;
}

.category-divider {
  color: #eee;
  margin: 0 5rpx;
}

/* 地图区域 */
.map-container {
  flex: 1;
  position: relative;
  background-color: #eee;
  display: flex;
  justify-content: center;
  align-items: center;
}

.map-placeholder {
  color: #999;
  font-size: 32rpx;
}

/* 底部导航栏 */
.bottom-nav {
  background-color: #fff;
  padding: 20rpx;
  display: flex;
  align-items: center;
  border-top: 1px solid #eee;
}

.route-selection {
  flex: 1;
}

.route-point {
  padding: 10rpx 0;
}

.point-label {
  font-size: 28rpx;
  color: #666;
}

.direction-icon {
  width: 60rpx;
  height: 60rpx;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 20rpx;
}

.direction-arrow {
  color: #6A87AD;
  font-size: 32rpx;
}

.plan-route-btn {
  background-color: #6A87AD;
  color: white;
  padding: 15rpx 30rpx;
  border-radius: 30rpx;
  font-size: 28rpx;
}
</style>