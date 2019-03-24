<template>
  <div>
    <div v-if="!repoUrl">loading</div>
    <div v-else>
      most star repo is
      <a :href="repoUrl">{{repoName}}</a>
    </div>
  </div>
</template>

<script>
// axios在哪里用就在哪里引入
import axios from "axios";
export default {
  data() {
    return {
      repoUrl: "",
      repoName: ""
    };
  },

  //初始化的时候显示
  mounted() {
    //发ajax请求获取数据
    const url = `https://api.github.com/search/repositories?q=v&sort=stars`;
    //this.$http.get(url)得到的是promise
    // this.$http.get(url).then(
    //   response => {
    //     //success callback
    //     //console.log(response.data)  //返回结果数据
    //     const result = response.data;
    //     //得到最受欢迎的repo
    //     const mostRepo = result.items[0];
    //     this.repoUrl = mostRepo.html_url;
    //     this.repoName = mostRepo.full_name;
    //   },
    //   response => {
    //     //erroe callback
    //     //console.log(response.statusText)   //错误信息
    //     alert("请求失败");
    //   }
    // );

    //使用axios发送ajax请求
    axios
      .get(url)
      .then(response => {
        const result = response.data;
        //得到最受欢迎的repo
        const mostRepo = result.items[0];
        this.repoUrl = mostRepo.html_url;
        this.repoName = mostRepo.full_name;
      })
      .catch(error => {
        alert("请求失败");
      });
  }
};
</script>

<style>
</style>
