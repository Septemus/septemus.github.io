---
title: "基于局域网的音视频即时聊天客户端及服务器软件设计与开发"
date: 2023-01-09T18:33:53+08:00
draft: false
categories: ["Projects"]

featuredImagePreview: "/images/Project1/WebRTC_Logo.svg"
featuredImage: "/images/Project1/WebRTC_Logo.svg"
---

{{< admonition type=warning title="" open=false >}}
此项目成员均为学生，还在开发过程中，因此相比企业级项目而言页面简陋技术落后，望看到这篇文章的高手轻喷。并且如果发现BUG或有改进建议，欢迎和我联系！
{{< /admonition >}}

> ## 摘要
本课题拟重点关注应急通信的需求，在临时搭建的局域网通信环境下，设计与开发适用于手机、平板和电脑的音视频即时聊天工具，包括客户端和服务器软件，实现无互联网环境下的局域网即时通信功能。

以下是本课题所用到的技术：

- HTML
- CSS
- Javascript
- Electron
- Cordova
- nodejs

Github源代码：

> ## 模块介绍

> ### 主服务器端

> #### 前端

前端页面的设计包括HTML+CSS的网页展示模块以及基于JavaScript前端脚本模块。  
其中，前端脚本模块所做的工作如下：

1. 利用DOM操作获取到网页中输入框的内容，并进行初步的模式匹配，以防止不合法的输入出现。
2. 利用Ajax机制进行前后端数据通信，通过访问后端服务器所提供的接口URL来进行相关的注册、登录、信息修改以及网页跳转的工作。
3. 在获得了后端服务器发来的成功登录的信息后，将报文中的token保存在浏览器本地的sessionStorage中，并在后续的每次访问中携带该token。

> #### 后端

后端需要引入数据库模块用于记录用户的注册信息。在本项目中使用了MySQL关系型数据库，用过JavaScript操作SQL语句进行数据的增、删、查、改操作。  
服务器对外提供了登录、注册、用户信息修改的接口，以登录接口为例，登录接口的URL地址如下：http://服务器IP:服务端口号/api/login  
后端提供登录、注册、信息增删的服务之前需要采取如下操作：

1. 利用开源的joi模块进行前端所发来的数据的模式识别，以防止不合法的输入被传入数据库。
2. 若因为注册、信息修改等操作导致用户密码被设置或修改，需要利用开源的bscryptjs模块对密码进行加密后再写入数据库，以防止泄密。在每次登录时，需要将从数据库中取出的密码解密后再与前端所发来的密码比对。
3. 在验证用户信息后，主服务器会依据从数据库中获取到的用户信息，利用开源的jsonwebtoken模块生成一个JSON格式的token串，并将该token串以及相应的信息传输给前端，随后前端的每次带权限的请求（如获取WebRTC即时音视频服务、访问主页等）都需要携带此token，后端验证token通过后才提供相应的服务。
此外，服务器需要将前端页面所需要的所有HTML以及相关的CSS样式、JavaScript脚本文件设置成静态资源以方面用户进行访问。

> ### 信令服务器端

> #### WebRTC开发环境搭建

WebRTC目前已经被Trident、Chromium、Webkit等多种浏览器内核所支持，具有很高的兼容性，不需要额外的下载外部模块。但是，如表4-1所示，由于不同厂商在开发WebRTC项目时对同一个接口采用了不同的接口名，不同的浏览器在运行同一个WebRTC应用时可能会出现接口不适配的问题。
| WebRTC标准 |	Chrome |	Firefox |
| ------------ | --- | ------------- | 
| getUserMedia |	webkitGetUserMedia |	getUserMedia |
| RTCPeerConnection |	webkitRTCPeerConnection |	RTCPeerConnection |
| RTCsessionDescription |	RTCsessionDescription |	RTCsessionDescription |
| RTCIceCandidate |	RTCIceCandidate|	RTCIceCandidate |


因此，需要采用WebRTC官方提供的适配器adapter-latest.js文件才能解决如上的兼容性问题。该兼容性解决方案需要在渲染页面时引入，即在即时通话的HTML页面中使用`<script src="adapter-latest.js"></script>`语句引入适配器文件。

![process1](/images/process1.png)

> #### 信令服务器端

1. 服务器使用app.use(express.static(path.join(__dirname, '../public')))语句将对外提供的HTML、CSS以及JavaScript脚本文件设置为静态资源，客户端可以通过URL来访问这些资源以获取即时通信服务。其中，app为信令服务器所创建的HTTPS服务器实例，‘public’为存放客户端文件的目录。

2. 服务器在获取到客户端的URL后，根据URL中携带的jwt token字符进行身份校验，若token验证通过才将URL对应的资源页面提供给客户端，否则，拒绝这次请求。

3. 使用socket.io技术实时监听客户端所发来的数据，以协助通信双方的信令交互。
服务器的处理流程如下图所示：

 <img src='/images/process2.jpg' width='60%' >

> #### 浏览器前端

浏览器前端的所需要完成功能则相对较多，包括获取音视频流、协商通信配置、建立P2P连接等，按照顺序可以分为以下几个步骤：
1. 获取客户端本地的音视频流
由于针对不同的客户端以及浏览器会有不同的硬件设备，需要为这些不同的设备或浏览器提供兼容性的解决方案，因此需要引入由WebRTC官方提供的适配器模块
adapter.js。随后通过getUserMedia函数获取音视频流。

2. 建立PeerConnection对象
在客户端的JavaScript脚本内创建PeerConnection，由于创建、协调并维持通信双方的连接。随后，将PeerConnection的ontrack成员方法与远程视频流绑定，将
PeerConnection的addStream成员方法与本地视频流绑定。

3. 加入房间
在访问即时音视频通信服务中，会在get请求中附带room参数，在成功获取到服务后，前端会向信令服务器使用socket.io的emit函数发送一个名为rooms的事件，事
件携带的数据为get请求中room的参数。  
服务器监听到rooms事件后，会将该客户加入值为room的房间，随后，该客户的所有信令信息仅在值为room的房间中转发。

4. 协商会话描述配置
受限于通信双方的硬件设置等因素的影响，在正式通信之前通信双方需要协商通信的配置信息。主叫向被叫发送PeerConnection的成员变量 localDescription，被
叫通过使用PeerConnection的成员方法setRemoteDescription来实现主叫与被叫之间的会话描述配置。  
客户端通过socket.io的emit函数发送一个名为message的事件，事件携带的参数为localDescription。

