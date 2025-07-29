# Binance Futures Trading Bot 🤖

A comprehensive, Command-Line Interface (CLI) based trading bot designed for the **Binance USDT-M Futures Testnet**. This bot features a robust, interactive interface that guides the user through placing various order types, from basic market orders to advanced strategies like TWAP and Grid trading.

## ✨ Key Features

  - **Interactive CLI**: A user-friendly, prompt-based interface that asks for inputs one-by-one with helpful hints and built-in validation.
  - **Core Order Types**:
      - Market Orders
      - Limit Orders
  - **Advanced Trading Strategies**:
      - **Stop-Limit Orders**: Place a conditional limit order.
      - **OCO (One-Cancels-the-Other)**: Place a simultaneous take-profit and stop-loss.
      - **TWAP (Time-Weighted Average Price)**: Execute large orders in smaller chunks over time.
      - **Grid Trading**: Place a grid of buy and sell orders to profit from volatility.
  - **Structured Logging**: All actions, API responses, and errors are automatically logged with timestamps to `bot.log` for easy auditing and debugging.
  - **Secure Configuration**: API credentials are kept secure and separate from the source code using a `.env` file.

-----

## 📂 Project Structure

The project is organized in a modular structure for clarity and scalability.

```
binance-futures-bot/
│
├── .env
├── README.md
├── requirements.txt
├── bot.log
│
└── src/
    ├── __init__.py
    ├── client.py
    ├── market_orders.py
    ├── limit_orders.py
    │
    └── advanced/
        ├── __init__.py
        ├── stop_limit_orders.py
        ├── oco_orders.py
        ├── twap_orders.py
        └── grid_orders.py
```

-----

## ⚙️ Setup and Installation

Follow these steps to set up and run the bot on your local machine.

### 1\. Clone the Repository

```bash
git clone <your-github-repo-url>
cd binance-futures-bot
```

### 2\. Create and Activate a Virtual Environment

It is highly recommended to use a virtual environment to manage project dependencies.

```bash
# Create the environment
python -m venv venv

# Activate it
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3\. Install Dependencies

Install all the required Python libraries from the `requirements.txt` file.

```bash
pip install -r requirements.txt
```

### 4\. Configure API Credentials

The bot requires API keys from the [Binance Futures Testnet](https://testnet.binancefuture.com/).

  - Create a file named `.env` in the project's root directory.
  - Copy the following format and paste your Testnet API Key and Secret.

<!-- end list -->

```
# .env file
BINANCE_API_KEY="YOUR_TESTNET_API_KEY"
BINANCE_API_SECRET="YOUR_TESTNET_API_SECRET"
```

-----

## 🚀 How to Use the Bot

All scripts are run from the project's root directory. They will interactively prompt you for the necessary information.

### Market Order

To place an order that executes immediately at the current market price.

**Command:**

```bash
python src/market_orders.py
```

**Example Interaction:**

```
--- Place a New Market Order ---
Enter symbol (e.g., BTCUSDT): BTCUSDT
Enter side (BUY or SELL): BUY
Enter quantity: 0.001
```

### Limit Order

To place an order that executes only at a specified price or better.

**Command:**

```bash
python src/limit_orders.py
```

**Example Interaction:**

```
--- Place a New Limit Order ---
Enter symbol (e.g., BTCUSDT): BTCUSDT
Enter side (BUY or SELL): SELL
Enter quantity: 0.002
Enter limit price for the SELL order: 68000
```

### Stop-Limit Order (Advanced)

To place a conditional order that activates when a trigger price is hit. The script provides hints to ensure the trigger price is logical relative to the current market.

**Command:**

```bash
python -m src.advanced.stop_limit_orders
```

**Example Interaction:**

```
--- Place a New Stop-Limit Order ---
First, check the current market price of your symbol.
Enter symbol (e.g., BTCUSDT): BTCUSDT
Enter side (BUY or SELL): BUY
Enter quantity: 0.002
Enter trigger/stop price (must be ABOVE current market): 67000
Enter limit price (the price your order will be placed at): 67100
```

### OCO Order (Advanced)

To place a pair of orders (take-profit and stop-loss) simultaneously.

**Command:**

```bash
python -m src.advanced.oco_orders
```

**Example Interaction:**

```
--- Place a New OCO (One-Cancels-the-Other) Order ---
First, check the current market price of your symbol.
Enter symbol (e.g., BTCUSDT): BTCUSDT
Enter side to CLOSE the position (BUY or SELL): SELL
Enter quantity to close: 0.002
Enter Take Profit price (must be ABOVE current market): 68000
Enter Stop Loss price (must be BELOW current market): 62000
```

### TWAP Order (Advanced)

To execute a large order by breaking it into smaller pieces over a specified duration.

**Command:**

```bash
python -m src.advanced.twap_orders
```

**Example Interaction:**

```
--- Place a New TWAP Order ---
Enter symbol (e.g., BTCUSDT): BTCUSDT
Enter side (BUY or SELL): BUY
Enter total quantity to execute: 0.1
Enter total duration in MINUTES: 60
Enter number of smaller orders to place: 10
```

### Grid Trading (Advanced)

To place a grid of buy and sell limit orders within a defined price range.

**Command:**

```bash
python -m src.advanced.grid_orders
```

**Example Interaction:**

```
--- Place a New Grid of Orders ---
Enter symbol (e.g., BTCUSDT): BTCUSDT
Enter the lower price boundary of the grid: 60000
Enter the upper price boundary of the grid: 70000
Enter the number of grid lines (e.g., 5): 7
Enter the quantity for each grid order: 0.002
```

-----

## 📝 Logging

All bot activities, including order placements, successful API responses, and any errors encountered, are logged in a structured format to **`bot.log`**. This file is essential for auditing and debugging the bot's behavior.

-----

## 👤 Author

**Abhi Ghudaiya**