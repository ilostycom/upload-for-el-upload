<template>
  <!-- <UploadForElUpload v-model="file" /> -->
  <div>11111</div>

  <el-form>
    <el-form-item label="文件">
      <UploadForElUpload
        v-model="file"
        :previewBoxStyle="previewBoxStyle"
        :acceptTypeList="acceptTypeList"
        :uploadSuccess="uploadSuccess"
        tips="请上传png,jpg格式图片"
        action="http://localhost/test.php"
      ></UploadForElUpload>
      <p>上传文件地址：{{ file }}</p>
      <!-- <UploadPreview :url="file" :previewBoxStyle="previewBoxStyle"></UploadPreview> -->
    </el-form-item>
  </el-form>
</template>

<script setup>
import UploadForElUpload from "./components/UploadForElUpload.vue";
import "element-plus/dist/index.css";
// import UploadPreview from './components/UploadPreview.vue';
import { ref } from "vue";
import { ElForm, ElFormItem } from "element-plus";

const file = ref([
  "https://earth-rt.chengji-inc.com/market/open/2024-04-18/eb1979d9-041e-49ff-a468-caaab736bb1b.png",
  "http://localhost/test.jpg",
]);
// const file = ref('http://earth-rt-test.oss-cn-beijing.aliyuncs.com/c3d205cf-9970-4c7b-8a08-73e06f7d649b.mp4');
const previewBoxStyle = {
  width: "100px",
  height: "100px",
};

const uploadSuccess = (response, uploadFile, uploadFiles) => {
  console.log(response, uploadFile, uploadFiles);
  return response.src;
};

const acceptTypeList = ["image/jpeg"];
console.log(file.value);
</script>