5. 协商连接双方的网络信息
由于通信双方可能处于NAT网络之后，需要通过ICE服务器提供的内网穿透服务才能正式建立连接，因此通信双方之间需要发送RTCIceCandidate这一对象，该对象包
含的属性包括本地IP地址、公网IP地址等等所有相关网络配置信息。  
该配置信息的发送是基于socke.io发送的名为message的事件来实现。

6. 建立P2P连接
主叫通过调用PeerConnection的成员方法createOffer向被叫发起建立连接请求，被叫收到请求后可以拒绝这个请求或调用PeerConnection的成员方法createAnswer
来响应这个请求。  
主叫与被叫所发送的信息都是基于socket.io的emit函数来发送一个名为message的事件。

> ### 移动端

由于项目基于web开发，所以选择cordova框架进行打包移植。打包的流程大致如下：

1. 相关的环境配置

2. 创造cordova项目

3. 在项目中添加移动端平台

4. 将前端页面文件移入www文件夹

5. 将页面布局调整以适应手机大小

6. 在config.xml中修改权限解决跨域问题

7. 生成app

8. 后续实机调试 

> ## 核心代码

> ### 注册和登录

> #### 前端
为按钮绑定ajax事件将用户输入的信息传到后端，根据后端返回信息决定下一步。

自动获取ip地址：

```Javascript
var ip
window.RTCPeerConnection = window.RTCPeerConnection || window.mozRTCPeerConnection || window.webkitRTCPeerConnection; //compatibility for Firefox and chrome
if (!RTCPeerConnection) {

  let win = iframe.contentWindow;
  RTCPeerConnection = win.RTCPeerConnection || win.mozRTCPeerConnection || win.webkitRTCPeerConnection;
}
var pc = new RTCPeerConnection({iceServers:[]}), noop = function(){};      
pc.createDataChannel(''); //create a bogus data channel
pc.createOffer(pc.setLocalDescription.bind(pc), noop); // create offer and set local description
pc.onicecandidate = function(ice){
    if (ice && ice.candidate && ice.candidate.candidate){
       ip = /([0-9]{1,3}(\.[0-9]{1,3}){3}|[a-f0-9]{1,4}(:[a-f0-9]{1,4}){7})/.exec(ice.candidate.candidate)[1];
       console.log('my IP: ', ip);   
       pc.onicecandidate = noop;
     }
};
try{
  if(!ip) ip=/([0-9]{1,3}(\.[0-9]{1,3}){3}|[a-f0-9]{1,4}(:[a-f0-9]{1,4}){7})/.exec(window.location.href)[1]
}catch(err){
  ip='localhost'
}

```

```Javascript


let login_btn = document.getElementById('login_btn');
let id = document.getElementById('id');
let password = document.getElementById('password');
$('#login_btn').on('click', function () {
    var params = 'id=' + id.value + '&password=' + password.value;
    console.log("clicked login")
    $.ajax({
        type: 'post',
        url: 'http://' + ip + ':3007/api/login',
        contentType: 'application/x-www-form-urlencoded',
        data: params,
        success: function (result) {
            window.localStorage.setItem(result.id, result.id);
            sessionStorage.name = result.name;
            sessionStorage.id = result.id;
            sessionStorage.serverIP = result.serverIP;
            if (result.status === 0) {
                alert("登录成功,跳转至主界面");
                window.location.href = "./HomePage.html";
            }
            else
                alert(result.message);
        }
    })
})
let register = document.getElementById('register');
let Rid = document.getElementById('Rid');
let Rname = document.getElementById('Rname');
let Rpassword = document.getElementById('Rpassword');
$('#register').on('click',function () {
    var params = "id=" + Rid.value + "&password=" + Rpassword.value + "&name=" + Rname.value;
    console.log(params)
    console.log('http://' + ip + ':3007/api/reguser')
    $.ajax({
        type: 'post',
        url: 'http://' + ip + ':3007/api/reguser',
        contentType: 'application/x-www-form-urlencoded',
        data: params,
    }).then(result => {
        if (result.status === 0) {
            alert("注册成功,点击回到登陆界面");
            window.location.reload()
        }
        else {
            alert(result.message);  
        }
    })
    .catch(err=>{
        console.log("failure:",err)
        alert('something wrong')
    })
})

```

> #### 后端
在数据库中检索用户输入信息并执行相关操作
```Javascript
exports.regUser = (req, res) => {
  // 获取客户端提交到服务器的用户信息
  const userinfo = req.body;

  // 定义 SQL 语句，查询用户名是否被占用
  const sqlStr = 'select * from users where id=?';
  db.query(sqlStr, userinfo.id, (err, results) => {
    // 执行 SQL 语句失败
    if (err) {
      return res.cc(err);
    }
    // 判断用户名是否被占用
    if (results.length > 0) {
      return res.cc('用户名被占用，请更换其他用户名！', 2);
    }
    // 调用 bcrypt.hashSync() 对密码进行加密
    userinfo.password = bcrypt.hashSync(userinfo.password, 10);

    // 定义插入新用户的 SQL 语句
    const sql = 'insert into users set ?';
    // 调用 db.query() 执行 SQL 语句
    db.query(sql, { id: userinfo.id, password: userinfo.password, name: userinfo.name }, (err, results) => {
      // 判断 SQL 语句是否执行成功
      // if (err) return res.send({ status: 1, message: err.message })
      if (err) return res.cc(err);
      // 判断影响行数是否为 1
      if (results.affectedRows !== 1) return res.cc('注册用户失败，请稍后再试！', 1);
      // 注册用户成功
      res.cc('注册成功！', 0, 'http://' + ip + ':3007');
    })
  })
}

// 登录的处理函数
exports.login = (req, res) => {
  console.log("login post received!")
  const userinfo = req.body;
  console.log(userinfo)
  const sql = 'select * from users where id = ?';
  db.query(sql, userinfo.id, (err, results) => {
    if (err) {
      console.log("error!")
      return res.cc(err);
    }
    if (results.length !== 1) return res.cc('登陆失败');

    //比较密码是否正确
    const compare = bcrypt.compareSync(userinfo.password, results[0].password);
    if (!compare) return res.cc('密码输入错误');
    //else return res.cc('登陆成功', 0);

    const user = { ...results[0], password: '', user_pic: '' };//...为展开运算符，将results[0]中所有元素赋给user
    //利用用户信息生成token
    const token = jwttoken.sign(user, jwtconfig.jwtSecretKey, { expiresIn: jwtconfig.expiresIn });//有效期为3小时
    res.send({
      status: 0,
      message: '登陆成功！',
      token: 'Bearer ' + token,
      url: 'http://' + ip + ':3007/HomePage.html',
      name: results[0].name,
      id: results[0].id,
      serverIP: ip
    })
  })
}

```

