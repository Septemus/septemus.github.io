---
title: "西南交通大学-计算机图形学实验2-2025年"
date: 2025-04-11T22:45:00+08:00
draft: false
categories: ["college"]
featuredImagePreview: "/images/cg/opengl.jpg"
featuredImage: "/images/cg/opengl.jpg"
---
{{< admonition type=note title="" open=false >}}
此笔记针对西南交通大学2025-2026学年上半学期开设的计图实验课
{{< /admonition >}}

{{< admonition type=success title="" open=false >}}
已更新任务2内容
{{< /admonition >}}


{{< admonition type=failure title="" open=false >}}
已知绘图区窗口大小改变时图像会消失，此问题未找到解决方法，如果有读者解决欢迎在评论区提出！
{{< /admonition >}}


﻿<!-- Improved compatibility of back to top link: See: https://github.com/Septemus/swjtu-computergraphics-exp2/pull/73 -->
<a id="readme-top"></a>
<!--
*** Thanks for checking out the swjtu-computergraphics-exp. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![Unlicense License][license-shield]][license-url]



<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/Septemus/swjtu-computergraphics-exp2">
    <img src="/images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">西南交通大学-计算机图形学实验2-2025年</h3>

  <p align="center">
    实验环境与实验程序框架搭建
    <br />
    <a href="https://septemus.github.io/computer_graphics_exp2/"><strong>访问博客获得更多信息</strong></a>
    <br />
    <br />
    <a href="https://github.com/Septemus/swjtu-computergraphics-exp2">View Demo</a>
    &middot;
    <a href="https://github.com/Septemus/swjtu-computergraphics-exp2/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/Septemus/swjtu-computergraphics-exp2/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>



<!-- ABOUT THE PROJECT -->
> # 实验要求



使用实验一的程序项目，根据任务设置程序界面，两周课程依次完成如下任务：


1. 任务（1）（第 6 周） 
    - 实现任意斜率直线段生成算法（DDA 算法、中点算法、Bresenham 算法），每种算法完成任意斜率直线段的绘制。选择 12~24 边的一种正多边形两两顶点相连形成线段进行每种算法测试。（必做）
    - 实现中点画圆算法（必做），以同心圆簇（若干同心圆）与不同位置的圆进行测试；
    - Bresenham 画圆算法、圆弧绘制算法，以同心圆簇（若干同心圆）、0-90 度、0-180 度、0-270 度、0-360 度等范围内多个圆弧进行验证（选做）。
1. 任务（2）（第 7 周）
    - 实现扫描线多边形填充算法（有效边表多边形填充算法）并至少以多个凸、凹多边形进行验证（包括有水平边的多边形）；（必做）
    - 实现种子填充算法（四联通的边界表示、内点表示），并使用自己的画圆算法绘制边界边界表示的点阵区域,再作为内点表示的区域进行填充验证。（选做）

<p align="right">(<a href="#readme-top">back to top</a>)</p>



> # 实验工具



