# CloakBrowser

> A privacy-focused browser automation and scraping toolkit — Fork of [CloakHQ/CloakBrowser](https://github.com/CloakHQ/CloakBrowser)

[![CI](https://github.com/your-org/CloakBrowser/actions/workflows/ci.yml/badge.svg)](https://github.com/your-org/CloakBrowser/actions/workflows/ci.yml)
[![PyPI version](https://badge.fury.io/py/cloakbrowser.svg)](https://badge.fury.io/py/cloakbrowser)
[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

CloakBrowser provides a high-level API for browser automation with built-in fingerprint spoofing, proxy rotation, and anti-detection capabilities. Built on top of Playwright, it allows you to browse the web programmatically while minimizing detection by bot-protection systems.

## Features

- 🕵️ **Fingerprint Spoofing** — Randomize browser fingerprints (user-agent, canvas, WebGL, fonts)
- 🔄 **Proxy Rotation** — Seamlessly rotate proxies per request or session
- 🛡️ **Anti-Detection** — Bypass common bot detection mechanisms
- ⚡ **Async-First** — Built with `asyncio` for high-performance concurrent scraping
- 🧩 **Playwright-Backed** — Leverages Playwright for reliable cross-browser support
- 📦 **Simple API** — Intuitive interface for common browser automation tasks

## Installation

```bash
pip install cloakbrowser
```

Then install the required browser binaries:

```bash
playwright install chromium
```

## Quick Start

```python
import asyncio
from cloakbrowser import CloakBrowser

async def main():
    async with CloakBrowser() as browser:
        page = await browser.new_page()
        await page.goto("https://example.com")
        title = await page.title()
        print(f"Page title: {title}")
        await page.screenshot(path="screenshot.png")

asyncio.run(main())
```

### With Proxy Support

```python
import asyncio
from cloakbrowser import CloakBrowser, ProxyConfig

async def main():
    proxy = ProxyConfig(
        server="http://proxy.example.com:8080",
        username="user",
        password="pass"
    )

    async with CloakBrowser(proxy=proxy) as browser:
        page = await browser.new_page()
        await page.goto("https://httpbin.org/ip")
        content = await page.content()
        print(content)

asyncio.run(main())
```

### Fingerprint Spoofing

```python
import asyncio
from cloakbrowser import CloakBrowser, FingerprintConfig

async def main():
    fingerprint = FingerprintConfig(
        spoof_canvas=True,
        spoof_webgl=True,
        spoof_timezone="America/New_York",
        spoof_locale="en-US"
    )

    async with CloakBrowser(fingerprint=fingerprint) as browser:
        page = await browser.new_page()
        await page.goto("https://browserleaks.com")
        await page.screenshot(path="fingerprint_test.png")

asyncio.run(main())
```

## Configuration

| Option | Type | Default | Description |

## Notes (Personal Fork)

- I use `spoof_timezone="Europe/London"` and `spoof_locale="en-GB"` as my personal defaults since that matches my testing environment better than the `en-US` examples above.
- Tested primarily on Python 3.11 — haven't tried 3.9 myself.