> ### 用户界面
通过socket实现用户列表的显示和更新
> #### 前端
```Javascript
var welcome = document.getElementById('welcome');
    welcome.innerHTML = '欢迎 ' + sessionStorage.name;
    const socket = io(sessionStorage.serverIP + ':3007');

    socket.on("connect", () => {
      sessionStorage.socketID = socket.id;
      socket.emit('login', JSON.stringify({ 'id': sessionStorage.id, 'name': sessionStorage.name, 'sid': sessionStorage.socketID }));
    });

    socket.on('called', (data) => {
      var info = JSON.parse(data);
      if (info.calledID == sessionStorage.id) {
        window.blur(); setTimeout(window.focus(), 100);
        var r = window.confirm('您正在被' + info.callingID + '呼叫！');
        if (r == false) {
          socket.emit('refuse', JSON.stringify({ 'name': sessionStorage.name, 'callingSid': info.callingSid }));
        }
        else {
          window.open('https://' + sessionStorage.serverIP + ':8443/index.html?room=' + info.callingID+'&id='+sessionStorage.id);
          socket.emit('agree', info.callingSid);
        }
      }
    })
    
    socket.on('refuse', (data) => {
      alert(data + '拒绝了您的通话请求！');
    });

    socket.on('agree', () => {
      console.log(1);
      window.open('https://' + sessionStorage.serverIP + ':8443/index.html?room=' + sessionStorage.id+'&id='+sessionStorage.id);
    })
    socket.on('joinroom',(data) => {
      var info = JSON.parse(data);
      // window.blur(); setTimeout(window.focus(), 100);
      //   var r = window.confirm('您是否要加入' + info.roomid + '房间！');
        window.open('https://' + sessionStorage.serverIP + ':8443/index2.html?name='+sessionStorage.name);
        //socket.emit('agree', info.callingSid);
    })
    //const roomName = document.getElementById("roomName"); // 房间号输入框
    const joinRoom = document.getElementById("joinRoom"); // 加入房间按钮
    //console.log(sessionStorage.name);
    const socket = io(sessionStorage.serverIP + ':3007');
    var table = document.getElementById('table');

    socket.on('init', data => {
        for (var i = 0; i < data.length; i++) {
            if (data[i].id != sessionStorage.id) {
                var tr = document.createElement('tr');
                table.appendChild(tr);
                //创建Sid栏
                var td_sid = document.createElement('td');
                td_sid.innerHTML = data[i].sid;
                tr.appendChild(td_sid);
                //创建id栏
                var td_id = document.createElement('td');
                td_id.innerHTML = data[i].id;
                td_id.id = data[i].id;
                tr.appendChild(td_id);
                //创建name栏
                var td_name = document.createElement('td');
                td_name.innerHTML = data[i].name;
                tr.appendChild(td_name);
                //创建会话图标栏
                var td_RTC = document.createElement('td');
                //创建图标
                var button = document.createElement('button');
                button.addEventListener('click', () => {
                    var data = JSON.stringify({ 'callingID': sessionStorage.id, 'calledID': td_id.id, 'callingSid': sessionStorage.socketID });
                    socket.emit('calling', data);
                });
                var img = document.createElement('img');
                img.setAttribute('src', '../assets/images/camera.webp');
                img.setAttribute('height', '30px');
                button.appendChild(img);
                tr.appendChild(button);
            }
        }
    })

    socket.on('online', (data) => {
        var user = JSON.parse(data);
        if (user.id != sessionStorage.id) {
            //动态创建行
            var tr = document.createElement('tr');
            table.appendChild(tr);
            //创建Sid栏
            var td_sid = document.createElement('td');
            td_sid.innerHTML = user.sid;
            tr.appendChild(td_sid);
            //创建id栏
            var td_id = document.createElement('td');
            td_id.innerHTML = user.id;
            td_id.id = user.id;
            tr.appendChild(td_id);
            //创建name栏
            var td_name = document.createElement('td');
            td_name.innerHTML = user.name;
            tr.appendChild(td_name);
            //创建会话图标栏
            var td_RTC = document.createElement('td');
            //创建图标
            var button = document.createElement('button');
            button.addEventListener('click', () => {
                var data = JSON.stringify({ 'callingID': sessionStorage.id, 'calledID': td_id.id, 'callingSid': sessionStorage.socketID });
                socket.emit('calling', data);
            });
            var img = document.createElement('img');
            img.setAttribute('src', '../assets/images/camera.webp');
            img.setAttribute('height', '30px');
            button.appendChild(img);
            tr.appendChild(button);
        }
    });
    joinRoom.onclick = function () {
        //var data = JSON.stringify({ 'callingID': sessionStorage.id, 'callingSid': sessionStorage.socketID , 'roomid':roomName.value});
        var data = JSON.stringify({ 'callingID': sessionStorage.id, 'callingSid': sessionStorage.socketID });
        console.log(data);
        socket.emit('joinroom', data);
    }
    socket.on('offline', (data) => {
        const table = document.getElementById('table');
        for (var i = 1; i < table.rows.length; i++) {
            //console.log(table.rows[i].cells[0].innerHTML);
            if (table.rows[i].cells[0].innerHTML == data)
                table.deleteRow(i);
        }
    });
```

> #### 后端

