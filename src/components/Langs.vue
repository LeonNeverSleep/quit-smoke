<template>
  <div class="langs-container">
    <div class="lang-item">
      <span>1年以下</span>
      <img src="../assets/img/lang1.png" alt="" />
    </div>
    <div class="lang-item">
      <span>1-3年</span>
      <img src="../assets/img/lang2.png" alt="" />
    </div>
    <div class="lang-item">
      <span> 3-8年 </span>
      <img src="../assets/img/lang3.png" alt="" />
    </div>
    <div class="lang-item">
      <span> 8年以上 </span>
      <img src="../assets/img/lang4.png" alt="" />
    </div>
  </div>
</template>
<script setup lang="ts"></script>
<style scoped>
.langs-container {
  display: flex;
  gap: 10px;
  margin-bottom: 50px;
  margin-top: 50px;
}
img {
  width: 100px;
  height: 100px;
}
.lang-item {
  display: flex;
  flex-direction: column-reverse;
  align-items: center;
}
</style>
