# Yande-Download (yande.re)
本项目是图片爬虫项目，对[cloudwindy/yander](https://github.com/cloudwindy/yander)的项目进行二次开发。可以从如 https://yande.re 之类的以 danbooru 为基础的网站上爬取图片（可以爬R18）。为了得到最佳的速率，建议使用离目标网站同一国家甚至同一机房的服务器。（要爬yandere的话建议使用日本主机）
# Yander 爬虫工具
## Windows 安装指南
0. 如果你已经安装 Python 3，跳转到第 4 步。
1. 前往最新的 Python 3 版本发布页面（一键传送👉https://www.python.org/downloads/）
2. 选择适合你 Windows 版本的 Python（你也可以直接点黄色的 Download Python 按钮）
3. 下载 Python 安装包
4. Git 克隆本项目（点绿色的写着 Code 的按钮然后点 Download ZIP 然后解压）
5. 按需求配置 config.json
6. 双击 main.py 运行 或者在控制台窗口输入 python3 main.py 然后回车

## Linux 安装指南
### Ubuntu / Debian-based 操作系统
```
sudo apt-get update
sudo apt-get install -y python3 git
git clone https://github.com/bcYwpK3/Yande-Download
cd Yande-Download
```

### CentOS / RedHat-based 操作系统
```
sudo yum install -y python3 git
git clone https://github.com/bcYwpK3/Yande-Download
cd Yande-Download
```

## 配置文件详解
|         参数         | 类型 |     解释      |     默认     |
| -------------------- | ---- | ------------- | ------------ |
| start                | 必选 | 起始页码      |              |
| end                  | 必选 | 结束页码      |              |
| save_dir             | 必选 | 保存路径      |              |
| thread_num           | 可选 | 线程数        | 单线程       |
| log                  | 可选 | 日志位置      | 不记录日志   |
| log_autopurge        | 可选 | 自动清空日志  | 不清空日志   |
| tags                 | 可选 | 标签          | 处理全部图片 |
| except_tags          | 可选 | 排除标签      | 不排除图片   |
| no_check_certificate | 可选 | 不检查SSL证书 | 检查SSL证书  |
| proxy                | 可选 | 使用代理      | 不使用代理   |
| proxy_addr           | 可选 | 代理地址      | 不使用代理   |

# 配置文件详解

## 术语解释

程序：指的是本项目的主程序 main.py。

模块：配置文件中的对象，比如说```"log":{"enabled": true}```，那么log就是一个模块，enabled决定这个模块是启用还是禁用的状态。（enabled是所有可禁用模块必须的参数）对于不可禁用的模块例如```"pages":{"mode":"infinite"}```，mode决定这个模块的运行状态（mode是所有不可禁用模块必须的参数）。

参数：配置文件中对象下的属性，比如说```"log":{"path":"./save"}```，那么path就是一个参数，这个参数决定了log模块是如何工作的。

标志：main.py 中的一些不属于配置文件的一部分配置，用于调试。这些标志中有的将来可能会移动到配置文件中，有的会被写死（hardcode）。标志可以在 main.py 源代码中找到，通常自带注释。

页面：由于 yande.re API 限制，一个页面是100张图片。

目标页面：要处理的页面，因为本程序除了下载以外还可以更改、校验、共享（正在开发）已下载的图集，因此不能称为“要下载的页面”。如果你只用这个程序来下载，那么当然可以理解为“要下载的页面”。

处理：下载、更改、校验。主要是下载。

## config.json文件

~~~json
{
	"start": 1,		起始页码
	"end": 1,		终止页码
	"log": "yander.log",		日志文件名
	"log_autopurge": false,		是否开启日志
	"tags": "rating:safe",		指定图片标签，可为空。多个标签用+连接
	"except_tags": "possible_duplicate",	指定图片排除标签，可为空。多个标签用+-连接
	"thread_num": 5,		最大线程数，建议5
	"save_dir": "E:\\yander-main\\pic",		图片保存路径，windows下使用\\双斜线
	"proxy": false,		是否使用代理
	"proxy_addr": "127.0.0.1:8118"		输入HTTP代理地址ipaddr:prot
}
~~~

# 运行示例

windows下使用：python .\main.py

linux下使用：python ./main.py

~~~bash
> python.exe .\main.py
[+] UI模块: UI模块已成功初始化
[*] 初始化: Yande.re 下载工具
[!] 初始化: 程序将仅处理第 1 页
[.] 页面 1: 正在获取元数据
[+] 页面 1: 已获取元数据
[.] 页面 1: 正在移除重复图片...
[.] 页面 1: 正在进行大小排序...
[+] 页面 1: 共 100 张图片
[*] 页面 1: 下载开始
图片1111531:   1%|▋                              | 950k/87.5M [00:02<53:32, 8kB/s]
图片1111515:   9%|█████▊                         | 2.59M/28.4M [00:02<60:14, 5kB/s]
图片1111226:  15%|█████████▊                     | 1.64M/10.8M [00:02<60:12, 7kB/s]
图片1111005:  13%|████████▌                       | 1.80M/13.7M [00:02<60:13, 2kB/s]
图片1111090:  11%|███████                         | 1.74M/16.0M [00:02<60:15, 2kB/s]
[+] 页面 1: 下载完毕
[*] 主程序: 正在等待任务结束
[+] UI模块: UI模块已退出

[*] 主程序: 下载工具已退出

[+] UI模块: UI模块已退出
~~~

