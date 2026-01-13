<script setup>
import { ElMessage } from 'element-plus'
import { ref } from 'vue'

// 上传文件的名称
const fileName = ref('')

// 文件选择/拖拽改变事件
const handleFileChange = (file) => {
  fileName.value = file.name
}

//步骤条状态
const active = ref(2)

// 最后一步按钮事件
const handleLastStep = () => {
  active.value = 3
  ElMessage.success('success !')
}

// 完成按钮事件
const handleFinish = () => {
  console.log('点击了完成，文件名：', fileName.value)
  if (fileName.value == '')
    ElMessage.warning('please upload a file !')
  // 可添加上传逻辑
  else {
    active.value = 3
    ElMessage.success('success !')
  }

}
</script>
<template>
  <main class="resume-upload-page">
    <!-- 页面容器 -->
    <div class="container">
      <!-- 左侧插画区域 -->
      <section class="illustration-section">
        <div class="illustration-content">
          <h1>Finish!</h1>
          <h2>Upload Your Resume</h2>
          <p class="desc">Upload your resume, the platform will help you parse and optimize, you can also skip this step
          </p>
          <div class="illustration-img">
            <img src="./assets/logo.png" style="width: 400px;">
          </div>
        </div>
      </section>

      <!-- 右侧上传区域 -->
      <section class="upload-section">
        <div class="upload-content" v-if="active != 3">
          <h3>Upload file</h3>

          <div>
            <!-- 上传组件 -->
            <div class="upload-box">
              <el-upload ref="uploadRef" class="resume-uploader" drag action="#" :auto-upload="false"
                :on-change="handleFileChange" :show-file-list="false">
                <el-icon class="upload-icon"><upload-filled /></el-icon>
                <p class="upload-tip">Drag your resume file to this area, or click on the area to select the appropriate
                  file to upload</p>
              </el-upload>

            </div>
            <!-- 显示已上传文件名 -->
            <div v-if="fileName" class="file-name">{{ fileName }}</div>
            <!-- 按钮区域 -->
            <div class="btn-group">
              <el-button type="primary" @click="handleLastStep">Last step</el-button>
              <el-button type="primary" @click="handleFinish">Finish</el-button>
            </div>
          </div>



        </div>
        <div class="progress-success" v-else>
          <h1>success !</h1>
        </div>
        <!-- 步骤条 -->
        <el-steps :active="active" finish-status="success" align-center>
          <el-step />
          <el-step />
          <el-step />
        </el-steps>
      </section>
    </div>
  </main>
</template>

<style scoped>
/* 页面基础样式 */
.resume-upload-page {
  min-height: 100vh;
  background-color: #f9f9f9;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

/* 容器布局 */
.container {
  width: 100%;
  max-width: 1200px;
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-wrap: wrap;
}

/* 左侧插画区域 */
.illustration-section {
  flex: 1;
  min-width: 300px;
  padding: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
  border-right: 1px solid #f0f0f0;
}

.illustration-content h1 {
  font-size: 28px;
  font-weight: 500;
  color: #333;
  margin: 0 0 8px 0;
}

.illustration-content h2 {
  font-size: 22px;
  font-weight: 500;
  color: #333;
  margin: 0 0 16px 0;
}

.illustration-content .desc {
  font-size: 14px;
  color: #999;
  line-height: 1.5;
  margin-bottom: 32px;
}

.illustration-img {
  margin-top: 20px;
  text-align: center;
}

/* 右侧上传区域 */
.upload-section {
  flex: 1;
  min-width: 300px;
  padding: 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.upload-content h3 {
  font-size: 20px;
  font-weight: 500;
  color: #333;
  margin-bottom: 24px;
}

.progress-success {
  height: 318px;
  line-height: 318px;
  text-align: center;
}

.progress-success h1 {
  font-size: 22px;
  font-weight: 500;
  color: #333;
  margin: 0 0 16px 0;
}

/* 上传框样式 */
.upload-box {
  margin-bottom: 16px;
}

.upload-box:hover {
  border-color: #409eff;
  background-color: #f0f7ff;
}

.resume-uploader {
  width: 100%;
}

.upload-icon {
  font-size: 48px;
  color: #409eff;
  margin-bottom: 16px;
}

.upload-tip {
  font-size: 14px;
  color: #999;
  text-align: center;
  line-height: 1.5;
  padding: 0 20px;
}

/* 已上传文件名 */
.file-name {
  margin-top: 12px;
  margin-bottom: 16px;
  font-size: 12px;
  color: #409eff;
  padding: 8px 12px;
  background-color: #f0f7ff;
  border-radius: 4px;
}

/* 按钮组 */
.btn-group {
  min-width: 300px;
  text-align: center;
  margin-bottom: 32px;
}

.btn-group .el-button {
  width: 150px;
}


/* 响应式适配（小屏上下布局） */
@media (max-width: 887px) {
  .container {
    flex-direction: column;
  }

  .illustration-section {
    border-right: none;
    border-bottom: 1px solid #f0f0f0;
    padding-bottom: 20px;
  }

  .upload-section {
    padding-top: 20px;
  }

  .progress-success {
    height: 297.5px;
    line-height: 297.5px;
  }
}
</style>