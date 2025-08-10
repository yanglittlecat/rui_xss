<h1 align="center">✨ Rui_XSS ✨</h1>
<p align="center">
  <b>基于 Burp Suite 的被动式 XSS 漏洞检测插件</b><br>
  🔍 自动检测隐藏表单参数 & JavaScript 参数的潜在跨站脚本漏洞 🔍
</p>

---

## 📌 项目简介

Rui_XSS 是一个为 **Burp Suite** 编写的被动式 XSS 漏洞检测插件，  
灵感与技术参考来源于 **xscan** 和 **xiasql** 项目，并在此基础上进行了功能优化与扩展。  

---

## 🚀 功能特点

- 🕵 **被动扫描**：无需主动发起扫描，自动监控 Burp Proxy / Repeater 流量  
- 🗂 **检测参数类型**：
  - 普通参数（URL / POST 表单）
  - 隐藏表单参数（`<input type="hidden">`）
  - JavaScript 参数（`<script>` 标签、HTML 事件属性）
- 🎯 **多编码 Payload 测试**：
  - 原始
  - HTML 实体编码
  - URL 编码
  - 双重 URL 编码
- 🪞 **反射检测**：识别 Payload 是否在响应中被反射
- 🔄 **递归挖掘**：支持多轮参数递归请求（默认深度 3）
- 📜 **白名单模式**：仅扫描指定域名
- 💻 **可视化 UI**：Burp Suite 标签页集中控制

---

## 📷 插件截图

<p align="center">
  <img src="https://github.com/yanglittlecat/rui_xss/blob/main/demo.png" alt="插件界面示例" width="80%">
</p>

---

## 📥 安装方法

1. **安装 Jython**  
   下载：[https://www.jython.org/download](https://www.jython.org/download)  
   在 Burp Suite → `Extender → Options → Python Environment` 配置 `jython.jar`

2. **加载插件**  
   - 打开 `Extender → Extensions`
   - 点击 **Add**
   - 选择 **Extension type** 为 `Python`
   - 选择 `rui_xss.py`
   - 点击 **Next**，加载成功后会出现 **Rui_XSS** 标签页

---

## 🎮 使用说明

- **启用/禁用扫描**（Enable scanning）
- **检测隐藏表单参数**（Test hidden form parameters）
- **检测 JavaScript 参数**（Test script parameters）
- **选择监控范围**（Monitor Proxy / Monitor Repeater）
- **递归深度**（Max recursion depth）
- **白名单域名**（Whitelist domains）

扫描结果会显示在插件的表格中，包括：
- 请求时间
- URL
- 参数类型
- 编码方式
- Payload
- 是否发现反射

### 发现反射点后的使用方法

当插件检测到反射（payload 反射出现在响应包中）时，工具会在返回包中标记包含测试字符串 `rui` 的位置。  
用户需要自行查看响应内容，搜索关键字 `rui`，并结合页面上下文进行分析，判断是否存在实际的 XSS 触发风险。  
本工具提供反射检测的辅助，最终判定仍需人工确认。
---

## ⚙ 技术原理

1. 拦截并解析 HTTP 响应
2. 提取 HTML 和 JavaScript 中的参数
3. 用多种编码方式注入 Payload
4. 检测响应是否反射 Payload
5. 支持递归挖掘更多隐藏参数

---

## ⚠ 注意事项

- 请仅在 **授权的目标** 上进行安全测试
- 会自动跳过大文件（图片、CSS、JS、PDF 等）
- 避免在生产环境中使用高递归深度，以防增加服务器压力

---

## 📄 许可证

MIT License © 2025 yanglittlecat