```Javascript
// 导入 express
const express = require('express');
// 创建服务器的实例对象
const app = express();
const joi = require('@hapi/joi');
const os = require('os');
// 获取IP地址
const {getIpAddress} = require('./getIpAddress')
const ip = getIpAddress();
//引入socket.io
const { createServer } = require("http");
const httpServer = createServer(app);
const { Server } = require("socket.io");
const io = new Server(httpServer, {
  cors: {
    origin: '*',
    allowedHeaders: ['Content-Type'],
  }
});
// 导入并配置 cors 中间件
const cors = require('cors');
app.use(cors({
  origin: '*',
  methods: ['GET', 'POST'],
  allowedHeaders: ['Content-Type'],
}));



//设置静态登陆界面
const path = require('path')
app.use(express.static(path.join(__dirname, 'public')));

// 配置解析表单数据的中间件，只能解析 application/x-www-form-urlencoded 格式的表单数据
app.use(express.urlencoded({ extended: false }));

// 封装 res.cc 函数
app.use((req, res, next) => {
  // status 默认值为 1，表示失败的情况
  // err 的值，可能是一个错误对象，也可能是一个错误的描述字符串
  res.cc = function (err, status = 1, url) {
    res.send({
      status,
      message: err instanceof Error ? err.message : err,
      url: url
    })
  }
  next();
})


//导入并配置jwt解析的中间件
const config = require('./config');
const jwt = require('express-jwt');
//app.use(jwt({ secret: config.jwtSecretKey }).unless({ path: [/^\/api\//] }));

// 导入并使用用户路由模块
const userRouter = require('./router/user');
app.use('/api', userRouter);
const userinfo = require('./router/userinfo');
app.use('/my', userinfo);

// 定义错误级别的中间件
app.use((err, req, res, next) => {
  // 验证失败导致的错误
  if (err instanceof joi.ValidationError) return res.cc(err);
  if (err.name === 'UnauthorizedError') return res.cc('身份验证失败')
  // 未知的错误
  res.cc(err);
})

const L = require("list");
var l = L.list(); //用户列表

io.on('connect', (socket) => {
  console.log(socket.id)
  io.to(socket.id).emit('init', L.toArray(l));

  socket.on('login', (data) => {
    const info = JSON.parse(data);
    l = L.append({ 'sid': info.sid, 'id': info.id, 'name': info.name }, l);//当io监听到有人登录 将sid、id和名字添加到list
    io.emit('online', data);
  })

  socket.on('disconnect', () => {
    io.emit('offline', socket.id);
    var a = L.toArray(l);
    for (var i = 0; i < a.length; i++) {  //监听到有人退出，从列表中把推出的用户信息删除
      if (a[i].sid === socket.id) {
        l = L.remove(i, 1, l);
        return;
      }
    }
  })

  socket.on('calling', (data) => {
    io.emit('called', data);
  });
  socket.on('refuse', (data) => {
    var info = JSON.parse(data);
    io.to(info.callingSid).emit('refuse', info.name); //
  });
  socket.on('joinroom', (data) => {
    var tmp=JSON.parse(data)
    io.to(tmp.callingSid).emit('joinroom', data);
  });
  socket.on('agree', callingSid => {
    console.log(callingSid);
    io.to(callingSid).emit('agree',);
  })
})

// 启动服务器
httpServer.listen(3007, () => {
  console.log('api server running at http://' + ip + ':3007');
})

```

> ### 通话页面

> #### 前端

创建房间页：

```Javascript
const createButton = document.querySelector("#createroom");
const videoCont = document.querySelector('.video-self');
const codeCont = document.querySelector('#roomcode');
const joinBut = document.querySelector('#joinroom');
const mic = document.querySelector('#mic');
const cam = document.querySelector('#webcam');

let micAllowed = 1;
let camAllowed = 1;

let mediaConstraints = {
    video: true,
    audio: true
};


navigator.mediaDevices.getUserMedia(mediaConstraints).then(localstream => {
    videoCont.srcObject = localstream;
})

//  Generating room code
function uuidv4() {
    return 'xxyxyxxyx'.replace(/[xy]/g, function (c) {
        var r = Math.random() * 16 | 0,
            v = c == 'x' ? r : (r & 0x3 | 0x8);
        return v.toString(16);
    });
}

//  Creating Room
const createroomtext = 'Creating Room...';

createButton.addEventListener('click', (e) => {
    e.preventDefault();
    createButton.disabled = true;
    createButton.innerHTML = 'Creating Room';
    createButton.classList = 'createroom-clicked';

    setInterval(() => {
        if (createButton.innerHTML < createroomtext) {
            createButton.innerHTML = createroomtext.substring(0, createButton.innerHTML.length + 1);
        } else {
            createButton.innerHTML = createroomtext.substring(0, createButton.innerHTML.length - 3);
        }
    }, 500);

    location.href = `/room.html?room=${uuidv4()}&name=${myname}`;
});

//  Joining Room
joinBut.addEventListener('click', (e) => {
    e.preventDefault();
    if (codeCont.value.trim() == "") {
        codeCont.classList.add('roomcode-error');
        return;
    }
    const code = codeCont.value;
    location.href = `/room.html?room=${code}&name=${myname}`;
})

codeCont.addEventListener('change', (e) => {
    e.preventDefault();
    if (codeCont.value.trim() !== "") {
        codeCont.classList.remove('roomcode-error');
        return;
    }
})

//  Index page cam/audio
cam.addEventListener('click', () => {
    if (camAllowed) {
        mediaConstraints = {
            video: false,
            audio: micAllowed ? true : false
        };
        navigator.mediaDevices.getUserMedia(mediaConstraints)
            .then(localstream => {
                videoCont.srcObject = localstream;
            })

        cam.classList = "nodevice";
        cam.innerHTML = `<i class="fas fa-video-slash"></i>`;
        camAllowed = 0;
    } else {
        mediaConstraints = {
            video: true,
            audio: micAllowed ? true : false
        };
        navigator.mediaDevices.getUserMedia(mediaConstraints)
            .then(localstream => {
                videoCont.srcObject = localstream;
            })

        cam.classList = "device";
        cam.innerHTML = `<i class="fas fa-video"></i>`;
        camAllowed = 1;
    }
})

mic.addEventListener('click', () => {
    if (micAllowed) {
        mediaConstraints = {
            video: camAllowed ? true : false,
            audio: false
        };
        navigator.mediaDevices.getUserMedia(mediaConstraints)
            .then(localstream => {
                videoCont.srcObject = localstream;
            })

        mic.classList = "nodevice";
        mic.innerHTML = `<i class="fas fa-microphone-slash"></i>`;
        micAllowed = 0;
    } else {
        mediaConstraints = {
            video: camAllowed ? true : false,
            audio: true
        };
        navigator.mediaDevices.getUserMedia(mediaConstraints)
            .then(localstream => {
                videoCont.srcObject = localstream;
            })

        mic.innerHTML = `<i class="fas fa-microphone"></i>`;
        mic.classList = "device";
        micAllowed = 1;
    }
})

//  Index Clock
function startTime() {
    const today = new Date();
    let h = today.getHours();
    let m = today.getMinutes();
    let s = today.getSeconds();
    m = checkTime(m);
    s = checkTime(s);
    document.querySelector('.index-time').innerHTML = h + ":" + m + ":" + s;
    setTimeout(startTime, 1000);
}

function checkTime(i) {
    if (i < 10) {
        i = "0" + i
    }; // add zero in front of numbers < 10
    return i;
}

startTime();
```

