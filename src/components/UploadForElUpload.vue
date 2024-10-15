<template>
  <el-upload :action="action" :headers="headers" :multiple="multiple" :data="data" :name="name"
    :on-success="handleSuccess" :file-list="fileList" :limit="limit">
    <el-button size="small" type="primary">上传</el-button>


  </el-upload>
  <UploadPreview v-if="typeof modelValue === 'string'" url="modelValue"></UploadPreview>
  <template v-if="Array.isArray(modelValue)">
    <UploadPreview v-for="(url, index) in modelValue" :key="index" :url="url"></UploadPreview>
  </template>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';
import { ElUpload, ElButton } from 'element-plus';
import UploadPreview from './UploadPreview.vue';

const fileList = ref([]);
defineProps({
  modelValue: [String, Array],
  previewBoxStyle: Object,
  uploadSuccess: Function,
  acceptTypeList: Array,
  action: String,
  headers: Array,
  multiple: Boolean,
  data: [Object, Function],
  name: String,
  onPreview: Function,
  limit: Number,
  setup(props) {
    console.log(props);
  },
});

// console.log(uploadSuccess);


const emit = defineEmits(['update:modelValue']);
const handleSuccess = (response, uploadFile, uploadFiles) => {
  if (response.exception) {
    console.log(uploadFile, uploadFiles);
    updateModel('exception');
  }

  // const value = props.uploadSuccess(response, uploadFile, uploadFiles);
  // if (value !== false) {
  //   updateModel(value);
  // }
};

function updateModel(value) {
  emit('update:modelValue', value);
}
</script>