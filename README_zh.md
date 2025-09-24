# Tushare MCP 服务器

[English](./README.md) | [中文](./README_zh.md)

本项目是一个基于 [Tushare](https://tushare.pro/) 数据接口的模型上下文协议 (MCP) 服务器，为 AI 助手提供丰富、全面的中国内地金融市场数据。

## 🌟 功能特性

- **股票数据**: 提供股票基本信息、日线/周线/月线行情及历史数据。
- **市场数据**: 包含龙虎榜、融资融券、大宗交易、资金流向等数据。
- **财务数据**: 获取上市公司的财务报表和关键财务指标。
- **指数数据**: 获取主要市场指数的行情和历史数据。
- **基金与ETF**: 提供 ETF 行情、基金净值、持仓、评级等信息。
- **债券数据**: 提供债券和可转债的基本信息及行情数据。
- **宏观经济**: 提供 GDP、CPI、利率、汇率、PMI、货币供应量等数据。
- **智能搜索**: 支持按名称或代码搜索股票。
- **高性能**: 采用异步处理，支持高效查询。

## 📦 安装指南

1.  克隆代码仓库：
    ```bash
    git clone https://github.com/your-username/tushare_mcp.git
    cd tushare_mcp
    ```

2.  安装所需依赖：
    ```bash
    pip install -r requirements.txt
    ```

## ⚙️ 配置说明

为了使用此服务器，您需要一个 Tushare API 令牌。您可以通过在 [Tushare Pro 官网](https://tushare.pro/) 注册来获取免费令牌。

您可以通过以下两种方式配置您的令牌：

#### 方法一：环境变量 (推荐)

这是最安全、最灵活的方法。服务器会优先从名为 `TUSHARE_TOKEN` 的环境变量中自动读取令牌。

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

#### 方法二：配置文件 (用于 MCP 客户端)

如果您使用的 MCP 客户端能为您启动服务器 (例如 Claude Desktop)，您应该使用 `mcp_config.json` 文件进行配置。

1.  **创建配置文件**：通过复制模板文件来创建您的配置文件：
    ```bash
    cp mcp_config.json.template mcp_config.json
    ```

2.  **编辑 `mcp_config.json`**：
    打开该文件并替换其中的占位符。
    -   `cwd`: 将此设置为 `tushare_mcp` 项目目录的**绝对路径**。
    -   `TUSHARE_TOKEN`: 在此处粘贴您的 Tushare 令牌。

    **`mcp_config.json` 示例:**
    ```json
    {
      "mcpServers": {
        "tushare": {
          "command": "python",
          "args": ["server.py"],
          "cwd": "/path/to/your/tushare_mcp",
          "env": {
            "TUSHARE_TOKEN": "YOUR_TUSHARE_TOKEN_HERE"
          }
        }
      }
    }
    ```

> **注意**: 如果未通过任何一种方式设置 `TUSHARE_TOKEN`，服务器将回退使用 Tushare 的免费接口，该接口在数据访问方面有较大限制。

## ▶️ 如何使用

主要有两种方式来运行此服务器：

#### 1. 独立模式

您可以直接从终端运行服务器。这种方式对于测试或连接到正在运行的进程的客户端非常有用。

1.  **设置您的 API 令牌**：使用上文描述的环境变量方法。
2.  **启动服务器**：
    ```bash
    python server.py
    ```
3.  **验证**: 成功启动后，您将看到以下消息之一：
    -   `✅ Tushare Token has been set.` (如果您配置了令牌)
    -   `⚠️ Tushare Token is not set, using free interface (limited functionality).` (如果未找到令牌)
    
    现在，服务器已在运行并等待客户端连接。

#### 2. 与 MCP 客户端一起使用 (例如 Claude Desktop)

大多数 MCP 客户端会为您管理服务器进程。

1.  **配置 `mcp_config.json`**：按照配置部分的说明，确保 `cwd` 和 `TUSHARE_TOKEN` 都已正确设置。
2.  **将您的客户端指向** 此 `mcp_config.json` 文件。
3.  **客户端将自动启动**：当您与其中一个工具交互时，客户端会自动启动 `server.py` 进程。您无需手动运行 `python server.py`。

## 🛠️ 可用工具

该服务器提供了一套全面的工具集，用于访问金融数据。以下是部分工具类别：

-   **基础股票数据**: `get_stock_basic`, `get_daily_data`, `get_weekly_data`, `get_monthly_data` 等。
-   **市场参考数据**: `get_top_list`, `get_money_flow`, `get_margin_detail`, `get_block_trade`。
-   **财务数据**: `get_financial_data`, `get_balance_sheet`, `get_cash_flow`, `get_fina_indicator`。
-   **指数数据**: `get_index_data`, `get_index_basic`, `get_index_weight`。
-   **ETF与基金数据**: `get_etf_basic`, `get_etf_daily`, `get_fund_daily`, `get_fund_portfolio`。
-   **债券数据**: `get_bond_basic`, `get_bond_daily`, `get_cb_basic`, `get_cb_daily`。
-   **宏观经济数据**: `get_gdp_data`, `get_cpi_data`, `get_interest_rate`, `get_exchange_rate`。

关于完整的工具列表及其参数，请参考 `server.py` 文件中的 `handle_list_tools` 函数。

## 📄 开源协议

本项目采用 [GPL v3.0 许可证](./LICENSE) 开源。
