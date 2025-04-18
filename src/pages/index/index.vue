<template>
  <view class="container">
    <!-- 顶部天气栏 -->
    <view class="weather-bar">
      <view class="weather-info">
        <text class="weather-icon">☀️</text>
        <text class="weather-text">今日天气: 晴 26°C</text>
      </view>
      <view class="search-icon">
        <text class="iconfont">🔍</text>
      </view>
    </view>

    <!-- 快捷功能区 -->
    <view class="quick-nav">
      <view class="nav-item" v-for="(item, index) in quickNavItems" :key="index" @click="handleNavClick(item)">
        <view class="nav-icon" :style="{ backgroundColor: item.bgColor }">
          <text class="iconfont">{{ item.icon }}</text>
        </view>
        <text class="nav-text">{{ item.text }}</text>
      </view>
    </view>

    <!-- 热门地点 -->
    <view class="section">
      <view class="section-header">
        <text class="section-title">热门地点</text>
        <text class="view-all" @click="viewAll('hotspot')">查看全部</text>
      </view>
      <view class="hotspot-list">
        <view class="hotspot-item" v-for="(item, index) in hotspots" :key="index">
          <image
            class="hotspot-image"
            :src="item.image"
            mode="aspectFill"
            :lazy-load="true"
            :srcset="item.image + ' 1x, ' + item.image + ' 2x'"
          ></image>
          <view class="hotspot-info">
            <text class="hotspot-name">{{ item.name }}</text>
            <text class="hotspot-time">{{ item.time }}</text>
          </view>
        </view>
      </view>
    </view>

    <!-- 近期活动 -->
    <view class="section">
      <view class="section-header">
        <text class="section-title">近期活动</text>
        <text class="view-all" @click="viewAll('activity')">查看全部</text>
      </view>
      <view class="activity-list">
        <view class="activity-item" v-for="(item, index) in activities" :key="index">
          <view class="activity-date">
            <text class="date-day">{{ item.day }}</text>
            <text class="date-month">{{ item.month }}月</text>
          </view>
          <view class="activity-content">
            <text class="activity-title">{{ item.title }}</text>
            <view class="activity-location">
              <text class="location-icon">📍</text>
              <text class="location-text">{{ item.location }}</text>
            </view>
            <text class="activity-time">{{ item.time }}</text>
          </view>
        </view>
      </view>
    </view>

    <!-- 相关链接弹窗 -->
    <view class="links-container" v-if="showLinksPopup">
      <!-- 半透明背景 -->
      <view class="mask" @click="closeLinksPopup"></view>
      
      <!-- 弹窗内容 -->
      <view class="popup-content">
        <view class="popup-header">
          <text class="popup-title">相关链接</text>
          <text class="close-btn" @click="closeLinksPopup">×</text>
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
  </view>
</template>

<script>
export default {
  data() {
    return {
      showLinksPopup: false,
      quickNavItems: [
        { icon: '📚', text: '导览服务', bgColor: '#6A87AD', path: '/pages/guide/navigate' },
        { icon: '📋', text: '校园指南', bgColor: '#9CB4CC', path: '/pages/campus/guide' },
        { icon: '🔍', text: '失物招领', bgColor: '#9CB4CC', path: '/pages/lost/found' },
        { icon: '🔗', text: '相关链接', bgColor: '#B6DCFE', isPopup: true }
      ],
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
      ],
      hotspots: [
        { 
          name: '中央图书馆', 
          image: '/static/library.jpg', 
          time: '8:00-22:00' 
        },
        { 
          name: '学生食堂', 
          image: '/static/canteen.jpg', 
          time: '6:30-20:00' 
        }
      ],
      activities: [
        {
          day: '15',
          month: '5',
          title: '校园文化节开幕式',
          location: '百年纪念礼堂',
          time: '19:00-21:00'
        },
        {
          day: '18',
          month: '5',
          title: '学术讲座：人工智能的未来',
          location: '科技楼报告厅',
          time: '14:30-16:30'
        }
      ]
    }
  },
  onLoad() {
    // 页面加载时可以获取实时天气数据
  },
  methods: {
    // 处理导航点击
    handleNavClick(item) {
      if (item.isPopup) {
        this.showLinksPopup = true;
      } else {
        this.navigateTo(item.path);
      }
    },
    
    // 关闭相关链接弹窗
    closeLinksPopup() {
      this.showLinksPopup = false;
    },
    
    // 打开链接
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
      
      this.closeLinksPopup();
    },
    
    viewAll(type) {
      // 查看全部功能
      uni.navigateTo({
        url: `/pages/${type}/list`
      })
    },
    navigateTo(path) {
      uni.navigateTo({
        url: path
      })
    }
  }
}
</script>

