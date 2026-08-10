# 第三方组件授权声明

本文件列出 SFM 依赖的第三方组件及其许可证。随发行版分发时须一并附带
对应许可证全文（LGPL 组件另见 §合规）。

## 引擎（engine/，运行时依赖）

| 组件 | 许可证 | 用途 |
|---|---|---|
| [blake3](https://github.com/oconnor663/blake3-py) | CC0-1.0 / Apache-2.0（双许可） | 强哈希（可选；缺失时回退 b3sum 子进程或 hashlib.sha256） |

引擎其余部分仅用 Python 标准库（sqlite3 / hashlib / ctypes / concurrent.futures 等）。

## 应用（app/，M0b 起引入——待补全）

以下为规划中的应用层依赖，将在对应里程碑落地时补入本表并附许可证：

| 组件 | 许可证 | 备注 |
|---|---|---|
| PySide6 | LGPL-3.0 | Qt 官方绑定；**LGPL 合规**：onedir 打包保持 Qt 动态库可替换、随包附 LGPLv3 全文与 Qt 模块清单、禁用 GPL-only Qt 模块（QtCharts/QtDataVisualization/QtVirtualKeyboard 等）。见 TECH_GUIDE KD-01。 |
| pywin32 | PSF | Shell 集成（IFileOperation 等） |
| [xlrd](https://github.com/python-excel/xlrd) | BSD-3-Clause | .xls（Excel 97-2003）预览文本抽取 |
| [olefile](https://github.com/decalage2/olefile) | BSD-2-Clause | .doc/.ppt（Office 97-2003）OLE 容器流读取（正文解析为按 [MS-DOC]/[MS-PPT] 公开规范自研） |
| comtypes | MIT | IShellItemImageFactory 等自定义 COM 接口 |
| [pypdf](https://github.com/py-pdf/pypdf) | BSD-3-Clause | PDF AES-256 打开口令（文件加密） |
| [msoffcrypto-tool](https://github.com/nolze/msoffcrypto-tool) | MIT | Office OOXML ECMA-376 agile 加密 |
| [cryptography](https://github.com/pyca/cryptography) | Apache-2.0 OR BSD-3-Clause | 加密后端 + 密码库 KDF（scrypt/AES-GCM） |
| [markdown-it-py](https://github.com/executablebooks/markdown-it-py) | MIT | Markdown 解析（CommonMark+GFM，预览完美渲染） |
| [mdit-py-plugins](https://github.com/executablebooks/mdit-py-plugins) | MIT | GFM/dollarmath/front-matter 插件 |
| [linkify-it-py](https://github.com/tsutsu3/linkify-it-py) | MIT | 自动链接（依赖 uc-micro-py，MIT） |
| [Pygments](https://pygments.org/) | BSD-2-Clause | 代码块语法高亮（noclasses 内联样式） |

## 随包 JS 资产（app/sfm_app/assets/js/，在 QJSEngine 内运行、不联网）

由 `scripts/build_js_bundles.py` 固定版本自 npm 构建（esbuild MIT，仅构建期、不随包分发）：

| 资产 | 上游 | 许可证 |
|---|---|---|
| mathjax.bundle.js | [MathJax / mathjax-full 3.2.2](https://github.com/mathjax/MathJax-src) | Apache-2.0 |
| nomnoml.bundle.js | [nomnoml 1.7.0](https://github.com/skanaar/nomnoml) 及其依赖 [graphre](https://github.com/skanaar/graphre) | MIT / MIT |

## 合规红线（摘自 TECH_GUIDE §8）

- 不复制/翻译任何 GPL/AGPL 代码（Double Commander、Explorer++、Sigma、orange、Xplorer——仅可 clean-room 借鉴思路）。
- Everything 仅经 SDK/IPC 调用（聚合非衍生）；若捆绑分发限 1.4.x（其 License.txt 为 MIT 式授权，官方允许捆绑）。
- Pro 闭源模块不得包含任何 copyleft 依赖。
