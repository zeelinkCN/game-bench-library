# GameBench Library（游戏市场资源库）

《拾光游戏厅》的公开游戏市场资源仓库。Mac / tvOS 客户端通过 HTTPS 读取目录，
按单款或合集安装资源。

目录元数据、市场清单、文档和仓库组织方式采用 MIT License。`owned/`、`covers/`
和 `legacy-images/` 中的资源不因本仓库的 MIT License 被重新授权，仍以来源记录
及其原有权利为准。
详细范围见 [LICENSE_SCOPE.md](LICENSE_SCOPE.md)。

## 目录

- `catalog.json`：应用读取的完整游戏目录、SHA-256、封面和精选排序。
- `store.json`：线上市场入口和各系列合集；客户端按单款或整套安装。
- `sources.json`：两个原始备份仓库的提交与跨仓库去重统计。
- `owned/`：按 SHA-256 命名的唯一 ROM，共 1131 款。
- `covers/`：从实际 ROM 自动验证并抓取的封面，以及本地标题卡。
- `legacy-images/`：旧仓库保留的 1162 组编号封面/截图，共 2324 张。
- `legacy-cover-index.json`：从旧在线站点恢复的编号、游戏名、发行信息映射。

## 添加新游戏

1. 将得到授权的 ROM 放进来源目录。
2. 在平台源码仓库运行 `scripts/import_owned_repositories.py` 更新目录并按内容去重。
3. 运行 `scripts/generate_covers.py` 为新增 ROM 抓取经过核心验证的画面。
4. 检查 `catalog.json` 中的标题、语言标记、系列和精选顺序。
5. 只提交本资源仓库；平台代码没有变化时无需重新提交源码仓库。

构建时将本仓库与 `game-bench-macos` 放在相邻目录，或设置：

```sh
export GAMEBENCH_LIBRARY_DIR=/absolute/path/to/GameBench-Library
```

## 当前验证

- 1324 个输入路径去除 193 个内容重复项，得到 1131 款唯一游戏。
- 1118 款在自动启动测试中输出有效画面。
- 13 款保留并在目录中标注兼容性待验证。
- 1131 款均有封面；版本不完全匹配的旧封面会单独标注匹配方式。
