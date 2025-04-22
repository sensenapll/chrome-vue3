<template>
  <div class="plugin-box">
    <div class="plugin-header">
      <span class="plugin-title">测试插件111222</span>
      <div class="switch-wrapper">
        <span>激活/禁用</span>
        <input type="checkbox" v-model="active" @change="handleChange" :disabled="isLoading" class="custom-toggle">
      </div>
    </div>
    <ul class="function-list">
      <li v-for="(item, index) in functionItems" :key="index" class="function-item" @click="handleFunctionClick(item)">
        <img :src="item.icon" alt="item.name" class="function-icon">
        <span>{{ item.name }}</span>
        <img v-if="item.hasArrow" src="../../icons/food-strawberry.png" alt="箭头" class="arrow-icon">
        <span v-if="item.versionTag" class="version-tag">{{ item.versionTag }}</span>
      </li>
    </ul>
    <a href="#" class="login-btn" @click.prevent="openLogin">立即登录</a>
    <p v-if="statusMessage" class="status-message">{{ statusMessage }}</p>
    <LoginPopup v-if="isLoginPopupVisible" @close="closeLogin" />
  </div>
</template>

<script setup lang="ts">
import { useCounterStore } from '../store/counter';
import { ref } from 'vue';
import LoginPopup from './LoginPopup.vue';

// 引入计数器存储
const store = useCounterStore();
console.log(store, 'store');

// 定义激活状态
const active = ref(false);
// 定义加载状态
const isLoading = ref(false);
// 定义状态消息
const statusMessage = ref('');
// 定义登录弹窗显示状态
const isLoginPopupVisible = ref(false);

// 功能列表数据
const functionItems = [
  { name: '启动插件(打开默认首页)', icon: '../../icons/food-chips.png', hasArrow: false, versionTag: '' },
  { name: '利润计算器', icon: '../../icons/food-cookie.png', hasArrow: false, versionTag: '' },
  { name: '打开Keepa插件替代', icon: '../../icons/food-doughnut.png', hasArrow: false, versionTag: '' },
  { name: '我的收藏列表', icon: '../../icons/food-pecan.png', hasArrow: true, versionTag: '' },
  { name: '偏好设置(v4.7.5)', icon: '../../icons/food-pudding.png', hasArrow: false, versionTag: '已是最新版本' },
  { name: '帮助教程(视频讲解)', icon: '../../icons/food-strawberry.png', hasArrow: false, versionTag: '' },
  { name: 'chrome官网', icon: '../../icons/food-strawberry.png', hasArrow: false, versionTag: '' }
];

// 处理开关状态改变的函数
const handleChange = async (): Promise<void> => {
  try {
    // 开启加载状态
    isLoading.value = true;
    // 清空状态消息
    statusMessage.value = '';
    // 模拟异步操作，实际应用中可替换为真实的 API 请求
    await new Promise((resolve) => setTimeout(resolve, 500));

    // 根据开关状态显示不同的提示信息
    if (active.value) {
      statusMessage.value = '已成功激活';
    } else {
      statusMessage.value = '已成功禁用';
    }
  } catch (error: unknown) {
    // 错误处理，显示错误信息
    statusMessage.value = '操作失败，请稍后重试';
    console.error('操作失败，请稍后重试', error);
  } finally {
    // 关闭加载状态
    isLoading.value = false;
  }
};

// 处理功能项点击事件
const handleFunctionClick = (item: { name: string }) => {
  console.log(`点击了: ${item.name}`);
  // 这里可以添加具体的功能逻辑
};

// 打开登录弹窗
const openLogin = () => {
  isLoginPopupVisible.value = true;
};

// 关闭登录弹窗
const closeLogin = () => {
  isLoginPopupVisible.value = false;
};
</script>

<style lang="less">
.plugin-box {
  width: 300px;
  background-color: #fff;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  padding: 16px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
}

.plugin-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}

.plugin-title {
  font-size: 20px;
  font-weight: 600;
  color: #2d3748;
}

.switch-wrapper {
  display: flex;
  align-items: center;
}

/* 美化原生checkbox开关样式 */
.custom-toggle {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  width: 44px;
  height: 24px;
  margin-left: 12px;
  background-color: #edf2f7;
  border-radius: 12px;
  outline: none;
  cursor: pointer;
  position: relative;
  transition: background-color 0.3s ease;

  &:checked {
    background-color: #4299e1;
  }

  &::before {
    content: "";
    width: 20px;
    height: 20px;
    position: absolute;
    top: 2px;
    left: 2px;
    background-color: white;
    border-radius: 50%;
    transition: left 0.3s ease;
  }

  &:checked::before {
    left: 22px;
  }

  &:disabled {
    background-color: #e2e8f0;
    cursor: not-allowed;
  }
}

.function-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.function-item {
  display: flex;
  align-items: center;
  padding: 10px 0;
  cursor: pointer;
  transition: background-color 0.3s ease;

  &:hover {
    background-color: #f7fafc;
  }
}

.function-icon {
  height: 24px;
  margin-right: 12px;
}

.arrow-icon {
  height: 14px;
  margin-left: auto;
}

.version-tag {
  color: #48bb78;
  font-size: 12px;
  margin-left: 8px;
}

.login-btn {
  display: block;
  background-color: #4299e1;
  color: white;
  text-align: center;
  padding: 12px;
  border-radius: 6px;
  text-decoration: none;
  margin-top: 16px;
  transition: background-color 0.3s ease;

  &:hover {
    background-color: #3182ce;
  }
}

.status-message {
  margin-top: 12px;
  color: #718096;
  font-size: 14px;
  text-align: center;
}
</style>    