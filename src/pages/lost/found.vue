<template>
  <view class="lost-found-container">
    <!-- 顶部标题 -->
    <view class="lost-found-header">
      <text class="lost-found-title">失物招领</text>
    </view>
    
    <!-- 搜索栏 -->
    <view class="search-bar">
      <view class="search-input">
        <text class="search-icon">🔍</text>
        <input type="text" placeholder="查找" confirm-type="search" />
      </view>
      <view class="add-button" @click="navigateToPublish">
        <text class="add-icon">+</text>
      </view>
    </view>
    
    <!-- 分类标签 -->
    <view class="category-tabs">
      <view class="tab" :class="{active: activeTab === 'all'}" @click="setActiveTab('all')">
        <text>全部</text>
      </view>
      <view class="tab" :class="{active: activeTab === 'lost'}" @click="setActiveTab('lost')">
        <text>失物</text>
      </view>
      <view class="tab" :class="{active: activeTab === 'found'}" @click="setActiveTab('found')">
        <text>寻物</text>
      </view>
    </view>
    
    <!-- 物品列表 -->
    <view class="item-list">
      <view class="item-card" v-for="(item, index) in items" :key="index" @click="navigateToDetail(item)">
        <view class="item-color-block" :style="{backgroundColor: item.color}"></view>
        <view class="item-content">
          <text class="item-title">{{ item.title }}</text>
          <text class="item-date">{{ item.date }}</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      activeTab: 'all',
      items: [
        { id: 1, title: '找到一部手机', color: '#9FEAA8', date: '2025/4/17', type: 'found', description: '在图书馆二楼自习室找到一部黑色手机，联系我认领。' },
        { id: 2, title: '丢失一个篮球', color: '#FFE699', date: '2025/4/17', type: 'lost', description: '在篮球场丢失一个蓝色篮球，有看到的请联系我。' },
        { id: 3, title: '食堂看到饭卡一张', color: '#B6DCFE', date: '2025/4/17', type: 'found', description: '在第一食堂二楼看到一张饭卡，失主请联系我认领。' },
        { id: 4, title: '操场丢失学生证', color: '#FFB6B6', date: '2025/4/17', type: 'lost', description: '在操场跑步时丢失学生证，有捡到的请联系我。' }
      ]
    }
  },
  methods: {
    setActiveTab(tab) {
      this.activeTab = tab;
    },
    navigateToDetail(item) {
      uni.navigateTo({
        url: `/pages/lost/detail?id=${item.id}&type=${item.type}`
      })
    },
    navigateToPublish() {
      uni.navigateTo({
        url: '/pages/lost/publish'
      })
    }
  }
}
</script>

<style>
.lost-found-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #f5f5f5;
  padding: 20rpx;
}

/* 顶部标题 */
.lost-found-header {
  padding: 20rpx;
  text-align: center;
  background-color: #6A87AD;
  border-radius: 15rpx;
  margin-bottom: 20rpx;
}

.lost-found-title {
  font-size: 36rpx;
  font-weight: bold;
  color: white;
}

/* 搜索栏 */
.search-bar {
  display: flex;
  align-items: center;
  margin-bottom: 20rpx;
}

.search-input {
  flex: 1;
  display: flex;
  align-items: center;
  background-color: #fff;
  border-radius: 30rpx;
  padding: 15rpx 20rpx;
  margin-right: 15rpx;
}

.search-icon {
  font-size: 30rpx;
  color: #999;
  margin-right: 10rpx;
}

.add-button {
  width: 70rpx;
  height: 70rpx;
  background-color: #9CB4CC;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.add-icon {
  color: white;
  font-size: 40rpx;
  font-weight: bold;
}

/* 分类标签 */
.category-tabs {
  display: flex;
  background-color: #fff;
  border-radius: 15rpx;
  margin-bottom: 20rpx;
  overflow: hidden;
}

.tab {
  flex: 1;
  text-align: center;
  padding: 20rpx 0;
  font-size: 28rpx;
  color: #666;
  position: relative;
}

.tab.active {
  color: #6A87AD;
  font-weight: bold;
}

.tab.active::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 40rpx;
  height: 6rpx;
  background-color: #6A87AD;
  border-radius: 3rpx;
}

/* 物品列表 */
.item-list {
  flex: 1;
}

.item-card {
  display: flex;
  background-color: #fff;
  border-radius: 15rpx;
  margin-bottom: 20rpx;
  overflow: hidden;
  box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.item-color-block {
  width: 80rpx;
  height: auto;
  border-top-left-radius: 15rpx;
  border-bottom-left-radius: 15rpx;
}

.item-content {
  flex: 1;
  padding: 20rpx;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.item-title {
  font-size: 30rpx;
  color: #333;
  font-weight: 500;
}

.item-date {
  font-size: 24rpx;
  color: #999;
}
</style>