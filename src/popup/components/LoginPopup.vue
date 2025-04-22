<template>
    <div class="login-popup">
      <div class="login-header">
        <h2>登录</h2>
        <button @click="closeLogin">关闭</button>
      </div>
      <div class="login-content">
        <!-- 这里可以添加登录表单，例如用户名、密码输入框 -->
        <input type="text" placeholder="用户名"  style="width: 90%"/>
        <input type="password" placeholder="密码" style="width: 90%"/>
        <button>登录</button>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref,defineEmits  } from 'vue';
  console.log(ref,'ref');
  const emits = defineEmits(['close']);
  const closeLogin = () => {
    // 这里可以触发关闭登录弹窗的逻辑
    emits('close');
    console.log('关闭登录弹窗');
  };
  </script>
  
  <style scoped lang="less">
  .login-popup {
    position: fixed;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 300px;
    background-color: #fff;
    border: 1px solid #e2e8f0;
    border-radius: 8px 8px 0 0;
    padding: 16px;
    box-shadow: 0 -4px 6px -1px rgba(0, 0, 0, 0.1), 0 -2px 4px -1px rgba(0, 0, 0, 0.06);
    z-index: 1000;
  }
  
  .login-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;
  }
  
  .login-header h2 {
    font-size: 20px;
    font-weight: 600;
    color: #2d3748;
  }
  
  .login-header button {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 18px;
    color: #718096;
  }
  
  .login-content input {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #e2e8f0;
    border-radius: 4px;
  }
  
  .login-content button {
    width: 100%;
    padding: 12px;
    background-color: #4299e1;
    color: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  
    &:hover {
      background-color: #3182ce;
    }
  }
  </style>