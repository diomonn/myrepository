<template>
<div>
  <canvas  width="120" height="45"  class="border  " id="canvas"></canvas>
</div>
</template>
<script setup lang="ts">
import {onMounted} from 'vue'
import CaptchaMini from 'captcha-mini';
import {useCaptchapStore} from '@/stores/Captchap';
const R=useCaptchapStore()
let captcha2 = new CaptchaMini({
        lineWidth: 1,   //线条宽度
        lineNum: 6,       //线条数量
        dotR: 2,          //点的半径
        dotNum: 25,       //点的数量
        preGroundColor: [10, 80],    //前景色区间
        backGroundColor: [150, 250], //背景色区间
        fontSize: 30,           //字体大小
        fontFamily: ['Georgia', '微软雅黑', 'Helvetica', 'Arial'],  //字体类型
        fontStyle: 'stroke',      //字体绘制方法，有fill和stroke
        content: '一个验证码abcdefghijklmnopqrstuvw生成的插件使用的是canvas显示',  //验证码内容
        length: 6    //验证码长度
 }); 
onMounted(()=>{
   captcha2.draw(document.querySelector('#canvas'), (r:any) => {
        R.captchap=''
       r.split('').filter((e:any)=>e<='Z'&&e>='A'||e<='z'&&e>='a').map((e:any)=>{
        R.captchap+=e
        })
});
})
</script>
