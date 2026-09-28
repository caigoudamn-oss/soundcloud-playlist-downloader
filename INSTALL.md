# 📥 详细安装指南

## 系统要求

- **Python 3.7 或更高版本**
- **FFmpeg**（用于音频转换）
- **网络连接**

---

## Windows 安装步骤

### 1️⃣ 安装 Python

1. 访问 https://www.python.org/downloads/
2. 下载 Python 3.11 (或最新版本)
3. 运行安装程序
4. ✅ **重要**: 勾选 "Add Python to PATH"
5. 点击 "Install Now"

### 2️⃣ 安装 FFmpeg

**方案 A: 使用 Chocolatey (推荐)**
```bash
# 以管理员身份打开 PowerShell，运行：
choco install ffmpeg
```

**方案 B: 手动下载**
1. 访问 https://ffmpeg.org/download.html
2. 下载 Windows 版本的 FFmpeg
3. 解压到 `C:\ffmpeg`
4. 将 `C:\ffmpeg\bin` 添加到系统 PATH

验证安装：
```bash
ffmpeg -version
```

### 3️⃣ 克隆项目

```bash
git clone https://github.com/caigoudamn-oss/soundcloud-playlist-downloader.git
cd soundcloud-playlist-downloader
```

### 4️⃣ 安装 Python 依赖

```bash
pip install -r requirements.txt
pip install yt-dlp
```

### 5️⃣ 开始使用

```bash
python soundcloud_downloader.py "https://soundcloud.com/user/sets/playlist-name"
```

---

## macOS 安装步骤

### 1️⃣ 安装 Homebrew (如果尚未安装)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2️⃣ 安装 Python 和 FFmpeg

```bash
brew install python@3.11
brew install ffmpeg
```

### 3️⃣ 克隆项目

```bash
git clone https://github.com/caigoudamn-oss/soundcloud-playlist-downloader.git
cd soundcloud-playlist-downloader
```

### 4️⃣ 安装依赖

```bash
pip3 install -r requirements.txt
pip3 install yt-dlp
```

### 5️⃣ 开始使用

```bash
python3 soundcloud_downloader.py "https://soundcloud.com/user/sets/playlist-name"
```

或使用 bash 脚本：
```bash
chmod +x download.sh
./download.sh "https://soundcloud.com/user/sets/playlist-name"
```

---

## Linux 安装步骤 (Ubuntu/Debian)

### 1️⃣ 更新系统

```bash
sudo apt update
sudo apt upgrade
```

### 2️⃣ 安装 Python、pip 和 FFmpeg

```bash
sudo apt install python3.11 python3-pip ffmpeg
```

### 3️⃣ 克隆项目

```bash
git clone https://github.com/caigoudamn-oss/soundcloud-playlist-downloader.git
cd soundcloud-playlist-downloader
```

### 4️⃣ 安装依赖

```bash
pip3 install -r requirements.txt
pip3 install yt-dlp
```

### 5️⃣ 开始使用

```bash
python3 soundcloud_downloader.py "https://soundcloud.com/user/sets/playlist-name"
```

或使用 bash 脚本：
```bash
chmod +x download.sh
./download.sh "https://soundcloud.com/user/sets/playlist-name"
```

---

## Docker 安装 (可选)

如果安装依赖困难，可以使用 Docker：

### 创建 Dockerfile

在项目根目录创建 `Dockerfile`：

```dockerfile
FROM python:3.11-slim

RUN apt-get update && apt-get install -y \
    ffmpeg \
    git \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt && pip install yt-dlp

COPY soundcloud_downloader.py .

ENTRYPOINT ["python", "soundcloud_downloader.py"]
```

### 构建和运行

```bash
# 构建 Docker 镜像
docker build -t soundcloud-downloader .

# 运行容器
docker run -v $(pwd)/downloads:/app/downloads soundcloud-downloader "https://soundcloud.com/user/sets/playlist-name"
```

---

## 验证安装

检查所有组件是否正确安装：

```bash
# 检查 Python
python --version
# 或
python3 --version

# 检查 FFmpeg
ffmpeg -version

# 检查 Python 包
pip list | grep yt-dlp
```

输出示例：
```
Python 3.11.0
ffmpeg version 5.1.2
yt-dlp                2.14.4
```

---

## 常见安装问题

### ❌ "Python not found" 或 "python: command not found"

**解决方案**：
- Windows: 重新安装 Python，勾选 "Add Python to PATH"
- macOS/Linux: 使用 `python3` 替代 `python`

### ❌ "FFmpeg not found"

**解决方案**：
- 重新安装 FFmpeg
- 验证 FFmpeg 在系统 PATH 中

### ❌ "ModuleNotFoundError: No module named 'yt_dlp'"

**解决方案**：
```bash
pip install --upgrade yt-dlp
```

### ❌ "Permission denied" (Linux/macOS)

**解决方案**：
```bash
chmod +x soundcloud_downloader.py
chmod +x download.sh
```

### ❌ SSL 证书错误

**解决方案**：
```bash
pip install --upgrade certifi
```

---

## 升级到最新版本

```bash
cd soundcloud-playlist-downloader
git pull origin main

pip install -r requirements.txt --upgrade
pip install yt-dlp --upgrade
```

---

## 卸载

### 移除项目文件

```bash
rm -rf soundcloud-playlist-downloader
```

### 移除 Python 包 (可选)

```bash
pip uninstall yt-dlp requests beautifulsoup4
```

---

需要帮助？访问 [GitHub Issues](https://github.com/caigoudamn-oss/soundcloud-playlist-downloader/issues)
