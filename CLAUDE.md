# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Single-page market dashboard (`index.html`) — a self-contained HTML/CSS/JS file with no build system, no dependencies, and no tests. It displays live financial data in four corners of the screen:

- **Top-left**: Nifty (during IST market hours) or Nasdaq (otherwise)
- **Top-right**: Gold price (toggles to USD/INR)
- **Bottom-left**: TMB.NS stock (during IST market hours) or US Treasury yields (otherwise)
- **Bottom-right**: Bitcoin price (toggles to BTC dominance)

Clicking any corner toggles its alternate view.

## Architecture

- **Data sources**: Yahoo Finance (via corsproxy.io CORS proxy), CNBC quote API (treasury yields, no CORS proxy needed), Binance WebSocket + REST API, CoinGecko API
- **Refresh intervals**: Market data every 30s (`run()`), Bitcoin real-time via WebSocket (`@miniTicker`), BTC reference price every 60s, BTC dominance every 30s
- **IST market hours detection**: `isISTMarketHours()` uses `Intl` timezone conversion to check if current time is between 8:30 AM–6:00 PM IST to auto-select Indian vs US instruments
- **Color coding**: Green (`.g`) for up, Red (`.r`) for down, Gold (`.y`) for fixed-color items
- **Wake Lock API** keeps the screen on for always-on dashboard use
- **CSS naming is heavily abbreviated**: `.w` = widget wrapper, `.l` = label, `.p` = price, `.sm` = small font, `.sub` = subtext

## Development

Open `index.html` directly in a browser or serve with any static file server. No build step required.
