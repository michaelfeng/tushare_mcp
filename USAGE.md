# Tushare MCP Server 使用指南

## ✅ **服务器已成功创建并运行！**

### 📁 **项目文件**

```
tushare_mcp/
├── server_simple.py       # ✅ 工作正常的 MCP 服务器
├── server.py              # 📋 完整版本（有兼容性问题）
├── requirements.txt       # 📦 依赖包列表
├── mcp_config.json        # ⚙️ MCP 客户端配置
├── test_simple.py         # 🧪 测试脚本
├── README.md              # 📖 详细文档
└── USAGE.md              # 📝 使用指南（本文件）
```

### 🚀 **快速启动**

#### **1. 安装依赖**
```bash
cd tushare_mcp
pip3 install -r requirements.txt
```

#### **2. 设置 Tushare Token（可选）**
```bash
export TUSHARE_TOKEN=your_token_here
```

#### **3. 启动服务器**
```bash
python3 server.py
```

### 🛠️ **可用工具**

#### **1. get_stock_basic**
获取股票基本信息列表
```json
{
  "name": "get_stock_basic",
  "arguments": {
    "exchange": ""  // 可选：SSE, SZSE 或空字符串
  }
}
```

#### **2. search_stocks** 
搜索股票
```json
{
  "name": "search_stocks", 
  "arguments": {
    "keyword": "茅台"  // 必需：搜索关键词
  }
}
```

### 🎯 **在 MCP 客户端中使用**

#### **Claude Desktop 配置**
将以下内容添加到您的 Claude Desktop 配置文件中：

```json
{
  "mcpServers": {
    "tushare": {
      "command": "python3",
      "args": ["server.py"],
      "cwd": "/path/to/your/tushare_mcp",
      "env": {
        "TUSHARE_TOKEN": "your_token_here"
      }
    }
  }
}
```

#### **使用示例**

1. **搜索股票**：
   ```
   请帮我搜索包含"银行"的股票
   ```

2. **获取股票列表**：
   ```
   请获取深交所的股票基本信息
   ```

### ⚠️ **重要说明**

1. **Token 设置**：
   - 未设置 Token：使用免费接口（功能受限）
   - 已设置 Token：使用 Pro 接口（完整功能）

2. **网络要求**：
   - 需要访问 Tushare API
   - 免费版本可能有网络限制

3. **兼容性**：
   - `server_simple.py`：简化版，兼容性好 ✅
   - `server.py`：完整版，可能有兼容性问题 ⚠️

### 🎉 **成功标志**

当您看到以下输出时，表示服务器启动成功：

```bash
$ python3 server.py
⚠️  未设置 Tushare Token，将使用免费接口（功能受限）
# 服务器开始等待 MCP 客户端连接...
```

### 🔧 **故障排除**

1. **依赖问题**：
   ```bash
   pip3 install -r requirements.txt
   ```

2. **权限问题**：
   ```bash
   chmod +x server_simple.py
   ```

3. **Token 问题**：
   - 访问 https://tushare.pro/ 注册
   - 获取 API Token
   - 设置环境变量

### 📞 **联系支持**

如有问题，请检查：
- Python 版本（推荐 3.8+）
- 依赖包安装
- 网络连接
- Tushare Token 设置

**🎊 您的 Tushare MCP 服务器已准备就绪！**
