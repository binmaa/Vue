<template>
  <!-- 主体区域 -->
  <section id="player">
    <!-- 输入框 -->
    <header class="header">
      <h1>
        <a href="https://blog.csdn.net/weixin_40845192?spm=1000.2115.3001.5113">
          <img src="./assets/img/player.png" alt="" />
        </a>
        音乐播放器
      </h1>
      <input
        autofocus="autofocus"
        autocomplete="off"
        placeholder="请输入歌名"
        class="new-todo"
        v-model="query"
        @keyup="search"
      />
    </header>
    <!-- 列表区域 -->
    <section class="main">
      <ul class="music-list">
        <li class="music" v-for="(item,index) in result" :key="index">
          <div class="view">
            <span class="index">{{index+1}}.</span>
            <label>{{item.name}}</label>
            <button class="play" @click="play(item.id)"></button>
          </div>
        </li>
      </ul>
    </section>
    <!-- 统计和清空 -->
    <footer class="footer">
      <audio :src="musicUrl" controls autoplay></audio>
    </footer>
  </section>
</template>

<script>
  /*
    接口1:歌曲搜索
      地址:https://autumnfish.cn/search
      方法:get
      参数:keywords  搜索关键字

    接口2:获取歌曲播放地址
      地址:https://autumnfish.cn/song/url
      方法:get
      参数:id  歌曲id
  */
  import './assets/css/player.css'
  //创建一个变量把下载的axios设置给他
  import axios from 'axios'
  export default {
    data(){
      return {
        query:'',
        result:[],
        musicUrl:''
      }
    },
    methods:{
      search(){
        axios({
          url:"https://autumnfish.cn/search",
          method:"GET",
          params:{keywords:this.query}
        }).then(res =>{
          this.result = res.data.result.songs;
        })
      },
      play(musicId){
        axios({
          url:"https://autumnfish.cn/song/url",
          method:"GET",
          params:{id:musicId}
        }).then(res => {
            console.log(res)
            this.musicUrl = res.data.data[0].url;
        })

      }

    }

  }
</script>

<style></style>
