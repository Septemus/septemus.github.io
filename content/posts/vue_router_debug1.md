---
title: "Fixed:Vue-router 跳转到指定页面后强行返回主页解决"
date: 2023-10-28T06:57:45-07:00
draft: false
categories: ["develop"]
featuredImagePreview: "/images/vue.png"
featuredImage: "/images/vue.png"
---


{{< admonition type=success title="Fixed" open=false >}}
这个bug已经被解决
{{< /admonition >}}


> # 问题简述 (One-line summary)

vue-router编程式导航跳转到一个页面后强制返回主页


> # 问题复现 (Steps-to-reproduce)


1. 一开始用 `<router-link>` 方式实现没有问题

    ![old](/images/vuerouter_debug_1/original.png)


2. 后来改成编程式导航的方式，结果每次跳转完成后很短时间内返回主页（根路径）

    ![mid](/images/vuerouter_debug_1/middle.png)

    ![final](/images/vuerouter_debug_1/final.png)


3. `router.push`和`router.replace`一样会遇到问题
4. 去掉路由守卫问题仍存在


> # 预期效果 (What is expected)

编程式导航和标签式导航效果一致，跳转到指定页面后只要不被路由守卫拦截就不再跳转

> # 实际效果 (What is actually happening?)

每次跳转完成后很短时间内返回主页（根路径）, 控制台无报错

> # 问题原因 (Reason)

检查很久代码发现外层的a标签href设置为`""`导致点击事件冒泡后默认跳转事件执行，所以会跳转回主页

> # 解决办法 (Solution)

a标签的href属性修改为`javascript:void(0);`

![solution](/images/vuerouter_debug_1/solution.png)