房间页面：

```Javascript
const socket = io();
const overlayContainer = document.querySelector('#overlay')
const continueButt = document.querySelector('.continue-name');
const nameField = document.querySelector('#name-field');
const chatRoom = document.querySelector('.chat-cont');
const sendButton = document.querySelector('.chat-send');
const messageField = document.querySelector('.chat-input');
const cutCall = document.querySelector('.cutcall');
let chatToggle = document.querySelector(".chatting");

//  Room id
const roomid = params.get("room");
document.querySelector('.roomcode').innerHTML = `${roomid}`

//  name set
let vidCon;

let username = params.get('name')

if (username) {
    overlayContainer.classList.add("hidden");
    //overlayContainer.style.visibility = 'hidden';
    document.querySelector("#myname").innerHTML = `${username} (You)`;
    socket.emit("join room", roomid, username);
}
else {
    continueButt.addEventListener('click', () => {
        if (nameField.value == '') return;
        username = nameField.value;
        overlayContainer.classList.add("hidden");
        //overlayContainer.style.visibility = 'hidden';
        document.querySelector("#myname").innerHTML = `${username} (You)`;
        socket.emit("join room", roomid, username);
    })
}


nameField.addEventListener("keyup", function (event) {
    if (event.keyCode === 13) {
        event.preventDefault();
        continueButt.click();
    }
});

//  Chat
sendButton.addEventListener('click', () => {
    const msg = messageField.value;
    messageField.value = '';
    // socket.emit('message', msg, username, roomid);
    var time = getTime()
    var tmp = JSON.stringify({
        msg,
        username,
        roomid,
        time
    })
    console.log(tmp)
    socket.emit('message', tmp);
})

messageField.addEventListener("keyup", function (event) {
    if (event.keyCode === 13) {
        event.preventDefault();
        sendButton.click();
    }
});

socket.on('message', (message) => {
    message = JSON.parse(message)
    chatRoom.scrollTop = chatRoom.scrollHeight;
    let time = message.time
    time = `${time.h}:${time.m}:${time.s}`
    chatRoom.innerHTML += `<div class="message">
    <div class="info">
        <div class="username">${message.username}</div>
        <div class="time">${time}</div>
    </div>
    <div class="content">
        ${message.msg}
    </div>
