---
title: TAA 相关结果展示
published:  2024-05-24T20:06:22.000Z
updated: 2024-05-24T20:06:22.000Z
description: 展示 TAA 中的结果及分析
image: "/images/cover1.jpeg"
tags:
  - TAA
  - Unity
  - motion vector
category: 工作记录
draft: false
---


# TAA相关总结

时域抗锯齿是目前主流抗锯齿方法之一，相对msaa来说可应对着色锯齿，减少着色计算。使图像边缘更加柔和，但可能会引入一定模糊，加入锐化可适当减轻

*   使用说明：
    
    *   开启TAA时，摄像机移动场景需要深度信息，故而需要去掉勾选FOVCameraObjects和FOVCameraForTransparentObjects Feature中的ClearDepth选项，一般而言，这个两个Feature需要起作用时，摄像机不移动。
        
    *   TAA目前没和MSAA兼容
        
    *   FovType 需要正确设置，因为有些FOV2层人物用到了fov调整效果，有些FOV2层人物没有用到。用到Fov效果的人物需要设置为FOV Camera Objects来设置（似乎只有主界面？？）——主界面需要设置FovType为FOV Camera Objects，其余界面设置为Not Fov
        

# 手机端画面对比（三星Note9）

TAA开启的选项是采样周围5像素颜色构建包围盒，采样周围5像素深度确定MotionVector，未开启锐化，当前帧占比为0.15，启用BicubicFilter采样历史帧，FOV选项为NotFOV。

1.  球员界面1
    
    1.  未开启AA  
        ![Screenshot_20240603-102651_NoAA531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/a05e402c-32c2-4fe8-821c-124d8ae81ff3.jpeg)
        
    2.  taa  
        ![Screenshot_20240603-112209_TAA5Dilation531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/c51b758d-bf16-4b95-8ef8-099cfee89562.jpeg)
        
    3.  msaa2x  
        ![Screenshot_20240603-102411_MSAA2x531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/9eae446d-5527-400a-8a39-841d1147f840.jpeg)
        
    4.  msaa4x  
        ![Screenshot_20240603-102949_MSAA4x531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/bc669280-73b4-463c-bbd6-a3988a9e0879.jpeg)
        
    5.  小结  
        球员界面TAA表现不错，可去除其他AA情况下，球员头部周围的一些着色锯齿高光闪烁的问题。
        
2.  球员界面2
    
    1.  未开启AA  
        ![Screenshot_20240603-102623_NoAA531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/c0d7bbd6-5a05-47c8-b385-be6d45945aab.jpeg)
        
    2.  taa  
        ![Screenshot_20240603-105956_TAA5Dilation531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/c84b7db5-086d-4c83-a642-b3a77ac7f4bd.jpeg)
        
    3.  msaa2x  
        ![Screenshot_20240603-102442_MSAA2x531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/35fe039f-ac47-4c20-a4ad-6723fa834a07.jpeg)
        
    4.  msaa4x  
        ![Screenshot_20240603-102917_MSAA4x531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/553ec7d1-3b65-46b6-9b91-28a7d2db0525.jpeg)
        
    5.  小结  
        球衣界面的字符锯齿问题在TAA的情况下可以得到有效解决。
        
3.  比赛内界面1
    
    1.  未开启AA  
        ![Screenshot_20240603-101745_NoAA531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/b336d6e5-7f1d-4990-b9c9-d90124d88571.jpeg)
        
    2.  taa  
        ![Screenshot_20240603-110037_TAA5Dilation531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/4143bc23-568b-491d-b753-3e10cccece31.jpeg)
        
    3.  msaa2x  
        ![Screenshot_20240603-102509_MSAA2x531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/a1be82d6-db1c-4177-8b4d-976f5e83abec.jpeg)
        
    4.  msaa4x  
        ![Screenshot_20240603-103012_MSAA4x531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/9aa74a11-440c-4576-90de-24c34b4b8807.jpeg)
        
    5.  小结  
        比赛内的情况，TAA使得图像变得柔和，且抗锯齿效果好于MSAA2x，与MSAA4x相当。TAA对球衣字符的着色锯齿也有一定缓解，但是会引入一定的模糊，而MSAA4x虽然不解决着色锯齿，但是不会引入模糊的效果。玩家可能更加偏好有锯齿但清晰的界面
        
4.  比赛界面2
    
    1.  未开启AA  
        ![Screenshot_20240603-101854_NoAA531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/a41a5c30-8411-4520-aa23-9fdd6a9e8940.jpeg)
        
    2.  taa  
        ![Screenshot_20240603-102015_TAA5Dilation531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/ccbda0d3-0429-43b6-acdd-29cf871d7109.jpeg)
        
    3.  msaa2x  
        ![Screenshot_20240603-101636_MSAA2x531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/5618e1a7-bf7e-4789-ba90-a1d1a811b477.jpeg)
        
    4.  msaa4x  
        ![Screenshot_20240603-103053_MSAA4x531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/348d21d5-5802-4abe-a89b-9b12f20bcd5c.jpeg)
        
5.  总结  
    对比了多场景下，未开启抗锯齿、TAA、MSAA2x和MSAA4x上的性能和效果。从性能上来看，TAA的性能与MSAA2x相近，比MSAA4x好。从效果上看TAA的效果与MSAA4x相似，都好于MSAA2x。但是在比赛内，TAA会引起一定的模糊情况，例如赛内球员球衣上的字符会变得更加柔和但是模糊。且由于TAA抖动镜头，远处的细节会不清晰或抖动，运动的场景无需调整，静态可能需要手动调整TAA参数。  
    ![Screenshot_20240603-102027_TAA5Dilation531.jpeg](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/000d9a67-bad2-4408-8fe9-d7962335c06a.jpeg)
    

