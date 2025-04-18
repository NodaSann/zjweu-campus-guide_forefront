<template>
  <view class="publish-container">
    <!-- 顶部标题 -->
    <view class="publish-header">
      <text class="publish-title">发布物品</text>
    </view>
    
    <!-- 发布表单 -->
    <view class="publish-form">
      <!-- 标题输入 -->
      <view class="form-item">
        <text class="form-label">标题</text>
        <input class="form-input" type="text" v-model="formData.title" placeholder="请输入标题" />
      </view>
      
      <!-- 描述输入 -->
      <view class="form-item">
        <text class="form-label">描述</text>
        <textarea class="form-textarea" v-model="formData.description" placeholder="请输入物品描述" />
      </view>
      
      <!-- 联系方式 -->
      <view class="form-item">
        <text class="form-label">联系方式</text>
        <input class="form-input" type="text" v-model="formData.contact" placeholder="请输入联系方式" />
      </view>
      
      <!-- 地点 -->
      <view class="form-item">
        <text class="form-label">地点</text>
        <input class="form-input" type="text" v-model="formData.location" placeholder="请输入地点" />
      </view>
      
      <!-- 上传图片 -->
      <view class="form-item">
        <text class="form-label">上传图片</text>
        <view class="upload-box" @click="chooseImage">
          <view v-if="!formData.image" class="upload-placeholder">
            <text class="upload-icon">+</text>
            <text class="upload-text">上传图片</text>
          </view>
          <image
            v-else
            class="preview-image"
            :src="formData.image"
            mode="aspectFill"
            :lazy-load="true"
            :srcset="formData.image + ' 1x, ' + formData.image + ' 2x'"
          ></image>
        </view>
      </view>
      
      <!-- 提交按钮 -->
      <button class="submit-button" @click="submitForm">发布</button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        title: '',
        description: '',
        contact: '',
        location: '',
        image: '',
        type: 'lost' // 默认为失物
      }
    }
  },
  methods: {
    chooseImage() {
      uni.chooseImage({
        count: 1,
        success: (res) => {
          this.formData.image = res.tempFilePaths[0];
        }
      });
    },
    submitForm() {
      // 表单验证
      if (!this.formData.title) {
        uni.showToast({
          title: '请输入标题',
          icon: 'none'
        });
        return;
      }
      
      if (!this.formData.description) {
        uni.showToast({
          title: '请输入描述',
          icon: 'none'
        });
        return;
      }
      
      if (!this.formData.contact) {
        uni.showToast({
          title: '请输入联系方式',
          icon: 'none'
        });
        return;
      }
      
      // 模拟提交
      uni.showLoading({
        title: '发布中...'
      });
      
      setTimeout(() => {
        uni.hideLoading();
        uni.showToast({
          title: '发布成功',
          icon: 'success'
        });
        
        // 返回上一页
        setTimeout(() => {
          uni.navigateBack();
        }, 1500);
      }, 1000);
    }
  }
}
</script>

<style>
.publish-container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  background-color: #f5f5f5;
  padding: 20rpx;
}

/* 顶部标题 */
.publish-header {
  padding: 20rpx;
  text-align: center;
  background-color: #6A87AD;
  border-radius: 15rpx;
  margin-bottom: 20rpx;
}

.publish-title {
  font-size: 36rpx;
  font-weight: bold;
  color: white;
}

/* 表单样式 */
.publish-form {
  background-color: #fff;
  border-radius: 15rpx;
  padding: 30rpx;
  box-shadow: 0 2rpx 10rpx rgba(0, 0, 0, 0.05);
}

.form-item {
  margin-bottom: 30rpx;
}

.form-label {
  display: block;
  font-size: 28rpx;
  color: #333;
  margin-bottom: 15rpx;
  font-weight: 500;
}

.form-input {
  width: 100%;
  height: 80rpx;
  background-color: #f8f8f8;
  border-radius: 10rpx;
  padding: 0 20rpx;
  font-size: 28rpx;
  color: #333;
}

.form-textarea {
  width: 100%;
  height: 200rpx;
  background-color: #f8f8f8;
  border-radius: 10rpx;
  padding: 20rpx;
  font-size: 28rpx;
  color: #333;
}

/* 上传图片 */
.upload-box {
  width: 100%;
  aspect-ratio: 16/9;
  background-color: #f8f8f8;
  border-radius: 10rpx;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  position: relative;
}

.upload-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.upload-icon {
  font-size: 60rpx;
  color: #ccc;
  margin-bottom: 10rpx;
}

.upload-text {
  font-size: 28rpx;
  color: #999;
}

.preview-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 10rpx;
  display: block;
  /* 支持高分屏 */
  image-rendering: -webkit-optimize-contrast;
  image-rendering: crisp-edges;
}

/* 提交按钮 */
.submit-button {
  width: 100%;
  height: 90rpx;
  background-color: #6A87AD;
  color: white;
  border-radius: 45rpx;
  font-size: 32rpx;
  font-weight: bold;
  margin-top: 20rpx;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>