</div>`
});

//  End Meet
cutCall.addEventListener('click', () => {
    location.href = `/index2.html?name=${username}`;
})

//  Meet Clock

function getTime() {
    const today = new Date();
    let h = today.getHours();
    let m = today.getMinutes();
    let s = today.getSeconds();
    m = checkTime(m);
    s = checkTime(s);
    return {
        h, m, s
    }
}

function startTime() {
    var cur = getTime()
    document.querySelector('.meet-time').innerHTML = cur.h + ":" + cur.m + ":" + cur.s;
    setTimeout(startTime, 1000);
}

function checkTime(i) {
    if (i < 10) {
        i = "0" + i
    }; // add zero in front of numbers < 10
    return i;
}

startTime();

//  Chat slide
let chatContainer = document.querySelector(".right-cont");
chatToggle.addEventListener('click', () => {
    chatContainer.classList.toggle("hidden");
});

let xchat=document.getElementById('turnoff_chat')
xchat.addEventListener('click',()=>{
    chatContainer.classList.toggle("hidden");
})
///  Full Screen
function openFullscreen(elem) {
    if (elem.requestFullscreen) {
        elem.requestFullscreen();
    } else if (elem.webkitRequestFullscreen) {
        /* Safari */
        elem.webkitRequestFullscreen();
    } else if (elem.msRequestFullscreen) {
        /* IE11 */
        elem.msRequestFullscreen();
    }
}


function allFullScreen() {
    //console.log("count is " + count);
    let fullBut = document.querySelectorAll(`.full-screen`);
    for (let i = 0; i < fullBut.length; i++) {
        //console.log("here + " + i + i);
        fullBut[i].addEventListener('click', () => {
            let fullVideo = fullBut[i].parentNode;
            openFullscreen(fullVideo);
        })
    }
    setTimeout(allFullScreen, 1);
}

allFullScreen();
const myvideo = document.querySelector("#vd1");
const videoContainer = document.querySelector('#vcont');
const videoButt = document.querySelector('.novideo');
const audioButt = document.querySelector('.audio');

let videoAllowed = 1;
let audioAllowed = 1;

let micInfo = {};
let videoInfo = {};

let videoTrackReceived = {};

let mymuteicon = document.querySelector("#mymuteicon");
mymuteicon.style.visibility = 'hidden';

let myvideooff = document.querySelector("#myvideooff");
myvideooff.style.visibility = 'hidden';

const configuration = {
    iceServers: [{
        urls: "stun:stun.stunprotocol.org"
    }]
}

const mediaConstraints = {
    video: true,
    audio: true
};

let connections = {};
let cName = {};
let audioTrackSent = {};
let videoTrackSent = {};

let mystream;

function CopyClassText() {

    var textToCopy = document.querySelector('.roomcode');
    var currentRange;
    if (document.getSelection().rangeCount > 0) {
        currentRange = document.getSelection().getRangeAt(0);
        window.getSelection().removeRange(currentRange);
    } else {
        currentRange = false;
    }

    var CopyRange = document.createRange();
    CopyRange.selectNode(textToCopy);
    window.getSelection().addRange(CopyRange);
    document.execCommand("copy");

    window.getSelection().removeRange(CopyRange);

    if (currentRange) {
        window.getSelection().addRange(currentRange);
    }

    document.querySelector(".copycode-button").textContent = "Copied!"
    setTimeout(() => {
        document.querySelector(".copycode-button").textContent = "Copy Code";
    }, 5000);
}

socket.on('user count', count => {
    if (count > 1) {
        videoContainer.className = 'video-cont';
    } else {
        videoContainer.className = 'video-cont-single';
    }
})

let peerConnection;

function handleGetUserMediaError(e) {
    switch (e.name) {
        case "NotFoundError":
            alert("Unable to open your call because no camera and/or microphone" +
                "were found.");
            break;
        case "SecurityError":
        case "PermissionDeniedError":
            break;
        default:
            alert("Error opening your camera and/or microphone: " + e.message);
            break;
    }

}


function reportError(e) {
    console.log(e);
    return;
}


function startCall() {

    navigator.mediaDevices.getUserMedia(mediaConstraints)
        .then(localStream => {
            myvideo.srcObject = localStream;
            myvideo.muted = true;

            localStream.getTracks().forEach(track => {
                for (let key in connections) {
                    connections[key].addTrack(track, localStream);
                    if (track.kind === 'audio')
                        audioTrackSent[key] = track;
                    else
                        videoTrackSent[key] = track;
                }
            })

        })
        .catch(handleGetUserMediaError);


}

function handleVideoOffer(offer, sid, cname, micinf, vidinf) {

    cName[sid] = cname;
    console.log('video offered recevied');
    micInfo[sid] = micinf;
    videoInfo[sid] = vidinf;
    connections[sid] = new RTCPeerConnection(configuration);

    connections[sid].onicecandidate = function (event) {
        if (event.candidate) {
            console.log('icecandidate fired');
            socket.emit('new icecandidate', event.candidate, sid);
        }
    };

    connections[sid].ontrack = function (event) {

        if (!document.getElementById(sid)) {
            console.log('track event fired')
            let vidCont = document.createElement('div');
            let newvideo = document.createElement('video');
            let name = document.createElement('div');
            let muteIcon = document.createElement('div');
            let videoOff = document.createElement('div');
            let fullScreen = document.createElement('div');
            videoOff.classList.add('video-off');
            muteIcon.classList.add('mute-icon');
            fullScreen.classList.add('full-screen');
            name.classList.add('nametag');
            name.innerHTML = `${cName[sid]}`;
            vidCont.id = sid;
            muteIcon.id = `mute${sid}`;
            videoOff.id = `vidoff${sid}`;
            muteIcon.innerHTML = `<i class="fas fa-microphone-slash"></i>`;
            fullScreen.innerHTML = `<i class="fas fa-compress"></i>`;
            videoOff.innerHTML = 'Video Off'
            vidCont.classList.add('video-box');
            newvideo.classList.add('video-frame');
            newvideo.autoplay = true;
            newvideo.playsinline = true;
            newvideo.id = `video${sid}`;
            newvideo.srcObject = event.streams[0];
            
            if (micInfo[sid] == 'on')
                muteIcon.style.visibility = 'hidden';
            else
                muteIcon.style.visibility = 'visible';

            if (videoInfo[sid] == 'on')
                videoOff.style.visibility = 'hidden';
            else
                videoOff.style.visibility = 'visible';

            vidCont.appendChild(newvideo);
            vidCont.appendChild(name);
            vidCont.appendChild(muteIcon);
            vidCont.appendChild(videoOff);
            vidCont.appendChild(fullScreen);

            videoContainer.appendChild(vidCont);

        }


    };

    connections[sid].onremovetrack = function (event) {
        if (document.getElementById(sid)) {
            document.getElementById(sid).remove();
            console.log('removed a track');
        }
    };

    connections[sid].onnegotiationneeded = function () {

        connections[sid].createOffer()
            .then(function (offer) {
                return connections[sid].setLocalDescription(offer);
            })
            .then(function () {

                socket.emit('video-offer', connections[sid].localDescription, sid);

            })
            .catch(reportError);
    };

    let desc = new RTCSessionDescription(offer);

    connections[sid].setRemoteDescription(desc)
        .then(() => {
            return navigator.mediaDevices.getUserMedia(mediaConstraints)
        })
        .then((localStream) => {

            localStream.getTracks().forEach(track => {
                connections[sid].addTrack(track, localStream);
                console.log('added local stream to peer')
                if (track.kind === 'audio') {
                    audioTrackSent[sid] = track;
                    if (!audioAllowed)
                        audioTrackSent[sid].enabled = false;
                } else {
                    videoTrackSent[sid] = track;
                    if (!videoAllowed)
                        videoTrackSent[sid].enabled = false
                }
            })

        })
        .then(() => {
            return connections[sid].createAnswer();
        })
        .then(answer => {
            return connections[sid].setLocalDescription(answer);
        })
        .then(() => {
            socket.emit('video-answer', connections[sid].localDescription, sid);
        })
        .catch(handleGetUserMediaError);


}

function handleNewIceCandidate(candidate, sid) {
    console.log('new candidate recieved')
    var newcandidate = new RTCIceCandidate(candidate);

    connections[sid].addIceCandidate(newcandidate)
        .catch(reportError);
}

function handleVideoAnswer(answer, sid) {
    console.log('answered the offer')
    const ans = new RTCSessionDescription(answer);
    connections[sid].setRemoteDescription(ans);
}

socket.on('video-offer', handleVideoOffer);

socket.on('new icecandidate', handleNewIceCandidate);

socket.on('video-answer', handleVideoAnswer);


socket.on('join room', async (conc, cnames, micinfo, videoinfo) => {
    socket.emit('getCanvas');
    if (cnames)
        cName = cnames;

    if (micinfo)
        micInfo = micinfo;

    if (videoinfo)
        videoInfo = videoinfo;


    console.log(cName);
    if (conc) {
        await conc.forEach(sid => {
            connections[sid] = new RTCPeerConnection(configuration);

            connections[sid].onicecandidate = function (event) {
                if (event.candidate) {
                    console.log('icecandidate fired');
                    socket.emit('new icecandidate', event.candidate, sid);
                }
            };

            connections[sid].ontrack = function (event) {

                if (!document.getElementById(sid)) {
                    console.log('track event fired')
                    let vidCont = document.createElement('div');
                    let newvideo = document.createElement('video');
                    let name = document.createElement('div');
                    let muteIcon = document.createElement('div');
                    let videoOff = document.createElement('div');
                    let fullScreen = document.createElement('div');
                    videoOff.classList.add('video-off');
                    muteIcon.classList.add('mute-icon');
                    fullScreen.classList.add('full-screen');
                    name.classList.add('nametag');
                    name.innerHTML = `${cName[sid]}`;
                    vidCont.id = sid;
                    muteIcon.id = `mute${sid}`;
                    videoOff.id = `vidoff${sid}`;
                    muteIcon.innerHTML = `<i class="fas fa-microphone-slash"></i>`;
                    fullScreen.innerHTML = `<i class="fas fa-compress"></i>`;
                    videoOff.innerHTML = 'Video Off'
                    vidCont.classList.add('video-box');
                    newvideo.classList.add('video-frame');
                    newvideo.autoplay = true;
                    newvideo.playsinline = true;
                    newvideo.id = `video${sid}`;
                    newvideo.srcObject = event.streams[0];
                    console.log('this is the remote stream:',event.streams[0])
                    
                    if (micInfo[sid] == 'on')
                        muteIcon.style.visibility = 'hidden';
                    else
                        muteIcon.style.visibility = 'visible';

                    if (videoInfo[sid] == 'on')
                        videoOff.style.visibility = 'hidden';
                    else
                        videoOff.style.visibility = 'visible';

                    vidCont.appendChild(newvideo);
                    vidCont.appendChild(name);
                    vidCont.appendChild(muteIcon);
                    vidCont.appendChild(videoOff);
                    vidCont.appendChild(fullScreen);

                    videoContainer.appendChild(vidCont);

                }

            };

            connections[sid].onremovetrack = function (event) {
                if (document.getElementById(sid)) {
                    document.getElementById(sid).remove();
                }
            }

            connections[sid].onnegotiationneeded = function () {

                connections[sid].createOffer()
                    .then(function (offer) {
                        return connections[sid].setLocalDescription(offer);
                    })
                    .then(function () {

                        socket.emit('video-offer', connections[sid].localDescription, sid);

                    })
                    .catch(reportError);
            };

        });

        console.log('added all sockets to connections');
        startCall();

    } else {
        console.log('waiting for someone to join');
        navigator.mediaDevices.getUserMedia(mediaConstraints)
            .then(localStream => {
                myvideo.srcObject = localStream;
                myvideo.muted = true;
                mystream = localStream;
            })
            .catch(handleGetUserMediaError);
    }
})

socket.on('remove peer', sid => {
    if (document.getElementById(sid)) {
        document.getElementById(sid).remove();
    }

    delete connections[sid];
})

videoButt.addEventListener('click', () => {

    if (videoAllowed) {
        for (let key in videoTrackSent) {
            videoTrackSent[key].enabled = false;
        }
        videoButt.innerHTML = `<i class="fas fa-video-slash"></i>`;
        videoAllowed = 0;
        videoButt.style.backgroundColor = "#b12c2c";

        if (mystream) {
            mystream.getTracks().forEach(track => {
                if (track.kind === 'video') {
                    track.enabled = false;
                }
            })
        }

        myvideooff.style.visibility = 'visible';

        socket.emit('action', 'videooff');
    } else {
        for (let key in videoTrackSent) {
            videoTrackSent[key].enabled = true;
        }
        videoButt.innerHTML = `<i class="fas fa-video"></i>`;
        videoAllowed = 1;
        videoButt.style.backgroundColor = "#4ECCA3";
        if (mystream) {
            mystream.getTracks().forEach(track => {
                if (track.kind === 'video')
                    track.enabled = true;
            })
        }


        myvideooff.style.visibility = 'hidden';

        socket.emit('action', 'videoon');
    }
})


audioButt.addEventListener('click', () => {

    if (audioAllowed) {
        for (let key in audioTrackSent) {
            audioTrackSent[key].enabled = false;
        }
        audioButt.innerHTML = `<i class="fas fa-microphone-slash"></i>`;
        audioAllowed = 0;
        audioButt.style.backgroundColor = "#b12c2c";
        if (mystream) {
            mystream.getTracks().forEach(track => {
                if (track.kind === 'audio')
                    track.enabled = false;
            })
        }

        mymuteicon.style.visibility = 'visible';

        socket.emit('action', 'mute');
    } else {
        for (let key in audioTrackSent) {
            audioTrackSent[key].enabled = true;
        }
        audioButt.innerHTML = `<i class="fas fa-microphone"></i>`;
        audioAllowed = 1;
        audioButt.style.backgroundColor = "#4ECCA3";
        if (mystream) {
            mystream.getTracks().forEach(track => {
                if (track.kind === 'audio')
                    track.enabled = true;
            })
        }

        mymuteicon.style.visibility = 'hidden';

        socket.emit('action', 'unmute');
    }
})

socket.on('action', (msg, sid) => {
    if (msg == 'mute') {
        console.log(sid + ' muted themself');
        document.querySelector(`#mute${sid}`).style.visibility = 'visible';
        micInfo[sid] = 'off';
    } else if (msg == 'unmute') {
        console.log(sid + ' unmuted themself');
        document.querySelector(`#mute${sid}`).style.visibility = 'hidden';
        micInfo[sid] = 'on';
    } else if (msg == 'videooff') {
        console.log(sid + 'turned video off');
        document.querySelector(`#vidoff${sid}`).style.visibility = 'visible';
        videoInfo[sid] = 'off';
    } else if (msg == 'videoon') {
        console.log(sid + 'turned video on');
        document.querySelector(`#vidoff${sid}`).style.visibility = 'hidden';
        videoInfo[sid] = 'on';
    }
})
```

> #### 后端

```Javascript
const HTTPS_PORT = 8443;
const PORT = 3000;
const fs = require('fs');

