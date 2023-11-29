<template>
  <el-form 
      :model="controls" 
      :rules="rules" 
      ref="form"
      @submit.native.prevent="onSubmit"
    >

      <h2>Создать новый пост</h2>

      <el-form-item label="Введите название поста" prop="title">
        <el-input 
          v-model.trim="controls.title"
        />
      </el-form-item>
      
      <el-form-item label="Текст в формате .md или .html" prop="text">
        <el-input 
          type="textarea"
          v-model="controls.text" 
          resize="none"
          :rows="10"
        />
      </el-form-item>

      <el-button class="mb" type="success" plain @click="previewDialog = true">
        Предпросмотр
      </el-button>

      <el-dialog title="Предпросмотр" :visible.sync="previewDialog">
        <div :key="controls.text">
          <vue-markdown>{{ controls.text }}</vue-markdown>
        </div>
      </el-dialog>

      <el-upload
        class="mb"
        drag
        ref="upload"
        action="https://jsonplaceholder.typicode.com/posts/"
        :on-change="handleImageChange"
        :auto-upload="false"
      >
        <i class="el-icon-upload2 icon-upload"></i>
        <div class="el-upload__text">Перетащите картинку <em>или нажмите</em></div>
        <div slot="tip" class="el-upload__tip">Файлы с расширением jpg/png</div>
      </el-upload>

      <el-form-item>
        <el-button 
          type="primary" 
          native-type="submit"
          round
          :loading="loading"
        >Создать пост</el-button>
      </el-form-item>
    </el-form>
</template>

<script>
export default {
  layout: 'admin',
  middleware: ['admin-auth'],
  data() {
    return {
      image: null,
      previewDialog: false,
      loading: false,
      controls: {
        title: '',
        text: ''
      },
      rules: {
        text: [
          { required: true, message: 'Поле текста не должно быть пустым', trigger: 'blur' }
        ],
        title: [
          { required: true, message: 'Введите название поста', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      this.$refs.form.validate(async valid => {
        if (valid && this.image) {
          this.loading = true;

          const FormData = {
            title: this.controls.title,
            text: this.controls.text,
            image: this.image
          };

          try {
            await this.$store.dispatch('post/create', FormData);
            
            this.controls.title = '';
            this.controls.text = '';
            this.image = null;
            this.$refs.upload.clearFiles();
            
            this.$message.success('Пост успешно создан');
          } catch (e) {} finally {
            this.loading = false;
          }
        } else {
          this.$message.warning('Форма не заполнена');
        }
      })
    },
    handleImageChange(file, fileList) {
      this.image = file.raw;
    }
  }
}
</script>

<style lang="scss" scoped>
  form {
    width: 600px;
  }

  .icon-upload {
    margin-top: 50px;
  }
</style>