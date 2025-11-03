# GitHub Pages 静态页面访问规则与路径配置指南

## 📋 目录
- [基本访问规则](#基本访问规则)
- [目录结构与访问路径](#目录结构与访问路径)
- [相对路径配置规则](#相对路径配置规则)
- [链接配置示例](#链接配置示例)
- [本项目路径配置](#本项目路径配置)
- [常见问题与解决方案](#常见问题与解决方案)
- [最佳实践](#最佳实践)

---

## 🌐 基本访问规则

### GitHub Pages 默认行为
1. **默认首页**：`index.html` 是每个目录的默认首页文件
2. **目录访问**：访问 `about/` 会自动寻找 `about/index.html`
3. **文件访问**：直接访问 `.html` 文件需要完整文件名
4. **大小写敏感**：GitHub Pages 对文件名大小写敏感

### URL 结构
```
https://用户名.github.io/仓库名/路径
```

---

## 📁 目录结构与访问路径

### 当前项目结构
```
d:\github\sunnicholas\
├── index.html              # 主页
├── README.md               # 项目说明
├── docs\                   # 项目文档
│   └── github-pages-路径规则.md
└── about\                  # 关于页面目录
    ├── index.html          # 关于首页
    └── experience.html     # 工作经历页面
```

### 对应的访问路径

| 文件路径 | 本地测试访问 | GitHub Pages 访问 |
|---------|-------------|------------------|
| `index.html` | `http://localhost:8000/` | `https://用户名.github.io/仓库名/` |
| `about/index.html` | `http://localhost:8000/about/` | `https://用户名.github.io/仓库名/about/` |
| `about/experience.html` | `http://localhost:8000/about/experience.html` | `https://用户名.github.io/仓库名/about/experience.html` |

---

## 🔗 相对路径配置规则

### 路径符号说明
- `./` - 当前目录
- `../` - 上级目录
- `文件名.html` - 同目录下的文件
- `目录名/` - 子目录（自动寻找 index.html）

### 路径配置原则
1. **使用相对路径**：避免硬编码域名
2. **省略 index.html**：目录访问自动寻找
3. **保持一致性**：统一使用相对路径规则
4. **考虑层级关系**：根据文件位置确定相对路径

---

## 💡 链接配置示例

### 1. 从主页链接到子页面
```html
<!-- 主页 index.html 中 -->
<a href="about/">关于我</a>                    <!-- 链接到 about/index.html -->
<a href="about/experience.html">工作经历</a>    <!-- 链接到 about/experience.html -->
```

### 2. 在 about 目录内的页面间跳转
```html
<!-- about/index.html 中 -->
<a href="experience.html">工作经历</a>          <!-- 同目录下的页面 -->
<a href="./">关于我首页</a>                    <!-- 当前目录的 index.html -->

<!-- about/experience.html 中 -->
<a href="./">返回关于我</a>                    <!-- 返回 about/index.html -->
<a href="../">返回主页</a>                     <!-- 返回主页 index.html -->
```

### 3. 锚点链接配置
```html
<!-- 跳转到主页的特定部分 -->
<a href="../#services">服务</a>                <!-- 主页的 services 部分 -->
<a href="../#contact">联系</a>                 <!-- 主页的 contact 部分 -->
```

---

## 🎯 本项目路径配置

### 导航栏配置

#### 主页导航 (index.html)
```html
<nav>
    <ul>
        <li><a href="#home">首页</a></li>
        <li><a href="about/">关于我</a></li>
        <li><a href="#services">服务</a></li>
        <li><a href="#contact">联系</a></li>
    </ul>
</nav>
```

#### About 页面导航 (about/index.html)
```html
<nav>
    <ul>
        <li><a href="../">首页</a></li>
        <li><a href="./" style="color: #667eea;">关于</a></li>
        <li><a href="experience.html">工作经历</a></li>
        <li><a href="../#services">服务</a></li>
        <li><a href="../#contact">联系</a></li>
    </ul>
</nav>
```

#### 工作经历页面导航 (about/experience.html)
```html
<nav>
    <ul>
        <li><a href="../">首页</a></li>
        <li><a href="./">关于我</a></li>
        <li><a href="experience.html" style="color: #ffd700;">工作经历</a></li>
        <li><a href="../#services">服务</a></li>
        <li><a href="../#contact">联系</a></li>
    </ul>
</nav>
```

---

## ❓ 常见问题与解决方案

### 问题 1：页面跳转 404 错误
**原因**：路径配置错误或文件不存在
**解决方案**：
- 检查文件路径是否正确
- 确认文件名大小写
- 使用相对路径而非绝对路径

### 问题 2：本地测试正常，GitHub Pages 访问异常
**原因**：路径配置不符合 GitHub Pages 规则
**解决方案**：
- 使用 `about/` 而不是 `about/index.html`
- 使用 `../` 而不是 `../index.html`
- 确保所有链接使用相对路径

### 问题 3：CSS 或 JS 文件加载失败
**原因**：静态资源路径配置错误
**解决方案**：
- 使用相对路径引用资源
- 将资源文件放在合适的目录结构中
- 检查文件路径的层级关系

### 问题 4：锚点链接无法正常工作
**原因**：跨页面锚点链接配置错误
**解决方案**：
- 使用 `../#section` 格式
- 确保目标页面存在对应的锚点元素
- 添加平滑滚动 JavaScript 代码

---

## ✅ 最佳实践

### 1. 目录结构规划
```
项目根目录/
├── index.html          # 主页
├── assets/             # 静态资源
│   ├── css/
│   ├── js/
│   └── images/
├── docs/               # 项目文档
├── about/              # 关于页面
├── blog/               # 博客页面
└── contact/            # 联系页面
```

### 2. 命名规范
- 使用小写字母和连字符
- 避免空格和特殊字符
- 保持文件名简洁明了
- 使用有意义的目录名

### 3. 路径配置检查清单
- [ ] 所有链接使用相对路径
- [ ] 目录访问省略 `index.html`
- [ ] 锚点链接格式正确
- [ ] 本地测试所有链接正常
- [ ] 考虑移动端响应式设计

### 4. 维护建议
- 定期检查链接有效性
- 保持文档更新
- 使用版本控制跟踪变更
- 建立测试流程

---

## 📝 更新日志

### 2024-11-03
- 创建初始版本的路径规则文档
- 添加基本访问规则和配置示例
- 完善常见问题解决方案

---

## 📞 联系信息

如有问题或建议，请通过以下方式联系：
- GitHub Issues
- 项目维护者邮箱

---

*本文档将根据项目发展持续更新，请定期查看最新版本。*