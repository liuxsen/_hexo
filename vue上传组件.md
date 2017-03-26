---
title: vue上传组件
date: 2017-03-02 10:47:36
tags: vue
---

{% asset_img 上传.gif %}

### 使用方式

```html
<input-img :onChange="change" v-model="target"></input-img>
```

+ onChange 当选中了文件之后，回调会被调用
+ target 会同步选择的文件；

#### 源码展示
```html
<template> 
    <div>
        <div ref="box" class="updata" :class="{dropenter: dropenter}">
            <input type="file" :id="inputId" ref="inputer" @change="handleFIlechange">
            <label v-if="!dropenter" :for="inputId">点击上传/拖拽上传</label>
            <label v-if="dropenter">拖放上传</label>
            <div class="err-text" v-show="errText">{{errText}}</div>
        </div>
        <span v-if="fileName">{{fileName}}</span>
        <span v-if="fileSize">{{fileSize}} KB</span>
    </div>
    
</template>
<script>
    export default {
        props:{
            onChange:{
                type: Function,
                defulat: null,
            },
            id:{
                type:String,
                default: ""
            }
        },
        data(){
            return {
                dataUrl:"",
                dropenter: false,
                errText: "",
                dorpEnter: "",
                fileName: "",
                fileSize: "",
                inputId:""
            }
        },
        methods:{
            handleFIlechange(){
                let inputDom = this.$refs.inputer;
                this.file = inputDom.files[0];
                this.errText = "";
                let size = Math.floor(this.file.size/1024);
                // 大小控制
                // if(size>10){
                //     return false;
                // }
                // 触发组件对象的input事件
                this.$emit('input',this.file);
                this.fileName = this.file.name;
                 this.fileSize = Math.round(this.file.size/1024);
                this.onChange && this.onChange(this.file,inputDom.value);
                this.imgPreview(this.file);
            },
            imgPreview (file) {
                let self = this;
                // 看支持不支持FileReader
                if (!file || !window.FileReader) return;
        
                if (/^image/.test(file.type)) {
                    // 创建一个reader
                    var reader = new FileReader();
                    // 将图片将转成 base64 格式
                    reader.readAsDataURL(file);
                    // 读取成功后的回调
                    reader.onloadend = function () {
                        self.dataUrl = this.result;
                        // console.log(self.dataUrl)
                    }
                }
            },
            preventDefaultEvent(eventName){
                document.addEventListener(eventName,function(e){
                    e.preventDefault();
                    // console.log(e)
                },false);
            },
            addDropSupport(){
                let box = this.$refs.box;
                box.addEventListener('dragenter',(e)=>{
                    e.preventDefault();
                    this.dropenter = true;
                });
                box.addEventListener('dragleave',(e)=>{
                    e.preventDefault();
                    this.dropenter = false;
                });
                box.addEventListener('drop',(e)=>{
                    e.preventDefault();
                    // 获得文件对象列表
                    let fileList = e.dataTransfer.files;
                    if(fileList.length === 0){
                        return false;
                    }
                    //           拖拽文件列表 image/jpeg
                    console.log("拖拽文件列表",fileList[0].type);
                    if(fileList[0].type.indexOf('image') === -1){
                        this.errText = '请选择图片'
                    }else{
                        this.errText = ''
                    }
                    if(fileList.length>1){
                        this.errText = "暂时不支持多文件";
                        return false;
                    }
                    this.file = fileList[0];
                    this.$emit('input',this.file);
                    this.fileName = this.file.name;
                    this.fileSize = Math.round(this.file.size/1024);
                    this.onChange && this.onChange(this.file,this.fileName);
                    this.imgPreview(this.file);
                    this.dropenter = false;
                })
            },
            generateId(){
                var nonstr = Math.random().toString(36).substring(3,8);
                if(!document.getElementById(nonstr)){
                    return nonstr;
                }else{
                   return this.generateId();
                }
            }
        },
        mounted(){
            this.inputId = this.id || this.generateId();
            ['dragleave','drog','dragenter','dragover'].forEach(eventName=>{
                //console.log(eventName)
                this.preventDefaultEvent(eventName);
            });
            this.addDropSupport();
        }
    }
</script>
<style scoped>
    .updata{
        display:inline-block;
        position: relative;
        width: 100%;
        height: 100px;
        border: 1px dashed #aaaaaa;
        text-align: center;
        line-height: 100px;
    }
    .updata.dropenter{
        box-shadow: 0 0 3px #aaaaaa;
    }
    input{
        position: absolute;
        left: -9999px;
    }
    label{
        position: absolute;
        left: 0;
        top: 0;
        right: 0;
        bottom: 0;
        z-index: 10;
    }
    .err-text{
        position: absolute;
        bottom: 0;
        left: 0;
        line-height: 22px;
        color: red;
    }
</style>
``` 