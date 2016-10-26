<template>
    <div id="app">
      <h1>todos</h1>
      <ul class="list">
          <listcard class = "listcard"
                  :index = "index"
                  :item = "item"
                  :lists = lists
                  v-for= "(item, index) in lists"
                  @del= "update">
                  </listcrd>
      </ul>
      <div class="add-box">
          <button class="add-btn" @click= "add">＋</button>
          <button class="cancel-btn">-</button>
      </div>
    </div>
</template>
<script>
import Listcard from './components/Listcard'
export default {
    data() {
        let lists = JSON.parse(localStorage.getItem('todos-vue') || '[]');
        if (lists) {
            for (let i = lists.length - 1;i >= 0;i--) {
                if (lists[i] === null ) {
                    lists.splice(i, 1);
                }
            }
            localStorage.setItem('todos-vue', JSON.stringify(lists));
        }
        return {
            lists: lists
        }
    },
    components: {
        Listcard
    },
    methods: {
        add: function() {
            let id = this.lists.length;
            this.lists.push({id});
        },
        update: function(todos){
            this.lists = todos;
        }
    }
}

</script>
<style>
html {
    height: 100%;
    width: 100%;
}
h1 {
    text-align: center;
    width: 100%;
    font: 70px 'Helvetica Neue';
    font-weight: 100;
  }
body {
    font: 14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
    line-height: 1.4em;
    color: #4d4d4d;
    height: 100%;
    width: 100%;
    margin: 0 auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-weight: 300;
}
ul {
    list-style: none;
    padding: 0px;
    margin-left: 22px;
}
.listcard {
    float: left;
}
#app {
  height: 100%;
  display: block;
  font-size: 14px;
  margin: 20px;
}
.add-box .add-btn {
    background-color: #e91e63;
    position: fixed;
    bottom: 10px;
    right: 10px;
    height: 4rem;
    width: 4rem;
    border-radius: 100%;
    border-color: #e91e63;
    text-align: center;
    font-size: 2.2rem;
    color: #fff;
    line-height: 1rem;
    outline:none;
}
.add-box .cancel-btn {
    background-color: #e91e63;
    position: fixed;
    bottom: 100px;
    right: 10px;
    height: 4rem;
    width: 4rem;
    border-radius: 100%;
    border-color: #e91e63;
    text-align: center;
    font-size: 2.2rem;
    color: #fff;
    line-height: 1rem;
    outline:none;
}
</style>


