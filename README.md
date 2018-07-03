# about my repository

## 基于vue、element-ui的项目

##### 商品参数编辑[vue-good-param](https://github.com/Trubasa/vue-good-param)
##### 图片管理器[vue-picture-manager](https://github.com/Trubasa/vuePictureManager)
##### 图片拖拽排序[vue-img-sort](https://github.com/Trubasa/vue-img-sort)

- ### 项目描述

![项目描述](https://trubasa.github.io/doc/image/explain.png)

- ### 如何使用

查看example里的demo可快速掌握如何使用组件,这里以vue-picture-manager为例

> 引入依赖文件
```html
  <!--该项目依赖于vue，element-ui，如果您的项目已经引用过，可以不必再次引入-->
  <!--vue-->
  <script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
  <!--element-ui-->
  <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
  <script src="https://unpkg.com/element-ui/lib/index.js"></script>

  <!--必须保证在vue和element-ui的引入之后-->
  <!--vue-picture-manager-->
  <script src="../dist/vue-picture-manager.js"></script>
```
> 使用组件标签

将组件标签写入页面， **ref** 为组件注册一个对象（可理解为id），**:** 为组件接受的参数， **@** 为组件的回调事件
```html
<div id="app">

  ...

  <vue-picture-manager
    ref="pictureManager"
    :upload-path="uploadPath"
    :img-list="imgList"
    @upload-response="uploadResponse"
    @delete="deleteHandler"
    @selected="selected">
  </vue-picture-manager>


</div>

```
> js初始化vue

初始化Vue， **el** 为初始化的标签对象， **data** 里为vue实例的数据， **method** 存放Vue实例的方法

以下面代码为例，可使用 **app.isShow=true** 直接修改Vue实例里的数据，也可 **app.showPicManager()** 调用app实例里的方法，
**app.$refs.pictureManager.show()** 可调用到组件实例里的方法
```javascript
var app=new Vue({
    el:"#app",
    data:function () {
      return {
        uploadPath:'http://localhost:8088/smallappM/vender/goodsInfo/uploadImg',
        selectedList: [],
        isShow: false,
        imgList: []
      }
    },
    methods: {
      deleteHandler(url){
        //删除图片的回调
      },
      uploadResponse(res){
        //上传图片的回调
      },
      selected(val) {
        //选择图片的回调
        
      },
      showPicManager() {
          var that = this;
          this.$refs.pictureManager.show({
            defaultUrlList: [],  //默认选中的图片的地址数组
            ensureFun: function (res) {  //选中图片后点击'确定'的回调，返回选中的图片数组
              that.selectedList = res
            }
          });
        },
    }
  })
```