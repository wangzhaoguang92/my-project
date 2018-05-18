<template>
  <div id="wrapper">
    <el-row>
      <el-button type="primary" @click="add()">主要按钮</el-button>

    </el-row>
  </div>
</template>

<script>
  import SystemInformation from './LandingPage/SystemInformation'
  import {ipcRenderer } from 'electron'

  export default {
    name: 'landing-page',
    components: { SystemInformation },
      data() {
          return {
              activeIndex: '1',
              activeIndex2: '1'
          };
      },
    methods: {
        handleSelect(key, keyPath) {
            console.log(key, keyPath);
        },

      add(){
            //异步方法
//          ipcRenderer.send('asynchronous-message', '我接到了');
//          ipcRenderer.on('asynchronous-reply', function (event, arg) {
//              console.log( `我获取到的mac地址: ${arg}`)
//          })
          const reply = ipcRenderer.sendSync('synchronous-message', '我接到了')
          this.$message({
              showClose: true,
              message: `我获取到你的mac地址: ${reply}`,
              type: 'success'
          });

      }
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro');

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body { font-family: 'Source Sans Pro', sans-serif; }

  #wrapper {
    background:
      radial-gradient(
        ellipse at top left,
        rgba(255, 255, 255, 1) 40%,
        rgba(229, 229, 229, .9) 100%
      );
  }

  #logo {
    height: auto;
    margin-bottom: 20px;
    width: 420px;
  }

  main {
    display: flex;
    justify-content: space-between;
  }

  main > div { flex-basis: 50%; }

  .left-side {
    display: flex;
    flex-direction: column;
  }

  .welcome {
    color: #555;
    font-size: 23px;
    margin-bottom: 10px;
  }

  .title {
    color: #2c3e50;
    font-size: 20px;
    font-weight: bold;
    margin-bottom: 6px;
  }

  .title.alt {
    font-size: 18px;
    margin-bottom: 10px;
  }

  .doc p {
    color: black;
    margin-bottom: 10px;
  }

  .doc button {
    font-size: .8em;
    cursor: pointer;
    outline: none;
    padding: 0.75em 2em;
    border-radius: 2em;
    display: inline-block;
    color: #fff;
    background-color: #4fc08d;
    transition: all 0.15s ease;
    box-sizing: border-box;
    border: 1px solid #4fc08d;
  }

  .doc button.alt {
    color: #42b983;
    background-color: transparent;
  }
</style>
