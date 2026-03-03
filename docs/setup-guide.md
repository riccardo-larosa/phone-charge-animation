# Setup Guide

Get the charging animation running on your Pixel phone in about 10 minutes.

## 1. Set up GitHub Pages

1. Fork or clone this repo to your own GitHub account.
2. Go to **Settings > Pages**.
3. Under "Build and deployment", choose **Deploy from a branch**.
4. Select **main** branch, **/ (root)** folder, and click **Save**.
5. After a minute or two, your page will be live at:
   `https://YOUR-USERNAME.github.io/phone-charge-animation/`

## 2. Install Tasker

Download [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm) from the Play Store ($3.49). It automates opening the animation when you plug in your charger.

## 3. Import the Tasker profile

1. Download `charging-animation.prj.xml` from the `tasker/` folder in this repo (or clone the whole repo to your phone).
2. Open Tasker.
3. Long-press the **Projects** tab at the bottom.
4. Tap **Import**.
5. Select the downloaded `.prj.xml` file.

You should see a new project called "Charging Animation" with one profile and two tasks.

## 4. Configure the URL

1. In Tasker, open the **Start Charge Animation** task.
2. Tap **Action 2** (the "Variable Set" action that sets `%url`).
3. Replace `USERNAME` with your actual GitHub username in the URL.
4. Tap the back arrow to save.

## 5. Test it

Plug in your phone. After a 2-second delay, Chrome should open with the animation showing your live battery percentage, charging wattage, and estimated time to full.

You can also test manually by visiting your GitHub Pages URL with parameters:

```
https://YOUR-USERNAME.github.io/phone-charge-animation/?level=75&watts=27&timeLeft=42
```

## 6. Optional: Add to Home Screen

For a full-screen, app-like experience:

1. Open your GitHub Pages URL in Chrome.
2. Tap the three-dot menu.
3. Tap **Add to Home Screen**.

Launching from the home screen icon hides the browser toolbar.

## 7. Troubleshooting

**Wattage shows "--"**
The Tasker profile reads current and voltage from `/sys/class/power_supply/battery/`. Some devices use different sysfs paths (e.g., `current_avg` instead of `current_now`). Check which files exist on your device and update Actions 3-4 in the Start Charge Animation task.

**Chrome doesn't open when plugging in**
- Make sure Tasker has permission to run in the background (Settings > Apps > Tasker > Battery > Unrestricted).
- Make sure the "Charge Animation" profile is enabled (green toggle in Tasker).
- On Android 13+, grant Tasker the "Display over other apps" permission.

**Time to full shows "--"**
The `dumpsys battery` output varies by device and Android version. If `time_to_full_now` isn't available, the field will be blank. This is cosmetic only; the animation still works.

**Animation is laggy**
The particle count scales with wattage. On older devices, you can reduce `MAX_PARTICLES` in `index.html` (default is 150).
