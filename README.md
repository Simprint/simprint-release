# Simprint Release

本仓库用于存放 **Simprint（Tauri Windows）** 的发布产物（Release artifacts），以便在主代码仓库为私有仓库的情况下，仍可通过公开仓库分发安装包与更新元数据。

## 内容说明

- **Windows 安装包（NSIS）**：例如 `Simprint_<version>_x64-setup.exe`
- **更新元数据**：`latest.json`（供客户端/更新器读取）

> 说明：本仓库不存放源代码，仅存放编译产物与更新所需文件。

## 推荐目录结构

```
/
├── latest.json
└── windows/
    └── v0.1.0/
        ├── Simprint_0.1.0_x64-setup.exe
        └── Simprint_0.1.0_x64-setup.exe.sig  (可选：若启用签名)
```

## 发布流程（从主仓库产物同步到本仓库）

1. 在主仓库（`Simprint/simprint`）完成构建并生成 `latest.json`
   - 构建前端：`node build.cjs`
   - 打包（Windows）：`cargo tauri build`
   - 生成 `latest.json`：`node deploy/generate-latest-json.mjs`

2. 将生成的产物复制/同步到本仓库目录并提交
   - `latest.json`
   - `src-tauri/target/release/bundle/nsis/*.exe`（以及可选的 `.sig`）

3. 推送到本仓库 `main` 分支

## 注意事项

- `latest.json` 中的下载 URL 通常指向本仓库的文件托管位置（或 GitHub Releases 的下载地址）。
- 若你启用了签名（`.sig` / `signature` 字段），请确保发布流程同时同步签名文件。

