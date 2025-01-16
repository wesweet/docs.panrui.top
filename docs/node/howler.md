## 文档

- [官方仓库](https://github.com/goldfire/howler.js)

## 基础使用

```js
import { Howl, Howler } from "howler";
// 配置选项
const options = {
  src: ["sound.mp3"], //音频地址 Array/String 必填
  volume: 1, //音量 Number 0-1
  html5: false, //是否使用 HTML5 播放 Boolean
  loop: false, //是否循环 Boolean
  preload: true, //是否在页面加载后自动播放 Boolean
  autoplay: false, //是否自动播放 Boolean
  mute: false, //是否静音 Boolean
  sprite: {}, //音频分组 Object
  rate: 1, //播放速率 Number
  pool: 5, //音频池大小 Number
  format: null, //音频格式 Array
  xhrWithCredentials: false, //是否使用凭证 Boolean
  onload: () => {}, //加载完成回调 Function
  onloaderror: () => {}, //加载错误回调 Function
  onplayerror: () => {}, //播放错误回调 Function
  onplay: () => {}, //播放回调 Function
  onend: () => {}, //播放结束回调 Function
  onpause: () => {}, //暂停回调 Function
  onstop: () => {}, //停止回调 Function
  onmuted: () => {}, //静音回调 Function
  onvolume: () => {}, //音量回调 Function
  onrate: () => {}, //播放速率回调 Function
  onseek: () => {}, //跳转回调 Function
  onfade: () => {}, //淡入淡出回调 Function
  onunlock: () => {}, //解除锁定回调 Function
};
const sound = new Howl(options);

// sound 事件 TODO
sound.play(); //播放
sound.pause(); //暂停
sound.stop(); //停止
sound.mute(); //静音
sound.volume(0.5); //设置音量
sound.fade(0, 1, 1000); 
```

最后更新时间：2025-01-16 22:43:12
