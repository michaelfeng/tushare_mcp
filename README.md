# Tushare MCP Server

[English](./README.md) | [中文](./README_zh.md)

[![PyPI version](https://badge.fury.io/py/tushare-mcp-server.svg)](https://badge.fury.io/py/tushare-mcp-server)

This project is a Model Context Protocol (MCP) server based on the [Tushare](https://tushare.pro/) data interface. It provides rich and comprehensive financial market data for mainland China, designed to be used with AI assistants.

## 🌟 Features

- **Easy Installation**: Packaged and distributed on PyPI. Install with a single `pip` command.
- **Simple to Run**: Provides a direct command-line interface (`tushare-mcp`) for starting the server.
- **Rich Data Access**: Wraps a large number of Tushare Pro APIs, covering stocks, indices, funds, bonds, and macroeconomics.
- **High Performance**: Built with asynchronous processing to support efficient queries.
- **Secure**: Uses environment variables to handle API tokens securely.

## 📦 Installation

This package is published on PyPI and can be installed using `pip`.

```bash
# Install from PyPI
pip install tushare-mcp-server
```

To upgrade to the latest version:
```bash
pip install --upgrade tushare-mcp-server
```

## ⚙️ Configuration

To use the full features of this server, you need a Tushare API Token. You can get a free token by registering on the [Tushare Pro website](https://tushare.pro/).

The server is designed to automatically read the token from an environment variable named `TUSHARE_TOKEN`. This is the only supported method when running the packaged version.

-   **On macOS/Linux:**
    ```bash
    export TUSHARE_TOKEN="your_tushare_token_here"
    ```
    To make this setting permanent, add the line to your shell's profile file (e.g., `~/.bash_profile`, `~/.zshrc`).

-   **On Windows:**
    ```bash
    set TUSHARE_TOKEN="your_tushare_token_here"
    ```
    To set it permanently, you can use the System Properties > Environment Variables panel.

## ▶️ Usage

Once the package is installed and the `TUSHARE_TOKEN` environment variable is set, you can run the server with a single command:

```bash
tushare-mcp
```

Upon successful startup, you will see the message: `✅ Tushare Token has been set.`

The server is now running and waiting for a connection from an MCP client.

### Configuring Your Agent

To make your local agent (e.g., Claude Desktop) use this server, you need to point it to a configuration file. The content should be:

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

## 🛠️ Available Tools

This server exposes a comprehensive set of tools to access financial data. Here are some of the categories:

-   **Basic Stock Data**: `get_stock_basic`, `get_daily_data`, `get_weekly_data`, `get_monthly_data`, etc.
-   **Market Reference Data**: `get_top_list`, `get_money_flow`, `get_margin_detail`, `get_block_trade`.
-   **Financial Data**: `get_financial_data`, `get_balance_sheet`, `get_cash_flow`, `get_fina_indicator`.
-   **Index Data**: `get_index_data`, `get_index_basic`, `get_index_weight`.
-   **ETF & Fund Data**: `get_etf_basic`, `get_etf_daily`, `get_fund_daily`, `get_fund_portfolio`.
-   **Bond Data**: `get_bond_basic`, `get_bond_daily`, `get_cb_basic`, `get_cb_daily`.
-   **Macroeconomic Data**: `get_gdp_data`, `get_cpi_data`, `get_interest_rate`, `get_exchange_rate`.

For a complete list of tools and their parameters, please refer to the source code in `server.py`.

## 💻 Development

If you want to contribute to the project or test local changes without reinstalling the package, you can run the server directly from the source code.

1.  Clone the repository:
    ```bash
    git clone https://github.com/michaelfeng/tushare_mcp.git
    cd tushare_mcp
    ```

2.  Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

3.  Set the `TUSHARE_TOKEN` environment variable as described in the Configuration section.

4.  Run the server script:
    ```bash
    python server.py
    ```

## 📄 License

This project is open-sourced under the [GPL v3.0 License](./LICENSE).
