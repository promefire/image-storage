<!-- <template>
    <div>

        <p>upload image </p>
        <input type="file" @change="handleFileSelect">

    </div>
</template>

<script> 

export default{
    methods:{
        handleFileSelect(event) {
      const fileList = event.target.files;
      // 处理选中的文件
      console.log(fileList);
    }
}
}

</script> -->
<template>
    <div class="max-w-screen-md mx-auto p-4">
      <h1 class="text-2xl font-bold mb-4">Image Upload</h1>
      <input
        type="file"
        accept="image/*"
        @change="handleFileChange"
        class="mb-4"
      />
  
      <button @click="handleUpload" class="bg-blue-500 text-white py-2 px-4 rounded">
        Upload Image
      </button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        selectedFile: null,
      };
    },
    methods: {
      handleFileChange(event) {
        const file = event.target.files[0];
        this.selectedFile = file;
      },
      async handleUpload() {
        if (!this.selectedFile) {
          alert('Please select a file first');
          return;
        }
  
        const formData = new FormData();
        formData.append('file', this.selectedFile);
  
        try {
          const response = await fetch('https://backup.promefire.top/', {
            method: 'POST',
            body: formData,
          });
  
          if (response.ok) {
            const result = await response.json();
            console.log('result', result);
            window.alert('上传成功');
          } else {
            console.error('Upload failed. HTTP status:', response.status);
          }
        } catch (error) {
          console.error('Error during upload:', error);
        }
      },
    },
  };
  </script>
  
  <style>
  /* 添加样式，根据需要自定义样式 */
  </style>
  