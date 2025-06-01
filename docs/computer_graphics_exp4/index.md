# 西南交通大学-计算机图形学实验4-2025年


{{< admonition type=note title="" open=false >}}
此笔记针对西南交通大学2025-2026学年上半学期开设的计图实验课
{{< /admonition >}}

{{< admonition type=success title="" open=false >}}
学号单号和双号任务均已完成
{{< /admonition >}}

<!-- Improved compatibility of back to top link: See: https://github.com/Septemus/swjtu-computergraphics-exp4/pull/73 -->
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
  <a href="https://github.com/Septemus/swjtu-computergraphics-exp4">
    <img src="/images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">西南交通大学-计算机图形学实验4-2025年</h3>

  <p align="center">
    三维图形建模实验
    <br />
    <a href="https://septemus.github.io/computer_graphics_exp4/"><strong>访问博客获得更多信息</strong></a>
    <br />
    <br />
    <a href="https://github.com/Septemus/swjtu-computergraphics-exp4">View Demo</a>
    &middot;
    <a href="https://github.com/Septemus/swjtu-computergraphics-exp4/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/Septemus/swjtu-computergraphics-exp4/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>



<!-- ABOUT THE PROJECT -->
> # 实验要求




根据实验参考资料 4，完成立方体模型构建。根据以下对应的任务，可在 CGRenderable

基础上派生出对应的图形对象类，实现相关模型构建。在场景中添加图形实例节点进行显示。

1. 立方体模型构建（必选）
2. 对应学号尾数为单号：
    - 球体类（参数是半径、经度与维度方向上的细分数量），默认模型坐标系原点在球体中心，环 Z 轴细分数（相当于经度细分）`slice`、沿 Z 轴方向细分数（相当于维度方向细分数）`stack`。场景实例要求完成球体模型的多实例绘制。可设计面板按钮分别调用弹出对话框输入参数，完成球体线框模型、球体表面模型的绘制。
3. 对应学号尾数为双号：
    - 圆柱类（参数包括下底面半径、上顶面半径、高度、环 Z 轴细分数 `slice`、沿 Z 轴方向细分数 `stack`。要求当上顶面半径为 0 是能实现圆锥体。场景实例要求完成圆柱及体圆锥体的线框模型、球体表面模型的绘制。可设计面板按钮分别调用弹出对话框输入参数，完成圆柱及体圆锥体的多实例绘制。

![demand1](/images/cg/exp4/demand1.png)

![demand2](/images/cg/exp4/demand2.png)



<p align="right">(<a href="#readme-top">back to top</a>)</p>



> # 实验工具



- [![C++][C++]][C++-url]
- [![OpenGL][OpenGL]][OpenGL-url]
- [![Git][Git]][Git-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- GETTING STARTED -->
> # 实验效果

1. 立方体构建
    [![效果][result]](https://example.com) 
1. 球体构建
    - [![属性选择框][result2]](https://example.com)
    - [![效果][result3]](https://example.com)
1. 圆柱/锥体构建
    - [![属性选择框][result4]](https://example.com)
    - [![效果][result5]](https://example.com)


<p align="right">(<a href="#readme-top">back to top</a>)</p>


> # 使用教程

打开`Visual Studio`:

![step1](/images/step1.png)

选择克隆存储库

![step2](/images/step2.png)

粘贴`github`源代码仓库地址：[https://github.com/Septemus/swjtu-computergraphics-exp4](https://github.com/Septemus/swjtu-computergraphics-exp4.git)

![step3](/images/cg/exp4/step3.png)

设置好路径后点击克隆

![step4](/images/step4.png)

点击启动按钮

![step5](/images/step5.png)

启动成功

![step6](/images/cg/exp4/step6.png)

点击工具栏的三维图形类，可以看到按钮

![step7](/images/cg/exp4/step7.png)

> ## 球体（学号单号）

点击`球体`，出现对话框设置球体属性
    
![step8](/images/cg/exp4/step8.png)


设置球体属性

![step9](/images/cg/exp4/step9.png)

点击确定，绘图区出现球体

![step10](/images/cg/exp4/step10.png)

> ## 圆柱体（学号双号）

点击`圆柱`，出现对话框设置圆柱属性

![step2-1](/images/cg/exp4/step2-1.png)

设置圆柱属性

![step2-2](/images/cg/exp4/step2-2.png)

点击确定，绘图区出现圆柱

![step2-3](/images/cg/exp4/step2-3.png)

<!-- ROADMAP -->
> # 开发路线

- [x] 在Windows 11,Visual Studio 2022上创建MFC APP实现
- [ ] 在MacOS,QT6上创建QT APP实现

查看 [open issues](https://github.com/Septemus/swjtu-computergraphics-exp4/issues) 获取功能和问题列表

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

<a href="https://github.com/Septemus/swjtu-computergraphics-exp4/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=septemus/swjtu-computergraphics-exp4" alt="contrib.rocks image" />
</a>

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- LICENSE -->
> # License

Distributed under the Unlicense License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
> # 联系

博客留言 - [西南交通大学-计算机图形学实验4-2025年](https://septemus.github.io/computer_graphics_exp4/) - [musketeerdt@gmail.com](musketeerdt@gmail.com)

项目源代码仓库: [https://github.com/Septemus/swjtu-computergraphics-exp4](https://github.com/Septemus/swjtu-computergraphics-exp4)

<p align="right">(<a href="#readme-top">back to top</a>)</p>





<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/septemus/swjtu-computergraphics-exp4.svg?style=for-the-badge
[contributors-url]: https://github.com/Septemus/swjtu-computergraphics-exp4/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/septemus/swjtu-computergraphics-exp4.svg?style=for-the-badge
[forks-url]: https://github.com/Septemus/swjtu-computergraphics-exp4/network/members
[stars-shield]: https://img.shields.io/github/stars/septemus/swjtu-computergraphics-exp4.svg?style=for-the-badge
[stars-url]: https://github.com/Septemus/swjtu-computergraphics-exp4/stargazers
[issues-shield]: https://img.shields.io/github/issues/septemus/swjtu-computergraphics-exp4.svg?style=for-the-badge
[issues-url]: https://github.com/Septemus/swjtu-computergraphics-exp4/issues
[license-shield]: https://img.shields.io/github/license/septemus/swjtu-computergraphics-exp4.svg?style=for-the-badge
[license-url]: https://github.com/Septemus/swjtu-computergraphics-exp4/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/septemus
[product-screenshot]: images/screenshot.png
[result]: /images/cg/exp4/result.png
[result2]: /images/cg/exp4/result2.png
[result3]: /images/cg/exp4/result3.png
[result4]: /images/cg/exp4/result4.png
[result5]: /images/cg/exp4/result5.png
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
