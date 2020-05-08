<template>
  <div class="editor-div">
    <mavonEditor
      v-model="content"
      @change="change"
      @save="saveBlog"
      style="height: 100%"
    ></mavonEditor>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import { mavonEditor } from "mavon-editor";
import "mavon-editor/dist/css/index.css";

export default Vue.extend({
  name: "editor",
  mounted: function() {
    console.log("test");
    this.changeArticle()
  },
  data: function() {
    return {
      content: "# djxc",
      articleID: ""
    };
  },
  methods: {
    /**
     * **获取文章**
     * 1、获取文章数据，将文章内容直接赋值给`content`
     */
    changeArticle() {
      axios
        .get("http://localhost:3000/users/dj")
        .then(res => {
          if (res.status === 200) {
            console.log(res.data[0]);
            this.content = res.data[0].content;
            this.articleID = res.data[0]._id;
          }
        })
        .catch(error => {
          console.log(error);
        });
    },
    /**
     * name
     */
    change(value, render) {
      console.log(value, render);
    },
    saveBlog(value) {
      console.log(value);
      axios
        .post("http://localhost:3000/users/save_article", {
          content: value,
          id: this.articleID
        })
        .then(res => {
          console.log(res);
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  components: {
    mavonEditor
  }
});
</script>

<style>
.editor-div {
  height: 90vh;
  width: 100vw;
}
</style>
