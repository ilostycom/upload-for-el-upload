<template>
  <!-- <UploadForElUpload v-model="file" /> -->
  <div>11111</div>

  <UploadForElUpload v-model="file" :previewBoxStyle="previewBoxStyle" :acceptTypeList="acceptTypeList" :uploadSuccess="uploadSuccess"></UploadForElUpload>
  <p>上传文件地址：{{ file }}</p>
</template>

<script setup>

import UploadForElUpload from './components/UploadForElUpload.vue';
// import UploadPreview from './components/UploadPreview.vue';
import { ref } from 'vue';


const file = ref('https://earth-rt.chengji-inc.com/market/open/2024-04-18/eb1979d9-041e-49ff-a468-caaab736bb1b.png');
// const file = ref('http://earth-rt-test.oss-cn-beijing.aliyuncs.com/c3d205cf-9970-4c7b-8a08-73e06f7d649b.mp4');
const previewBoxStyle = {
  width: "800px",
  height: "600px",
};

const uploadSuccess = () => {
  return file.value;
};

const acceptTypeList = [
  'image/jpeg',
];
console.log(file.value)

</script>