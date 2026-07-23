# n8n-nodes-cloakbrowser

> A modern CloakBrowser automation node for n8n powered by Puppeteer.

`n8n-nodes-browser` brings browser automation to n8n with support for local Chromium, Browserless, CloakBrowser, and any Chrome DevTools Protocol (CDP) compatible browser.

## Features

- 🌐 Browser automation using Puppeteer
- 🚀 Remote browser support via CDP
- 🥷 Native CloakBrowser support (no browser ID management)
- ☁️ Browserless compatible
- 📸 Screenshots
- 📄 PDF generation
- 🖱 Mouse & keyboard automation
- 🍪 Cookie management
- 📦 Download files
- 🔍 Extract structured data from websites
- ⚡ Works with n8n queue mode

## Installation

### Community Nodes

Search for

```
n8n-nodes-cloakbrowser
```

or install via npm package.

### Docker

```dockerfile
FROM docker.n8n.io/n8nio/n8n:latest

RUN cd /home/node/.n8n \
 && npm init -y \
 && npm install n8n-nodes-cloakbrowser
```

## Supported Browser Providers

| Provider | Supported |
|-----------|-----------|
| Local Chrome | ✅ |
| Local Chromium | ✅ |
| Browserless | ✅ |
| CloakBrowser | ✅ |
| Remote Chrome (CDP) | ✅ |

## CloakBrowser

Unlike the original package, this node supports automatic browser discovery.

Instead of configuring

```
ws://browser:9222/devtools/browser/<browser-id>
```

configure

```
http://cloakbrowser:9222
```

The node automatically resolves the current browser endpoint before every execution.

No browser IDs.
No manual updates after restarts.

Example:

```yaml
PUPPETEER_BROWSER_DISCOVERY_URL=http://cloakbrowser:9222/json/version
```

## Browserless

```yaml
PUPPETEER_BROWSER_WS_ENDPOINT=ws://browserless:3000
```

## Remote Chrome

Works with any browser exposing the Chrome DevTools Protocol.

## Configuration

| Environment Variable | Description |
|----------------------|-------------|
| PUPPETEER_BROWSER_DISCOVERY_URL | CloakBrowser discovery endpoint |
| PUPPETEER_BROWSER_WS_ENDPOINT | Static CDP websocket endpoint |
| PUPPETEER_PROTOCOL | Browser protocol (`cdp`) |
| PUPPETEER_EXECUTABLE_PATH | Local Chrome executable |

Discovery URL takes precedence over static browser IDs.

## Why this fork?

The original project assumes a static CDP WebSocket endpoint.

Modern browser providers such as CloakBrowser generate a new browser WebSocket endpoint whenever the browser restarts.

This package automatically discovers the latest endpoint before connecting, eliminating the need to manually update browser IDs.

Additional improvements include:

- automatic browser discovery
- better remote browser support
- improved Docker experience
- compatibility with CloakBrowser
- future Playwright support

## Roadmap

- [x] Puppeteer support
- [x] Browserless
- [x] CloakBrowser
- [x] Automatic browser discovery
- [ ] Playwright
- [ ] Session persistence
- [ ] Browser pools
- [ ] HAR recording
- [ ] Video recording

## License

MIT
