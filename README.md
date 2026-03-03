# Phone Charge Animation

A full-screen charging animation for Android phones, designed for Pixel devices. Plug in your charger and watch electric particles rise from the bottom of the screen while your battery stats update in real time.

## What it looks like

A black OLED-friendly screen with glowing cyan particles drifting upward. In the center, a circular progress ring fills as your battery charges. Below it, your current charging wattage and estimated time to full are displayed.

## Features

- Animated electric particles that scale with charging wattage
- Circular battery progress ring with percentage
- Live charging wattage display
- Estimated time to full charge
- OLED-friendly pure black background
- Screen wake lock to prevent display timeout
- Launches and closes automatically via Tasker

## Quick Start

See the [Setup Guide](docs/setup-guide.md) for step-by-step instructions.

## How It Works

The animation is a single HTML page hosted on GitHub Pages. It reads battery data from URL parameters:

```
?level=75&watts=27&timeLeft=42
```

| Parameter  | Description                        |
|------------|------------------------------------|
| `level`    | Battery percentage (0-100)         |
| `watts`    | Charging power in watts            |
| `timeLeft` | Minutes until full charge          |

A Tasker profile on your phone detects when a charger is connected, reads live battery stats from the system, builds the URL with those values, and opens it in Chrome. When you unplug, Tasker closes the browser.

The Tasker project file is included at `tasker/charging-animation.prj.xml`.

## License

MIT
