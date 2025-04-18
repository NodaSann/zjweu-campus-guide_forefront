<template>
  <view class="detail-container">
    <!-- 顶部标题 -->
    <view class="detail-header">
      <text class="detail-title">{{ detailTitle }}</text>
    </view>
    
    <!-- 快递收发详情 -->
    <view class="detail-content" v-if="type === 'express'">
      <view class="detail-section">
        <text class="section-title">快递</text>
        
        <view class="info-item">
          <text class="info-label">营业时间：</text>
          <text class="info-value">8:30 - 19:00</text>
        </view>
        
        <view class="info-item">
          <text class="info-label">收发地址：</text>
          <text class="info-value">广西壮族自治区桂林市雁山区雁中路3号桂林学院</text>
        </view>
        
        <view class="info-item">
          <text class="info-label">校内快递点：</text>
          <text class="info-value">百世 | 圆通 | 申通 | 京东 | 中通 | 韵达 | 顺丰</text>
        </view>
        
        <view class="info-text">
          快递站均在东西宿舍楼对面，位置醒目。
        </view>
        
        <view class="info-item">
          <text class="info-label">校外快递点：</text>
          <text class="info-value">邮政快递</text>
        </view>
        
        <view class="info-text">
          位于北门对面西侧加州旅馆旁，有点远，建议在其他家收发快递。
        </view>
      </view>
      
      <view class="express-image">
        <image
          src="/static/express.jpg"
          mode="aspectFill"
          :lazy-load="true"
          srcset="/static/express.jpg 1x, /static/express.jpg 2x"
          class="express-img"
        ></image>
      </view>
    </view>
    
    <!-- 其他类型的详情页 -->
    <view class="detail-content" v-else>
      <view class="placeholder">
        <text>{{ type }}详情内容正在完善中...</text>
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
      detailTitle: '详情',
      detailData: {}
    }
  },
  onLoad(options) {
    this.id = options.id;
    this.type = options.type;
    this.loadDetailData();
  },
  methods: {
    loadDetailData() {
      // 根据type和id加载不同的详情数据
      switch(this.type) {
        case 'navigation':
          this.detailTitle = '水院导航';
          break;
        case 'schedule':
          this.detailTitle = '作息时间';
          break;
        case 'express':
          this.detailTitle = '快递收发';
          break;
        case 'building':
          this.detailTitle = '综合楼';
          break;
        case 'classroom':
          this.detailTitle = '教学楼';
          break;
        case 'canteen':
          this.detailTitle = '食堂';
          break;
        case 'access':
          this.detailTitle = '门禁';
          break;
        case 'utility':
          this.detailTitle = '水电充值';
          break;
        default:
          this.detailTitle = '详情';
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

/* 详情内容 */
.detail-content {
  background-color: #fff;
  border-radius: 15rpx;
  padding: 30rpx;
  box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.detail-section {
  margin-bottom: 30rpx;
}

.section-title {
  font-size: 32rpx;
  font-weight: bold;
  color: #6A87AD;
  margin-bottom: 20rpx;
  display: block;
  border-left: 8rpx solid #9CB4CC;
  padding-left: 15rpx;
}

.info-item {
  margin-bottom: 15rpx;
}

.info-label {
  font-size: 28rpx;
  color: #333;
  font-weight: bold;
}

.info-value {
  font-size: 28rpx;
  color: #666;
}

.info-text {
  font-size: 28rpx;
  color: #666;
  line-height: 1.6;
  margin-bottom: 20rpx;
}

.express-image {
  margin-top: 30rpx;
  border-radius: 15rpx;
  overflow: hidden;
  box-shadow: 0 4rpx 12rpx rgba(0, 0, 0, 0.1);
  width: 100%;
  aspect-ratio: 16/9;
  background: #f0f0f0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.express-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  border-radius: 15rpx;
  /* 支持高分屏 */
  image-rendering: -webkit-optimize-contrast;
  image-rendering: crisp-edges;
}

.placeholder {
  padding: 100rpx 0;
  text-align: center;
  color: #999;
  font-size: 28rpx;
  background-color: #f8f8f8;
  border-radius: 10rpx;
  border: 1rpx dashed #B6DCFE;
}
</style>