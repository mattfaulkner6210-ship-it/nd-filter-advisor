# DJI ND Filter Advisor

A free, mobile-first web app for DJI drone pilots. Meter the light with your iPhone camera, select your drone, and instantly get the correct ND filter recommendation using the 180° shutter rule — no guesswork, no separate apps needed.

**Live app:** [https://mattfaulkner6210-ship-it.github.io/nd-filter-advisor/](https://mattfaulkner6210-ship-it.github.io/nd-filter-advisor/)

---

## What the app does

1. **Selects your DJI drone** — aperture is set automatically for fixed-lens models, or you can input your chosen aperture for variable-aperture drones
2. **Meters the live light** using your iPhone's rear camera — tap anywhere on the viewfinder to place the spot meter on the brightest part of the sky
3. **Recommends the correct ND filter** based on your drone, frame rate, ISO, and the current light conditions
4. **Shows a conditions guide** that highlights where your current reading sits — from intense direct sun down to low light — with typical filter ranges for each condition
5. **Remembers your settings** — your last drone, frame rate, ISO and aperture are saved and pre-loaded next time you open the app

---

## What are ND filters?

ND (Neutral Density) filters are like sunglasses for your drone's camera. They reduce the amount of light entering the lens without affecting colour, allowing you to control your shutter speed independently of the available light.

### Why drone pilots use ND filters

Drone cameras — particularly DJI consumer models — mostly have fixed apertures. This means you cannot control depth of field the way you can on a DSLR, and your primary exposure controls are shutter speed and ISO. In bright conditions, this forces the shutter speed very high, resulting in footage that looks unnaturally sharp and "choppy" — a common problem called the **jelly roll effect**.

The solution is to fit an ND filter to slow the shutter speed down to a natural-looking range, producing smooth, cinematic motion blur.

### The 180° shutter rule

The 180° shutter rule is the gold standard for cinematic video. It states that your shutter speed should be **double your frame rate**:

| Frame rate | Target shutter speed |
|---|---|
| 24 fps | 1/48s |
| 25 fps | 1/50s |
| 30 fps | 1/60s |
| 60 fps | 1/120s |

This ratio produces natural-looking motion blur that matches how our eyes perceive movement, giving footage a filmic quality rather than the harsh, video-like look of a high shutter speed.

### ND filter strengths

ND filters are rated by how many stops of light they block:

| Filter | Light reduction | Stops blocked | Typical use |
|---|---|---|---|
| ND4 | 1/4 | 2 stops | Dusk / dawn / golden hour |
| ND8 | 1/8 | 3 stops | Heavy overcast / shade |
| ND16 | 1/16 | 4 stops | Full overcast |
| ND32 | 1/32 | 5 stops | Hazy daylight |
| ND64 | 1/64 | 6 stops | Full daylight |
| ND128 | 1/128 | 7 stops | Bright sun |
| ND256+ | 1/256+ | 8+ stops | Intense direct sun |

Each step up doubles the filter strength and allows the shutter speed to be halved. Choosing the wrong filter results in either overexposed footage (filter too weak) or underexposed footage (filter too strong).

---

## How the app calculates the recommended filter

The app uses the following logic:

1. **Measures the scene brightness** by sampling a spot from the live camera feed and calculating an Exposure Value (EV) reading at ISO 100
2. **Calculates the unfiltered shutter speed** — what shutter speed the drone would need to achieve correct exposure at ISO 100 with its fixed aperture and no filter fitted
3. **Calculates the target shutter speed** using the 180° rule: `1 ÷ (frame rate × 2)`
4. **Computes the stop difference** between the unfiltered shutter speed and the target shutter speed
5. **Selects the nearest ND filter** from the standard DJI filter range that matches the required stop reduction

### Example

- Drone: DJI Mini 4 Pro (f/1.7 fixed aperture)
- Frame rate: 30 fps → target shutter: 1/60s
- Measured EV: 13 (bright daylight)
- Unfiltered shutter speed at f/1.7, ISO 100: approx 1/2000s
- Stops needed to reach 1/60s: ~5 stops
- Recommended filter: **ND32**

---

## Supported drones

| Series | Models |
|---|---|
| Mini | Mini 2, Mini 3, Mini 3 Pro, Mini 4 Pro, Mini 5 Pro |
| Air | Air 2, Air 2S, Air 3 (wide + tele) |
| Mavic | Mavic 4 Pro (wide / mid-tele / tele), Mavic 2 Pro, Mavic 3 Pro, Mavic 3 Classic |
| Phantom | Phantom 4 Pro |
| Other | Avata, Neo |

Fixed-aperture drones have their aperture set automatically. Variable-aperture drones (Mavic series, Phantom 4 Pro) allow you to input your chosen aperture.

---

## How to use

1. Open the app in **Safari on iPhone**
2. Tap **Share → Add to Home Screen** to install it as a full-screen app
3. Select your **DJI drone** from the dropdown
4. Set your **frame rate** and **ISO** (ISO 100 recommended)
5. Tap **Start camera meter** and allow camera access
6. Point toward the **brightest part of the sky** and tap to place the meter spot there
7. Read the **recommended ND filter** from the green panel
8. Fit the filter to your drone **before take-off**, set manual mode, and fly

> **Tip:** Always meter toward the sun direction, even when shooting in another direction. This protects your highlights — blown sky cannot be recovered in post, but underexposed shadows can.

---

## Technical notes

- Built as a single HTML file — no frameworks, no dependencies, no server required
- Uses the browser `getUserMedia` API for live camera access (requires `https://` — works via GitHub Pages)
- Camera permission prompt shows the app name when launched from the home screen icon
- Settings are saved using `localStorage` and persist between sessions
- Works in any modern browser over `https://` — optimised for iPhone Safari
- Offline capable once loaded and added to home screen

---

## Limitations

- Light metering via browser camera is a good approximation but is not as precise as a dedicated hardware light meter. For critical professional work, consider verifying with a dedicated metering app
- The camera uses your iPhone's auto-exposure as a base reference — for best results, hold the phone steady and point directly at the sky before tapping the meter spot
- Camera access is blocked when the file is opened directly from local storage (`file://`) — the app must be accessed via `https://` to enable the camera meter

---

## License

Free to use and share. Built for the DJI drone community.
