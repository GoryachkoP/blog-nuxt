<template>
  <div class='post-create'>
    <el-form
      :model="controls"
      :rules="rules"
      ref="form"
      @submit.native.prevent="onSubmit"
    >
      <h2 class="mb">Создать новый пост</h2>
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

      <el-dialog title="Предпросмотр" :visible.sync="previewDialog">
        <div :key="controls.text">
          <vue-markdown>{{ controls.text }}</vue-markdown>
        </div>
      </el-dialog>

      <el-upload
        class="mb"
        ref="upload"
        drag
        action="https://jsonplaceholder.typicode.com/posts/"
        :on-change="handleImage"
        :auto-upload="false"
      >
        <i class="el-icon-upload"></i>
        <div class="el-upload__text">Перетащите картинку <em>или нажмите</em></div>
        <div class="el-upload__tip" slot="tip">файлы с расширением jpg/png</div>
      </el-upload>

      <el-form-item class="login-card__button">
        <el-button class="mb" type="success" round @click="previewDialog = true">
          Предпросмотр
        </el-button>

        <el-button 
          type="primary" 
          round
          native-type="submit"
          :loading="loading"
        >
          Создать пост
        </el-button>
      </el-form-item>
    </el-form>
  </div>
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
          { required: true, message: 'Текст не должен быть пустым', trigger: 'blur' }
        ],
        title: [
          { required: true, message: 'Название поста не может быть пустым', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    handleImage(file, filelist) {
      this.image = file.raw
      // console.log(this.image)
    },
    onSubmit () {
      this.$refs.form.validate(async valid => {
        if (valid && this.image) {
          this.loading = true

          const formData = {
            title: this.controls.title,
            text: this.controls.text,
            image: this.image
          }
          try {
            await this.$store.dispatch('post/create', formData)
            this.controls.title = ''
            this.controls.text = ''
            this.$refs.upload.clearFiles()
            this.$message.success('Пост создан')
          } catch (e) {} finally {
            this.loading = false
          }

        } else {
          this.$message.warning('Форма не валидна')
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
  .post-create {
    width: 600px;
  }
</style>

