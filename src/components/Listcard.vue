<template>
  <div class="listcard">
      <div class="card">
          <div class="header">
              <p class="filter"></p>
          </div>
          <div class="text-input">
              <textarea v-model="title" v-show="textModel"></textarea>
              <label v-show= "!textModel">{{ title }}</label>
          </div>
          <div class="footer">
              <button class="del-btn" @click="del">删除</button>
              <button class="save-btn" v-show="textModel" @click="save">保存</button>
              <button class="edit-btn" v-show="!textModel" @click="edit">修改</button>
          </div>
      </div>
  </div>
</template>
<script>
export default {
  props: [
      'index',
      'lists'
  ],
  data() {
      let todos = JSON.parse(localStorage.getItem('todos-vue') || '[]');
      let textModel = true;
      let title = '';
      if (todos[this.index]) {
        title = todos[this.index].text;
        textModel = false;
      }
      return {
        name: 'listcard',
        textModel: textModel,
        title: title,
        todos: todos
      }
  },
  methods: {
      save: function() {
          this.textModel = false;
          let todo = {
            text: this.title
          };
          this.todos[this.index] = todo;
          localStorage.setItem('todos-vue', JSON.stringify(this.todos));
      },
      edit: function() {
          this.textModel = true;
          console.log(this.lists);
      },
      del: function() {
       this.lists.splice(this.index,1);
        console.log(this.lists);
      }
  }
}
</script>
<style>
.listcard{
    display: block;
    width: 370px;
    box-shadow: 0 2px 5px 0 rgba(0, 0, 0, 0.12);
    margin-bottom: 20px;
    margin-left: 20px;
}
.header {
    background-color: #434db0;
    padding: 1.2em;
    height: 70px;
    box-sizing: border-box;
}
.footer {
    border-top: 1px solid #e5e5e5;
    text-align: right;
    padding: 20px 0;
}
.text-input {
    border: none;

    height: 120px;
}
textarea {
    padding: 2px 5px;
    width: 360px;
    border:none;
    outline:none;
    font-size: 18px;
    resize: none;
    line-height: 1.5;
    font-family: 'Helvetica Neue';
    font-weight: 300;
}
label {
    padding: 2px 5px;
    display: block;
    font-size: 18px;
    line-height: 1.5;
    word-wrap:break-word;
    word-break:keep-all;
    overflow:hidden;
    font-weight: 300;
}
button {
    background-color: #de236c;
    cursor: pointer;
    color: #fff;
    min-height: auto;
    height: auto;
    padding: 8px 14px;
    display: inline-block;
    margin-right: 1em;
    font-size: 16px;
    line-height: 16px;
    text-align: center;
    border:none;
    outline:none;
}
</style>