<style>
.container {
  padding: 20rpx;
  background-color: #f5f5f5;
}

/* 顶部天气栏 */
.weather-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #6A87AD;
  color: white;
  padding: 20rpx 30rpx;
  border-radius: 15rpx;
  margin-bottom: 20rpx;
}

.weather-info {
  display: flex;
  align-items: center;
}

.weather-icon {
  font-size: 40rpx;
  margin-right: 10rpx;
}

.weather-text {
  font-size: 28rpx;
}

.search-icon {
  font-size: 40rpx;
}

/* 快捷功能区 */
.quick-nav {
  display: flex;
  justify-content: space-between;
  margin-bottom: 30rpx;
  background-color: white;
  border-radius: 15rpx;
  padding: 30rpx 20rpx;
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 25%;
}

.nav-icon {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10rpx;
  color: white;
  font-size: 40rpx;
}

.nav-text {
  font-size: 24rpx;
  color: #333;
}

/* 热门地点和近期活动公共样式 */
.section {
  background-color: white;
  border-radius: 15rpx;
  padding: 20rpx;
  margin-bottom: 20rpx;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20rpx;
}

.section-title {
  font-size: 32rpx;
  font-weight: bold;
  color: #333;
}

.view-all {
  font-size: 24rpx;
  color: #6A87AD;
}

/* 热门地点样式 */
.hotspot-list {
  display: flex;
  flex-wrap: nowrap;
  overflow-x: auto;
  white-space: nowrap;
  padding-bottom: 10rpx;
  gap: 10rpx; /* 缩小间距以适配小屏 */
  padding-left: 5rpx;
  padding-right: 5rpx;
}

.hotspot-item {
  width: 45vw; /* 保证320px屏幕也能一行显示两个 */
  min-width: 140rpx;
  max-width: 200px;
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #fff;
  border-radius: 10rpx;
  box-sizing: border-box;
  /* 可选：加点阴影提升卡片感 */
  /* box-shadow: 0 2rpx 8rpx rgba(0,0,0,0.04); */
}

.hotspot-image {
  width: 100%;
  aspect-ratio: 1/1; /* 正方形比例 */
  max-height: 50vw;  /* 限制最大高度为容器宽度，保证正方形 */
  max-width: 50vw;
  border-radius: 10rpx 10rpx 0 0;
  object-fit: cover;
  display: block;
  background: #f0f0f0;
  /* 支持高分屏 */
  image-rendering: -webkit-optimize-contrast;
  image-rendering: crisp-edges;
}

.hotspot-name {
  font-size: 28rpx;
  color: #333;
  display: block;
}

.hotspot-time {
  font-size: 24rpx;
  color: #999;
}

@media (max-width: 500px) {
  .hotspot-item {
    width: 45vw;
    min-width: 45vw;
    max-width: 45vw;
  }
  .hotspot-image {
    aspect-ratio: 16/9;
  }
}

/* 近期活动样式 */
.activity-list {
  display: flex;
  flex-direction: column;
}

.activity-item {
  display: flex;
  margin-bottom: 20rpx;
  padding-bottom: 20rpx;
  border-bottom: 1rpx solid #eee;
}

.activity-date {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100rpx;
  height: 100rpx;
  background-color: #B6DCFE;
  border-radius: 10rpx;
  margin-right: 20rpx;
}

.date-day {
  font-size: 36rpx;
  font-weight: bold;
  color: #333;
}

.date-month {
  font-size: 24rpx;
  color: #666;
}

.activity-content {
  flex: 1;
}

.activity-title {
  font-size: 28rpx;
  font-weight: bold;
  color: #333;
  margin-bottom: 10rpx;
}

.activity-location {
  display: flex;
  align-items: center;
  margin-bottom: 5rpx;
}

.location-icon {
  font-size: 24rpx;
  margin-right: 5rpx;
}

.location-text {
  font-size: 24rpx;
  color: #666;
}

.activity-time {
  font-size: 24rpx;
  color: #999;
}

/* 相关链接弹窗样式 */
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
