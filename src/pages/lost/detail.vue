<template>
  <view class="detail-container">
    <!-- 顶部标题 -->
    <view class="detail-header">
      <text class="detail-title">物品详情</text>
    </view>
    
    <!-- 物品详情内容 -->
    <view class="detail-card">
      <view class="detail-title-section">
        <text class="item-title">{{ itemDetail.title }}</text>
      </view>
      
      <!-- 物品图片 -->
      <view class="item-image-container">
        <image class="item-image" src="/static/library.jpg" mode="aspectFill"></image>
      </view>
      
      <!-- 物品描述 -->
      <view class="item-description">
        <text class="description-text">{{ itemDetail.description }}</text>
      </view>
      
      <!-- 物品信息 -->
      <view class="item-info">
        <view class="info-row">
          <text class="info-label">发布日期:</text>
          <text class="info-value">{{ itemDetail.date }}</text>
        </view>
        <view class="info-row">
          <text class="info-label">联系方式:</text>
          <text class="info-value">{{ itemDetail.contact }}</text>
        </view>
        <view class="info-row">
          <text class="info-label">地点:</text>
          <text class="info-value">{{ itemDetail.location }}</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      id: null,
      type: '',
      itemDetail: {
        title: '',
        description: '',
        date: '',
        contact: '',
        location: ''
      }
    }
  },
  onLoad(options) {
    this.id = options.id;
    this.type = options.type;
    this.loadItemDetail();
  },
  methods: {
    loadItemDetail() {
      // 模拟从服务器获取数据
      // 实际应用中应该通过API获取数据
      const mockData = {
        1: {
          title: '找到一部手机',
          description: '在图书馆二楼自习室找到一部黑色手机，联系我认领。',
          date: '2025/4/17',
          contact: '135****6789',
          location: '图书馆二楼'
        },
        2: {
          title: '丢失一个篮球',
          description: '在篮球场丢失一个蓝色篮球，有看到的请联系我。',
          date: '2025/4/17',
          contact: '138****5678',
          location: '篮球场'
        },
        3: {
          title: '食堂看到饭卡一张',
          description: '在第一食堂二楼看到一张饭卡，失主请联系我认领。',
          date: '2025/4/17',
          contact: '132****4567',
          location: '第一食堂二楼'
        },
        4: {
          title: '操场丢失学生证',
          description: '在操场跑步时丢失学生证，有捡到的请联系我。',
          date: '2025/4/17',
          contact: '139****7890',
          location: '操场'
        }
      };
      
      if (mockData[this.id]) {
        this.itemDetail = mockData[this.id];
      }
    }
  }
}
</script>

<style>
.detail-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #f5f5f5;
  padding: 20rpx;
}

/* 顶部标题 */
.detail-header {
  padding: 20rpx;
  text-align: center;
  background-color: #6A87AD;
  border-radius: 15rpx;
  margin-bottom: 20rpx;
}

.detail-title {
  font-size: 36rpx;
  font-weight: bold;
  color: white;
}

/* 详情卡片 */
.detail-card {
  background-color: #fff;
  border-radius: 15rpx;
  overflow: hidden;
  box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
  padding: 20rpx;
}

.detail-title-section {
  padding: 20rpx 0;
  border-bottom: 1px solid #eee;
  margin-bottom: 20rpx;
}

.item-title {
  font-size: 34rpx;
  font-weight: bold;
  color: #333;
}

/* 物品图片 */
.item-image-container {
  width: 100%;
  height: 400rpx;
  margin: 20rpx 0;
  border-radius: 10rpx;
  overflow: hidden;
}

.item-image {
  width: 100%;
  height: 100%;
}

/* 物品描述 */
.item-description {
  padding: 20rpx 0;
  border-bottom: 1px solid #eee;
  margin-bottom: 20rpx;
}

.description-text {
  font-size: 28rpx;
  color: #666;
  line-height: 1.6;
}

/* 物品信息 */
.item-info {
  padding: 10rpx 0;
}

.info-row {
  display: flex;
  margin-bottom: 15rpx;
}

.info-label {
  width: 150rpx;
  font-size: 28rpx;
  color: #999;
}

.info-value {
  flex: 1;
  font-size: 28rpx;
  color: #333;
}
</style>