<template>
  <el-upload
    :action="action"
    :headers="headers"
    :multiple="multiple"
    :data="data"
    :name="name"
    :on-success="handleSuccess"
    :file-list="fileList"
    :limit="limit"
  >
    <el-button type="primary">上传</el-button>
    <template v-if="tips" #tip>
      <div class="el-upload__tip">
        {{ tips }}
      </div>
    </template>

    <template #file="{ file }">
      <UploadPreview
        :url="file.url"
        :previewBoxStyle="previewBoxStyle"
      ></UploadPreview>
      <span class="el-upload-list__item-actions">
        <span class="el-upload-list__item-preview" @click="handlePreview(file)">
          <el-icon><zoom-in /></el-icon>
        </span>
        <span class="el-upload-list__item-delete" @click="handleRemove(file)">
          <el-icon><delete /></el-icon>
        </span>
      </span>
    </template>
  </el-upload>
</template>

<script setup>
import { ref, defineProps, defineEmits } from "vue";
import { ElUpload, ElButton } from "element-plus";
import UploadPreview from "./UploadPreview.vue";

const props = defineProps({
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
  tips: String,
  setup(props) {
    console.log(props);
  },
});

const fileList = ref([]);
if (typeof props.modelValue == "string") {
  fileList.value.push({
    name: props.modelValue.split("/").pop(),
    url:props.modelValue,
  })
}

if (Array.isArray(props.modelValue)) {
  props.modelValue.map(function(url){
    fileList.value.push({
      name: url.split("/").pop(),
      url:url,
    })
  })
}

const emit = defineEmits(["update:modelValue"]);
const handleSuccess = (response, uploadFile, uploadFiles) => {
  const value = props.uploadSuccess(response, uploadFile, uploadFiles);
  if (value !== false) {
    updateModel(value);
  }

  console.log(props.modelValue);
};

function updateModel(value) {
  emit("update:modelValue", value);
}
</script>
