# 西南交通大学-计算机图形学实验3-2025年


{{< admonition type=note title="" open=false >}}
此笔记针对西南交通大学2025-2026学年上半学期开设的计图实验课
{{< /admonition >}}

{{< admonition type=warning title="" open=false >}}
暂未更新任务2内容
{{< /admonition >}}



<!-- Improved compatibility of back to top link: See: https://github.com/Septemus/swjtu-computergraphics-exp3/pull/73 -->
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
  <a href="https://github.com/Septemus/swjtu-computergraphics-exp3">
    <img src="/images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">西南交通大学-计算机图形学实验3-2025年</h3>

  <p align="center">
    二维图形变换与裁剪实验
    <br />
    <a href="https://septemus.github.io/computer_graphics_exp2/"><strong>访问博客获得更多信息</strong></a>
    <br />
    <br />
    <a href="https://github.com/Septemus/swjtu-computergraphics-exp3">View Demo</a>
    &middot;
    <a href="https://github.com/Septemus/swjtu-computergraphics-exp3/issues/new?labels=bug&template=bug-report---.md">Report Bug</a>
    &middot;
    <a href="https://github.com/Septemus/swjtu-computergraphics-exp3/issues/new?labels=enhancement&template=feature-request---.md">Request Feature</a>
  </p>
</div>



<!-- ABOUT THE PROJECT -->
> # 实验要求



任务1（第8周）：二维图形程交互绘制（参考资料：`计算机图形学实验参考02.pdf`）

在实验二程序框架基础上，根据提供的实验参考资料，逐步修改图形程序框架，实现自定义可绘制图形对象，场景管理功能，参考线段类的实现，添加工具面板按钮，完成以下图形类构建及交互绘制加入场景，交互绘制要能支持橡皮线功能并使用实验二中直线段绘制算法进行测试）:

- 学号单号：折线（鼠标左键单击指定第一点，第二点...右键点击作为最后一点结束），类似GL_LINE_STRIP功能
- 学号双号：闭合线（鼠标左键单击指定第一点，第二点...右键点击最后一点结束），类似GL_LINE_LOOP功能。

任务2(第9周)、二维图形几何变换（参考资料：`计算机图形学实验参考03.pdf`）添加工具面板按钮，实现二维图形的鼠标交互拾取，使用键盘及鼠标控制图形对象的几何变换。

1. 基本几何变换包括：平移、旋转、缩放；按自定义默认参数, 通过派生自定义的事件处理类实现；
2. 复合几何变换假定参考基准点为图形对象中心，绕基准点旋转、基于该基准点缩放（设计交互命令类支持鼠标交互获取角度、缩放比例）。运行程序目录下要写一个操作说明文档`readme.txt`。

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
    

<p align="right">(<a href="#readme-top">back to top</a>)</p>


> # 使用教程

打开`Visual Studio`:

![step1](/images/step1.png)

选择克隆存储库

![step2](/images/step2.png)

粘贴`github`源代码仓库地址：[https://github.com/Septemus/swjtu-computergraphics-exp3](https://github.com/Septemus/swjtu-computergraphics-exp3.git)

![step3](/images/cg/exp3/step3.png)

设置好路径后点击克隆

![step4](/images/step4.png)

点击启动按钮

![step5](/images/step5.png)

启动成功

![step6](/images/cg/exp3/step6.png)

> ## 任务（1）

点击工具栏的直线类，可以看到按钮

![step7](/images/cg/exp3/step7.png)

- 点击`直线段`，然后在绘图区用鼠标左键任意点击两个位置，出现一条新线段，按`ESC`退出
    ![step8](/images/cg/exp3/step8.png)
- 点击`折线（学号单号）`，然后在绘图区用鼠标左键任意点击多个位置，将会依次连接成折线，按鼠标右键点击的位置将成为折线最后一个点的位置，按`ESC`退出
    ![step9](/images/cg/exp3/step9.png)
- 点击`闭合线（学号双号）`，然后在绘图区用鼠标左键任意点击多个位置，将会依次连接成折线，按鼠标右键点击的位置将成为折线最后一个点的位置，并且和第一个位置相连形成闭合线，按`ESC`退出
    ![step10](/images/cg/exp3/step10.png)

<!-- ROADMAP -->
> # 开发路线

- [x] 在Windows 11,Visual Studio 2022上创建MFC APP实现
- [ ] 在MacOS,QT6上创建QT APP实现

查看 [open issues](https://github.com/Septemus/swjtu-computergraphics-exp3/issues) 获取功能和问题列表

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

<a href="https://github.com/Septemus/swjtu-computergraphics-exp3/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=septemus/swjtu-computergraphics-exp3" alt="contrib.rocks image" />
</a>

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- LICENSE -->
> # License

Distributed under the Unlicense License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONTACT -->
> # 联系

博客留言 - [西南交通大学-计算机图形学实验3-2025年](https://septemus.github.io/computer_graphics_exp3/) - [musketeerdt@gmail.com](musketeerdt@gmail.com)

项目源代码仓库: [https://github.com/Septemus/swjtu-computergraphics-exp3](https://github.com/Septemus/swjtu-computergraphics-exp3)

<p align="right">(<a href="#readme-top">back to top</a>)</p>





<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/septemus/swjtu-computergraphics-exp3.svg?style=for-the-badge
[contributors-url]: https://github.com/Septemus/swjtu-computergraphics-exp3/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/septemus/swjtu-computergraphics-exp3.svg?style=for-the-badge
[forks-url]: https://github.com/Septemus/swjtu-computergraphics-exp3/network/members
[stars-shield]: https://img.shields.io/github/stars/septemus/swjtu-computergraphics-exp3.svg?style=for-the-badge
[stars-url]: https://github.com/Septemus/swjtu-computergraphics-exp3/stargazers
[issues-shield]: https://img.shields.io/github/issues/septemus/swjtu-computergraphics-exp3.svg?style=for-the-badge
[issues-url]: https://github.com/Septemus/swjtu-computergraphics-exp3/issues
[license-shield]: https://img.shields.io/github/license/septemus/swjtu-computergraphics-exp3.svg?style=for-the-badge
[license-url]: https://github.com/Septemus/swjtu-computergraphics-exp3/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/septemus
[product-screenshot]: images/screenshot.png
[result]: /images/cg/exp3/result.png
[result2]: images/res2.png
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
