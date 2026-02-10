# Weather Videos (Mawaqit 360)

This repository hosts **weather background scene videos** used in the **Mawaqit 360 view**.
The mobile app downloads and updates these videos dynamically based on a remote `manifest.json`.

The goal is to allow lightweight updates to weather animations **without shipping a new app release**.

---

## 📁 Structure

```
weather-videos/
 ├── cloudy.mp4
 ├── rain.mp4
 ├── snow.mp4
 └── manifest.json
```

* All weather scene videos live inside `weather-videos/`
* `manifest.json` controls versioning, size, and download URLs

---

## 📄 manifest.json format

```json
{
  "videos": {
    "cloudy": {
      "url": "https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/cloudy.mp4",
      "version": "1.0.0",
      "size": 456931
    }
  }
}
```

### Fields

| Field     | Description                        |
| --------- | ---------------------------------- |
| `url`     | Direct GitHub raw URL to the video |
| `version` | Manual version number              |
| `size`    | File size in **bytes**             |

**Important:**
Size must be in bytes (not KB/MB).

---

## ⚙️ How the app updates videos

On app launch (when internet is available):

1. App downloads remote `manifest.json`
2. Compares with local manifest
3. If a video's `version` differs → only that video is downloaded
4. Local cache updates automatically
5. New animation appears in Mawaqit 360

Only changed videos are fetched.

---

## 🚀 How to update a weather video

### 1. Upload or replace video

Add or replace the `.mp4` file inside:

```
weather-videos/
```

File names can change.
Only the `url` and `version` in `manifest.json` matter.

---

### 2. Get file size (bytes)

macOS:

```bash
stat -f%z rain.mp4
```

Linux:

```bash
stat -c%s rain.mp4
```

---

### 3. Update `manifest.json`

* Update `url` if filename changed
* **Increment version manually**
* Update `size` in bytes

Example:

```json
"rain": {
  "url": "https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/rain.mp4",
  "version": "1.0.1",
  "size": 2536636
}
```

---

### 4. Commit & push

Once pushed to `main`, users will receive updates automatically
on next app launch (if internet is available).

---

## 🧪 Helpful commands

Print filename + size in bytes (macOS):

```bash
stat -f "%N %z" *.mp4
```

Generate manifest entries quickly:

```bash
for f in *.mp4; do
  name="${f%.*}"
  size=$(stat -f%z "$f")
  echo "\"$name\": {"
  echo "  \"url\": \"https://raw.githubusercontent.com/mawaqit/mobile-assets/main/weather-videos/$f\","
  echo "  \"version\": \"1.0.0\","
  echo "  \"size\": $size"
  echo "},"
done
```

---

## ⚠️ Guidelines

* Always increment version when a video changes
* Do not change version unnecessarily
* Ensure size is correct
* Verify raw GitHub URL works
* Keep videos optimized for mobile

---

## 🤝 Contributing

Both internal and external contributors can update weather scenes.

Before merging:

* Verify video plays correctly
* Confirm size in bytes
* Confirm version bump
* Validate JSON formatting

If unsure, open a PR and ask for review.