const serverConfig = {
    key: fs.readFileSync('key.pem'),
    cert: fs.readFileSync('cert.pem'),
};

// ----------------------------------------------------------------------------------------
function getTime() {
    const today = new Date();
    let h = today.getHours();
    let m = today.getMinutes();
    let s = today.getSeconds();
    m = checkTime(m);
    s = checkTime(s);
    return {
        h, m, s
    }
}
function checkTime(i) {
    if (i < 10) {
        i = "0" + i
    }; // add zero in front of numbers < 10
    return i;
}
require('dotenv').config();
const bodyParser = require("body-parser");
const express = require('express');
const app = express();
const moment = require('moment');
const https = require('https');
// const httpsServer = https.createServer(serverConfig, handleRequest);
const httpsServer = https.createServer(serverConfig, app);
app.use(bodyParser.urlencoded({
    extended: true
}));
app.use(bodyParser.json());
const { Server } = require('socket.io');
const io = new Server(httpsServer, {
    cors: {
        origin: '*',
        allowedHeaders: ['Content-Type']
    }
});
//io.listen(httpsServer).sockets;
const path = require('path')
const cors = require('cors')
app.use(express.static(path.join(__dirname, '../public')));
//  all variables for users
app.use(cors({
    origin: '*',
    methods: ['GET', 'POST'],
    allowedHeaders: ['Content-Type']
}))

