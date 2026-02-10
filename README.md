# Weather Videos (Mawaqit 360)

This repository hosts **weather background scene videos** used in the **Mawaqit 360 view**.  
The mobile app downloads and updates these videos dynamically based on a remote `manifest.json`.

The goal is to allow lightweight updates to weather animations **without shipping a new app release**.

---

## 📁 Directory Structure

```
weather-videos/
├── cloudy.mp4
├── overcast.mp4
├── light_rain.mp4
├── rain.mp4
├── snow.mp4
├── thunderstorm.mp4
├── sunny.mp4
└── manifest.json
```

- All weather scene videos live inside `weather-videos/`
- `manifest.json` controls versioning and download URLs

---

## 📄 manifest.json Format

```json
{
  "videos": {
    "cloudy": {
      "url": "https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/cloudy.mp4",
      "version": "1.0.0"
    },
    "overcast": {
      "url": "https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/overcast.mp4",
      "version": "1.0.0"
    },
    "light_rain": {
      "url": "https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/light_rain.mp4",
      "version": "1.0.0"
    },
    "rain": {
      "url": "https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/rain.mp4",
      "version": "1.0.0"
    },
    "snow": {
      "url": "https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/snow.mp4",
      "version": "1.0.0"
    },
    "thunderstorm": {
      "url": "https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/thunderstorm.mp4",
      "version": "1.0.0"
    }
  }
}
```

⚠️ **Important**: JSON keys must match your weather scene constants exactly (`cloudy`, `overcast`, `light_rain`, `rain`, `snow`, `thunderstorm`) for the app to recognize them.

---

## ⚙️ How the App Updates Videos

On app launch (with internet access):

1. App downloads remote `manifest.json`
2. Compares with local manifest
3. If a video's `version` differs → only that video is downloaded
4. Local cache updates automatically
5. New animation appears in Mawaqit 360

**Only changed videos are fetched.**

---

## 🚀 How to Update a Weather Video

### 1. Upload or Replace Video

Add or replace the `.mp4` file inside:

```
weather-videos/
```

File names can change. Only the `url` and `version` in `manifest.json` matter.

### 2. Update `manifest.json`

- Update `url` if filename changed
- Increment version manually

Example:

```json
"rain": {
  "url": "https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/rain.mp4",
  "version": "1.0.1"
}
```

### 3. Commit & Push

Once pushed to `main`, users will receive updates automatically on next app launch (if internet is available).

---

## 🧪 Helpful Commands

Generate manifest entries quickly:

```bash
for f in *.mp4; do
  name="${f%.*}"
  echo "\"$name\": {"
  echo "  \"url\": \"https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/$f\","
  echo "  \"version\": \"1.0.0\""
  echo "},"
done
```

---

## ⚠️ Guidelines

- Always increment version when a video changes
- Do not change version unnecessarily
- Verify raw GitHub URL works
- Keep JSON keys aligned with the weather scene constants
- Keep videos optimized for mobile

---

## 🤝 Contributing

Both internal and external contributors can update weather scenes.

Before merging:

- Verify video plays correctly
- Confirm version bump
- Validate JSON formatting

If unsure, open a PR and ask for review.