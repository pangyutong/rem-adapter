# less-adapter
  rem屏幕适配方案
    主要思路：
      通过rem的形式结合媒体查询  控制页面的缩放比例唯一  适配流行终端等比缩放
      （现适配320px,360px,375px,384px,400px,411px,414px,468px,480px,540px,600px,640px屏幕 可变）
      结合less 通过他拓展的变量和函数特性 统一控制缩放比例 在页面中使用px变量/@baseFontSize变量
      eg：padding: 0 90rem/@baseFontSize;
     公共参数：
        //设计稿宽度
        @psdWidth:750px;
        //默认基准值
        @baseFontSize:100px;
        //主流设备尺寸
        @deviceList:320px,360px,375px,384px,400px,411px,414px,468px,480px,540px,600px,640px,720px,750px;
        @len:length(@deviceList);
      函数设计：
           // 自调用 直到遍历到 数组最后一个  停止
          .adapterFuc(@index) when (@index <= @len){
            @media (min-width: extract(@deviceList,@index)) {
              html {
                font-size: extract(@deviceList,@index)/@psdWidth*@baseFontSize;
              }
            }
            .adapterFuc(@index + 1);
          }
        通过less的遍历 将所有适配的屏幕尺寸都媒体查询 生成npm编译成css代码
        
