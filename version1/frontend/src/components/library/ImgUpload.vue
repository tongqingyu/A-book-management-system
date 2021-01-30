<template>
  <el-upload
    class="img-upload"
    ref="upload"
    action="http://localhost:8443/api/covers"
    :on-preview="handlePreview"
    :on-remove="handleRemove"
    :before-remove="beforeRemove"
    :on-success="handleSuccess"
    multiple
    :limit="1"
    :on-exceed="handleExceed"
    :file-list="fileList">
    <el-button size="small" type="primary">Upload</el-button>
    <div slot="tip" class="el-upload__tip">jpg/png only，file size under 500kb</div>
  </el-upload>
</template>

<script>
  export default {
    name: 'ImgUpload',
    data () {
      return {
        fileList: [],
        url: ''
      }
    },
    methods: {
      handleRemove (file, fileList) {
      },
      handlePreview (file) {
      },
      handleExceed (files, fileList) {
        this.$message.warning(`Only on file allowed，you select ${files.length} file(s) this time，${files.length + fileList.length} files selected total`)
      },
      beforeRemove (file, fileList) {
        return this.$confirm(`Remove ${file.name}？`)
      },
      handleSuccess (response) {
        this.url = response
        this.$emit('onUpload')
        this.$message.warning('Successful')
      },
      clear () {
        this.$refs.upload.clearFiles()
      }
    }
  }
</script>
