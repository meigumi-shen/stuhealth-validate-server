# stuhealth-validate-server

提供给[自动打卡工具](https://github.com/SO-JNU/stuhealth)使用的，一个比较简单的滑动验证码自动完成 API 服务。使用 Python、Selenium 和 GeckoDriver 实现。

这个项目是一个“最简的可行产品”（Minimum viable product），因此存在一些局限性：

* 只能同时使用一个浏览器进程，因此同时响应多个请求的话需要排队。
* 鉴权机制使用的是简单的固定 token。
* HTTP 服务仅使用 Python 内置的 `BaseHTTPRequestHandler` 和 `ThreadingHTTPServer` 实现，不支持其他高级功能。
    * 如果一定要将 API 服务对公网暴露，建议使用 Nginx 等功能完整的 Web 服务器进行反向代理。

## 使用方式

使用前请安装好 Firefox 和 [GeckoDriver](https://github.com/mozilla/geckodriver)，然后 `pip3 install -r requirements.txt`。

`python3 main.py PORT TOKEN`

* `PORT` 为占用的端口。
* `TOKEN` 为调用 API 所需的 token，对应打卡工具中的 `-vt` 参数。
    * 你可以使用 `python3 -c "print(__import__('secrets').token_urlsafe(24))"` 随机生成一个。

服务启动后将在 `/` 路径响应请求。