- [![C++][C++]][C++-url]
- [![OpenGL][OpenGL]][OpenGL-url]
- [![Git][Git]][Git-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
> # 实验效果


1. 任务（1）
    [![效果][result]](https://example.com) 
1. 任务（2）
    [![效果][result2]](https://example.com)

<p align="right">(<a href="#readme-top">back to top</a>)</p>


> # 使用教程

> ## 任务（1）

打开`Visual Studio`:

![step1](/images/step1.png)

选择克隆存储库

![step2](/images/step2.png)

粘贴`github`源代码仓库地址：[https://github.com/Septemus/swjtu-computergraphics-exp2](https://github.com/Septemus/swjtu-computergraphics-exp2.git)

![step3](/images/cg/exp2/step3.png)

设置好路径后点击克隆

![step4](/images/step4.png)

点击启动按钮

![step5](/images/step5.png)

启动成功

![step6](/images/cg/exp2/step6.png)

把左侧栏拉宽一点

![step7](/images/cg/exp2/step7.png)

点击正多边形绘制按钮弹出对话框

![step8](/images/cg/exp2/step8.png)

选择算法、正多边形边数、坐标

![step9](/images/cg/exp2/step9.png)

点击确定，正多边形成功生成

![step10](/images/cg/exp2/step10.png)

点击圆绘制按钮弹出对话框

![step11](/images/cg/exp2/step11.png)

选择圆心坐标，半径，弧度（0-360）

![step12](/images/cg/exp2/step12.png)

点击确定，圆弧成功生成

![step13](/images/cg/exp2/step13.png)


> ## 任务（2）

使用最新的代码，可以看到左上工具栏出现新选项

![step2_1](/images/cg/exp2/step2_1.png)

1. 点击`有效边扫描线法填充多边形`按钮一次，进入选择顶点状态
2. 在绘图区鼠标点击任意位置，该位置将成为多边形顶点位置
3. 再点击一次`有效边扫描线法填充多边形`按钮，填充好的多边形出现

{{< bilibili BV1MJ5tz5EQN >}}

<!-- ROADMAP -->
> # 开发路线

- [x] 在Windows 11,Visual Studio 2022上创建MFC APP实现
- [ ] 在MacOS,QT6上创建QT APP实现

查看 [open issues](https://github.com/Septemus/swjtu-computergraphics-exp2/issues) 获取功能和问题列表

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTRIBUTING -->
> # 开源贡献

正是贡献让开源社区成为了学习、启发和创造的绝佳场所。我们非常感谢您的任何贡献。

如果您有改进建议，请分叉仓库并创建拉取请求。您也可以简单地打开一个带有标签“增强”的问题。

别忘了给项目点个星！再次感谢！

1. 分叉项目
2. 创建您的功能分支（`git checkout -b feature/AmazingFeature`）
3. 提交您的更改（`git commit -m 'Add some AmazingFeature'`）
4. 推送到分支（`git push origin feature/AmazingFeature`）
5. 打开拉取请求

> ## 贡献者:

<a href="https://github.com/Septemus/swjtu-computergraphics-exp2/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=septemus/swjtu-computergraphics-exp2" alt="contrib.rocks image" />
</a>

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- LICENSE -->
> # License

Distributed under the Unlicense License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
> # 联系

博客留言 - [西南交通大学-计算机图形学实验2-2025年](https://septemus.github.io/computer_graphics_exp2/) - [musketeerdt@gmail.com](musketeerdt@gmail.com)

项目源代码仓库: [https://github.com/Septemus/swjtu-computergraphics-exp2](https://github.com/Septemus/swjtu-computergraphics-exp2)

<p align="right">(<a href="#readme-top">back to top</a>)</p>





<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/septemus/swjtu-computergraphics-exp2.svg?style=for-the-badge
[contributors-url]: https://github.com/Septemus/swjtu-computergraphics-exp2/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/septemus/swjtu-computergraphics-exp2.svg?style=for-the-badge
[forks-url]: https://github.com/Septemus/swjtu-computergraphics-exp2/network/members
[stars-shield]: https://img.shields.io/github/stars/septemus/swjtu-computergraphics-exp2.svg?style=for-the-badge
[stars-url]: https://github.com/Septemus/swjtu-computergraphics-exp2/stargazers
[issues-shield]: https://img.shields.io/github/issues/septemus/swjtu-computergraphics-exp2.svg?style=for-the-badge
[issues-url]: https://github.com/Septemus/swjtu-computergraphics-exp2/issues
[license-shield]: https://img.shields.io/github/license/septemus/swjtu-computergraphics-exp2.svg?style=for-the-badge
[license-url]: https://github.com/Septemus/swjtu-computergraphics-exp2/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/septemus
[product-screenshot]: images/screenshot.png
[result]: /images/cg_exp2_res.png
[result2]: /images/cg/exp2/res2.png
[Next.js]: https://img.shields.io/badge/next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white
[C++]: https://img.shields.io/badge/c++-000000?style=for-the-badge&logo=cplusplus&logoColor=white
[C++-url]: https://en.wikipedia.org/wiki/C++
[OpenGL]: https://img.shields.io/badge/opengl-000000?style=for-the-badge&logo=opengl&logoColor=white
[OpenGL-url]: https://www.opengl.org/
[Git]: https://img.shields.io/badge/Git-000000?style=for-the-badge&logo=git&logoColor=white
[Git-url]: https://git-scm.com/downloads
[Next-url]: https://nextjs.org/
[React.js]: https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB
[React-url]: https://reactjs.org/
[Vue.js]: https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vuedotjs&logoColor=4FC08D
[Vue-url]: https://vuejs.org/
[Angular.io]: https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white
[Angular-url]: https://angular.io/
[Svelte.dev]: https://img.shields.io/badge/Svelte-4A4A55?style=for-the-badge&logo=svelte&logoColor=FF3E00
[Svelte-url]: https://svelte.dev/
[Laravel.com]: https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white
[Laravel-url]: https://laravel.com
[Bootstrap.com]: https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white
[Bootstrap-url]: https://getbootstrap.com
[JQuery.com]: https://img.shields.io/badge/jQuery-0769AD?style=for-the-badge&logo=jquery&logoColor=white
[JQuery-url]: https://jquery.com 
