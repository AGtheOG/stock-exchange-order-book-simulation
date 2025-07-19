# Limit Order Book - Mini Project

This project implements a simple limit order book using Node.js and Express. It allows users to place bid (buy) and ask (sell) limit orders, automatically matches orders based on price, and updates balances accordingly.

## Features

- Place bid and ask limit orders
- Match orders if prices overlap
- View order book depth
- Track user balances
- Basic quote endpoint (partially implemented)
- Test coverage using Jest and SuperTest

## Project Structure

```
.
─ index.ts             # Main logic and server
─ index.spec.ts        # Core functionality tests
─ assignment.mock.ts   # Quote-related test
```

## API Endpoints

### POST /order

Place a limit order.

**Request Body:**
```json
{
  "type": "limit",
  "side": "bid" | "ask",
  "price": number,
  "quantity": number,
  "userId": "1"
}
```

**Response:**
```json
{
  "filledQuantity": number
}
```

### GET /depth

Returns the current state of the order book.

**Response:**
```json
{
  "depth": {
    "price": {
      "type": "bid" | "ask",
      "quantity": number
    }
  }
}
```

### GET /balance/:userId

Returns the balances of the given user.

**Example Response:**
```json
{
  "balances": {
    "GOOGLE": 10,
    "USD": 50000
  }
}
```

### POST /quote *(partially implemented)*

TODO: Return quote for a given side and quantity.

## How Matching Works

- Orders are matched against the opposite side if prices are favorable.
- If fully matched, nothing is added to the order book.
- If partially matched, remaining quantity is added to the order book.
- Matching updates user balances using `flipBalance`.

## Running Tests

Install dependencies and run tests:

```bash
npm install
npm test
```

## Users

Two default users exist:

- User 1: `id: "1"` with 10 GOOGLE, 50000 USD
- User 2: `id: "2"` with 10 GOOGLE, 50000 USD

## Improvements

- Complete the quote endpoint
- Add order cancellation
- Support market orders
- Store users/orders in a persistent DB