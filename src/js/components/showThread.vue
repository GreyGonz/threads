<template>
  <div>
    <div class="box box-warning">
      <div class="box-header with-border">
        <h2 class="box-title">{{ thread.title }}</h2>
        <p>Created at {{ thread.created_at }} by {{ user.name }}</p>
        <div class="box-tools pull-right">
          <button type="button" class="btn btn-box-tool" data-widget="collapse"><i class="fa fa-minus"></i></button>
        </div>
        <!-- /.box-tools -->
      </div>
      <!-- /.box-header -->
      <div class="box-body">
        <medium-editor
          :text="thread.body"
          :options='options'
          custom-tag='p'>
          <!--v-on:edit="applyText">-->
        </medium-editor>
      </div>
      <div class="box-footer">
        <button type="button" class="btn btn-primary" @click="updateThread">Save</button>
      </div>
      <!-- /.box-body -->
    </div>
  </div>
</template>

<script>
  import editor from 'vue2-medium-editor'

  export default {
    name: 'showThread',
    data () {
      return {
        options: {
          toolbar: {buttons: ['bold', 'strikethrough', 'h1']}
        }
      }
    },
    props: ['thread', 'user'],
    components: {
      'medium-editor': editor
    },
    methods: {
      updateThread () {
        this.thread.body = document.getElementsByClassName('medium-editor-element')[0].innerText
        this.sendEmit('updateThread', this.thread)
      },
      sendEmit: function (option, message) {
        this.$emit(option, message)
      },
      // applyText: function () {
      //   // console.log(document.getElementsByClassName('medium-editor-element')[0].innerText)
      //   this.sendEmit('edited', document.getElementsByClassName('medium-editor-element')[0].innerText)
      // }
    }
  }
</script>