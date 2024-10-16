<!-- UploadPreview.vue -->
<template>
    <el-image v-if="isImg(url)" class="upload-preivew-img" :src="url" :style="previewBoxStyle" fit="contain"></el-image>
    <div v-if="isVideo(url)" :style="previewBoxStyle">
        <video :src="url" controls style="width:100%; height:100%;"></video>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
import { String } from 'core-js';
import { ElImage } from 'element-plus';

defineProps({
    url: String,
    previewBoxStyle: Object,
})

const
    isImg = (url) => {
        if (!isURL(url)) {
            return false;
        }

        return isExtension(url, ['jpg', 'jpeg', 'png', 'gif', 'bmp', 'webp', 'svg']);
    },

    isVideo = (url) => {
        console.log(url);
        if (!isURL(url)) {
            return false;
        }
        
        return isExtension(url, ['mp4']);
    },

    isExtension = (url, extensions) => {
        const ext = url.split('.').pop().toLowerCase();
        return extensions.includes(ext);
    },

    isURL = (str) => {
        try {
            new URL(str);
            return true;
        } catch (e) {
            console.log("preview url is not a url, ", str, e);
            return false;
        }
    };
</script>

<style>
.upload-preivew-img.el-image .el-image__inner {
    width:100%;
    height:100%;
}
</style>