# Unity内效果对比

1.  主界面
    
    1.  未开启AA  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/cd9c028f-e9b6-4230-88d0-b4c2126eb6ee.png)
        
    2.  taa  
        ![1TAA 2024-06-03 145723.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/9291322a-b83c-41f5-b43b-7b4c7d0faf31.png)
        
    3.  msaa2x  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/a06d2746-ce87-437d-a159-47f73ba7c0dd.png)
        
    4.  msaa4x  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/0d9beb3e-926d-4d21-b2b6-d3fbadcbab1c.png)
        
    5.  小结：taa整体图像会更加柔和，msaa看起来会更加锐利清晰
        
2.  主界面2x
    
    1.  未开启AA  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/af68eeea-ad4b-4a3c-9944-4826476abd4c.png)
        
    2.  taa  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/9734575d-44b9-40fc-9d1a-cabf7abdc385.png)
        
    3.  msaa2x  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/f108ba03-60c4-4717-81f0-385d0d81c51d.png)
        
    4.  msaa4x  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/785432d8-363c-4407-837f-8c0d5af7c4b1.png)
        
    5.  小结：taa抗锯齿效果与msaa4x相当，在着色锯齿方面更有优势（衣服中数字的显示）
        
3.  球员界面2x
    
    1.  未开启AA  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/470cc5e8-1fc0-4f72-906b-c8306f179008.png)
        
    2.  taa  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/4857414f-1467-4fcf-9d67-74eaac47c3de.png)
        
    3.  msaa2x  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/d943fffe-27bd-4020-ba73-7261eb26539a.png)
        
    4.  msaa4x  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/b1c24976-3bd7-4dc1-97c3-eebdd23a8e12.png)
        
4.  比赛内界面1x
    
    1.  未开启AA  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/e09fc029-72a0-4f09-9c31-4032557c602c.png)
        
    2.  taa  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/d02f9288-7912-4bc7-9c94-f0b10d0a1b5e.png)
        
    3.  msaa2x  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/6735d936-b09e-49b8-917f-6eeffcefbf83.png)
        
    4.  msaa4x  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/830ef4db-6b06-42b4-b824-de503fba0538.png)
        
    5.  taa提高当前帧占比加上锐化  
        ![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/a95e0192-5d0c-4ecd-b57f-b0ac5868fa2e.png)
        
    6.  小结  
        加入锐化和适当提高当前帧的情况下，模糊情况有所缓解，但是性能可能会下降。
        

# 具体选项说明

1.  BlendScale 
    
    *   当前帧所占比例：一般情况下无需修改，当画面抖动过大时可适当调小，常见值为0.05~0.25
        
    *   推荐值：    主界面及球员界面 0.1，比赛内0.2，或者全局0.15，画面抖动时可适当减少最低至0.04
        
2.  JitterScale 
    
    *   抖动尺度
        
3.  GammaBox 
    
    *   颜色盒尺寸：拒绝历史帧的颜色盒尺寸，
        
4.  UseSharp 
    
    *   使用锐化：因为TAA带来的模糊问题，使用锐化会有一定程度的缓解，但是性能消耗会增大，注意使用该选项需要启用“Use9Tap（采样周围9像素）”
        
5.  CurrentSharp 
    
    *   锐化程度
        
6.  UseBicubicFilter 
    
    *   双三次过滤（历史帧）：当镜头需要前后放大时，启用该选项可显著减少模糊
        
7.  Use9Tap 
    
    *   采样周围9像素：启用该选项可添加锐化，未启用则默认为采样周围5像素（用于颜色盒）
        
8.  UseClip 
    
    *   采用Clip方法或者Clamp方法
        
9.  LerpAtPerceptualSpace 
    
    *   在感知空间插值：若场景HDR效果导致微小闪光则启用该选项可减少闪光
        
10.  UseDilation 
    
    *   使用最近深度采样MotionVector
        
11.  FovType 
    
    *   Fov人物的类型：不同场景下，人物可能是FOV层级的，需要确认人物是由哪个RenderFeature画的，由此可对应相关的MotionVector。若不正确对应会导致残影。
        

# 推荐使用

目前经过测试，TAA可能适用于高端机型。渲染时间正常，可能传输数据稍大。在低端机型上会导致卡顿，高端机型上发热严重。建议在人物运动较少的场景开启TAA，比赛内因为模糊问题目前不建议开启。

# 性能探讨

TAA使用到了MotionVector，accumTex，DepthTexture，cameracolorAttachmentA和B5张rt，1920x1080情况下共占用63.2MB（其中深度图得拷出来占了15.8）。静态情况下，无需深度图，无需MotionVector，那么占用为39.5MB。采样总共15次（5次构建包围盒，5次双三次过滤采样历史帧，5次采样深度精确MotionVector），后续全屏后处理RT为7.9MB

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/dda0fb71-02fc-4358-a722-a0d2081f52ce.png)

MSAA2x使用55.3MB，后续全屏后处理RT为23.7MB

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/33ca93c9-506b-416a-b58d-474ca7f29862.png)

MSAA4x使用102.9MB，后续全屏后处理RT为39.6MB

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgkmMjRdPOWNX/img/c61db039-a50b-43b4-884b-3e80c4e5022d.png)