const { getIpAddress } = require('./getIpAddress')

const ip = getIpAddress()


let rooms = {};
let socketRooms = {};
let socketName = {};
let mic = {};
let video = {};
let whiteboard = {};

// ----------------------------------------------------------------------------------------

// Create a server for handling websocket calls
//const io = new WebSocketServer({ server: httpsServer });

io.on('connection', function (socket) {
    // const sockets = io.allSockets();
    // console.log(sockets);
    // const sockets = io.fetchSockets();
    // for (const socket of sockets)
    //   console.log(socket.id);

    socket.on('message', function (message) {
        console.log(message)
        var data = JSON.parse(message);
        io.to(data.roomid).emit('message', message);
        console.log(`${data.username} sent a txt message!`)
    });

    socket.on('error', (err) => {
        console.log(err);
    })

    socket.on('rooms', function (rooms) {
        var count = 0;
        var message = JSON.parse(rooms);
        socket.join(message.rooms);
        console.log(socket.id + '成功加入' + message.rooms);
        io.in(message.rooms).allSockets().then(items => {
            items.forEach(item => {
                count = count + 1;
            })
        });
        console.log(count);
    })

    socket.on("disconnect", async () => {
        const sockets = await io.fetchSockets();
        for (const socket of sockets)
            console.log(socket.id);
    });
    socket.on("sendMsg", function (data) {
        //data 为客户端发送的消息，可以是 字符串，json对象或buffer
        // 使用 emit 发送消息，broadcast 表示 除自己以外的所有已连接的socket客户端。
        console.log(data);
        socket.broadcast.to('rooms').emit('receiveMsg', data);
        io.sockets.emit("receiveMsg", data);
    })

    socket.on("join room", (roomid, username) => {
        socket.join(roomid);
        socketRooms[socket.id] = roomid;
        socketName[socket.id] = username;
        mic[socket.id] = 'on';
        video[socket.id] = 'on';
        if (rooms[roomid] && rooms[roomid].length > 0) {
            rooms[roomid].push(socket.id);
            socket.to(roomid).emit('message', JSON.stringify(
                {
                    msg: `${username} joined the room.`,
                    username: 'Meet-Bot',
                    roomid,
                    time: getTime()
                }
            ));
            io.to(socket.id).emit('join room', rooms[roomid].filter(pid => pid != socket.id), socketName, mic, video);
        } else {
            rooms[roomid] = [socket.id];
            io.to(socket.id).emit('join room', null, null, null, null);
        }
        io.to(roomid).emit('user count', rooms[roomid].length);

    });

    //  video/mic related stuff
    socket.on('action', msg => {
        if (msg == 'mute') {
            mic[socket.id] = 'off';
        }
        else if (msg == 'unmute') {
            mic[socket.id] = 'on';
        }
        else if (msg == 'videoon') {
            video[socket.id] = 'on';
        }
        else if (msg == 'videooff') {
            video[socket.id] = 'off';
        }
        socket.to(socketRooms[socket.id]).emit('action', msg, socket.id);
    });

    socket.on('video-offer', (offer, sid) => {
        socket.to(sid).emit('video-offer', offer, socket.id, socketName[socket.id], mic[socket.id], video[socket.id]);
    });

    socket.on('video-answer', (answer, sid) => {
        socket.to(sid).emit('video-answer', answer, socket.id);
    });

    socket.on('new icecandidate', (candidate, sid) => {
        socket.to(sid).emit('new icecandidate', candidate, socket.id);
    });

    //  Chats message


    //  Whiteboard canvas
    socket.on('getCanvas', () => {
        if (whiteboard[socketRooms[socket.id]])
            socket.emit('getCanvas', whiteboard[socketRooms[socket.id]]);
    });

    socket.on('draw', (newx, newy, prevx, prevy, color, size) => {
        socket.to(socketRooms[socket.id]).emit('draw', newx, newy, prevx, prevy, color, size);
    });

    socket.on('clearBoard', () => {
        socket.to(socketRooms[socket.id]).emit('clearBoard');
    });

    socket.on('store canvas', url => {
        whiteboard[socketRooms[socket.id]] = url;
    });
    socket.on('disconnectr', () => {
        if (!socketRooms[socket.id]) {
            return;
        }
        socket.to(socketRooms[socket.id]).emit('message', JSON.stringify(
            {
                msg: `${socketName[socket.id]} left the chat.`,
                username: `Meet-Bot`,
                roomid: rooms[socket.id],
                time: getTime()
            }
        )
        );
        socket.to(socketRooms[socket.id]).emit('remove peer', socket.id);
        let index = rooms[socketRooms[socket.id]].indexOf(socket.id);
        rooms[socketRooms[socket.id]].splice(index, 1);
        io.to(socketRooms[socket.id]).emit('user count', rooms[socketRooms[socket.id]].length);
        delete socketRooms[socket.id];
        console.log('leaving room.....');
        console.log(rooms[socketRooms[socket.id]]);
    });

});


httpsServer.listen(HTTPS_PORT, ip);
console.log(`Server running. Visit https://${ip}:` + HTTPS_PORT + ' in Firefox/Chrome'
);

```

> ## 成品效果

> ### pc端
![登录界面](/images/Project1/login.jpg)

![界面](/images/Project1/interface.jpg)

![被呼叫](/images/Project1/pc_called.PNG)

> ### 移动端

![登录界面1](/images/Project1/pixel_login.jpg)
![界面1](/images/Project1/pixel_user_interface.png)
![被呼叫1](/images/Project1/pixel_called.jpg)
![通话界面1](/images/Project1/pixel_chatroom.jpg)
