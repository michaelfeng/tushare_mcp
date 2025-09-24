# Tushare MCP 服务器

[English](./README.md) | [中文](./README_zh.md)

[![PyPI version](https://badge.fury.io/py/tushare-mcp-server.svg)](https://badge.fury.io/py/tushare-mcp-server)

本项目是一个基于 [Tushare](https://tushare.pro/) 数据接口的模型上下文协议 (MCP) 服务器，为 AI 助手提供丰富、全面的中国内地金融市场数据。

## 🌟 功能特性

- **安装简便**: 已打包并发布到 PyPI，可通过一条 `pip` 命令轻松安装。
- **运行简单**: 提供 `tushare-mcp` 命令行工具，一键启动服务。
- **丰富数据**: 封装了海量 Tushare Pro API，覆盖股票、指数、基金、债券、宏观经济等。
- **高性能**: 采用异步处理，支持高效并发查询。
- **高安全性**: 通过环境变量安全地处理 API 令牌。

## 📦 安装指南

本项目已发布到 PyPI，您可以使用 `pip` 来安装。

```bash
# 从 PyPI 安装
pip install tushare-mcp-server
```

要升级到最新版本：
```bash
pip install --upgrade tushare-mcp-server
```

## ⚙️ 配置说明

为了使用本服务的完整功能，您需要一个 Tushare API 令牌。您可以访问 [Tushare Pro 官网](https://tushare.pro/) 注册账户以获取免费令牌。

服务器会从名为 `TUSHARE_TOKEN` 的环境变量中自动读取您的令牌。当您通过 `pip` 安装后，这是唯一支持的配置方式。

-   **在 macOS/Linux 系统中:**
    ```bash
    export TUSHARE_TOKEN="your_tushare_token_here"
    ```
    为了使此设置永久生效，您可以将这行命令添加到您 shell 的配置文件中 (例如 `~/.bash_profile` 或 `~/.zshrc`)。

-   **在 Windows 系统中:**
    ```bash
    set TUSHARE_TOKEN="your_tushare_token_here"
    ```
    要永久设置，您可以使用“系统属性”面板中的“环境变量”功能。

## ▶️ 如何使用

当您安装好包并设置了 `TUSHARE_TOKEN` 环境变量后，只需一个命令即可启动服务器：

```bash
tushare-mcp
```

成功启动后，您会看到 `✅ Tushare Token has been set.` 的提示信息。

此时，服务器已在运行并等待来自 MCP 客户端的连接。

### 配置您的 Agent

要让您的本地 Agent (例如 Claude Desktop) 使用此服务，您需要为其指定一个配置文件。文件内容如下：

```json
{
  "mcpServers": {
    "tushare": {
      "command": "tushare-mcp",
      "args": [],
      "env": {
        "TUSHARE_TOKEN": "YOUR_TUSHARE_TOKEN_HERE"
      }
    }
  }
}
```

## 🛠️ 可用工具

该服务器提供了一套全面的工具集，用于访问金融数据。以下是部分工具类别：

-   **基础股票数据**: `get_stock_basic`, `get_daily_data`, `get_weekly_data`, `get_monthly_data` 等。
-   **市场参考数据**: `get_top_list`, `get_money_flow`, `get_margin_detail`, `get_block_trade`。
-   **财务数据**: `get_financial_data`, `get_balance_sheet`, `get_cash_flow`, `get_fina_indicator`。
-   **指数数据**: `get_index_data`, `get_index_basic`, `get_index_weight`。
-   **ETF与基金数据**: `get_etf_basic`, `get_etf_daily`, `get_fund_daily`, `get_fund_portfolio`。
-   **债券数据**: `get_bond_basic`, `get_bond_daily`, `get_cb_basic`, `get_cb_daily`。
-   **宏观经济数据**: `get_gdp_data`, `get_cpi_data`, `get_interest_rate`, `get_exchange_rate`。

关于完整的工具列表及其参数，请参考 `server.py` 的源代码。

## 💻 参与开发

如果您希望为本项目贡献代码，或在本地测试修改，可以不通过 `pip` 安装，而是直接从源码运行。

1.  克隆代码仓库:
    ```bash
    git clone https://github.com/michaelfeng/tushare_mcp.git
    cd tushare_mcp
    ```

2.  安装依赖:
    ```bash
    pip install -r requirements.txt
    ```

3.  设置 `TUSHARE_TOKEN` 环境变量，方法见“配置说明”部分。

4.  运行服务器脚本:
    ```bash
    python server.py
    ```

## 📄 开源协议

本项目采用 [GPL v3.0 许可证](./LICENSE) 开源。