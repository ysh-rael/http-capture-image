# http-capture-image

Simple Node.js utility library to capture images (or other media) from HTTP endpoints
and store them on disk using a date-based directory structure.

This library was originally created to capture images from IP cameras or HTTP devices
that require Basic Authentication.

---

## ✨ Features

- Capture images via HTTP request
- Support for Basic Auth
- Automatic directory creation
- Date-based folder structure
- Customizable file and folder naming
- Image, audio or video support (by extension)

---

## 📦 Installation

```bash
npm install http-capture-image
```

---

## 🚀 Usage

### Basic example

```js
const { Recorder, FileHandler } = require('http-capture-image');

const recorder = new Recorder({
  url: 'http://camera-ip/image.jpg',
  username: 'admin',
  password: 'admin',
  root: './captures',
  equipment: 'parking-lot',
  camera: 'cam01',
  type: 'image'
});

const fileHandler = new FileHandler();

const folderPath = recorder.getMediaTypePath();
fileHandler.createDirIfNotExists(folderPath);

const filename = recorder.getFilename(folderPath);

recorder.captureImage({ filename }, (err, filePath) => {
  if (err) {
    console.error('Error capturing image');
    return;
  }

  console.log('Image saved at:', filePath);
});
```

---

## 🗂 Directory Structure Example

```txt
captures/
└── 14-01-2026/
    └── 09/
        └── parking-lot/
            └── cam01/
                └── image/
                    └── 2026-01-14-9-30-05.jpg
```

---

## ⚙️ Recorder Configuration Options

| Option                | Type   | Description                                      |
| --------------------- | ------ | ------------------------------------------------ |
| `url`                 | string | HTTP endpoint to capture media                   |
| `username`            | string | Basic Auth username                              |
| `password`            | string | Basic Auth password                              |
| `root`                | string | Root folder for saving files                     |
| `equipment`           | string | Equipment identifier                             |
| `camera`              | string | Camera identifier                                |
| `type`                | string | `image`, `audio` or `video`                      |
| `directoryPathFormat` | string | Date format (default: `DD-MM-YYYY`)              |
| `fileNameFormat`      | string | File name format (default: `YYYY-MM-DD-h-mm-ss`) |

---

## 🧰 Exposed Modules

```js
const {
  Recorder,
  FileHandler
} = require('http-capture-image');
```

* **Recorder**: Handles HTTP capture and file naming
* **FileHandler**: Creates directories recursively if they don't exist

---

## 📌 Notes

* Uses `request` internally (deprecated but still functional)
* Uses `moment` for date formatting
* No external database or framework dependency

---

## 📄 License

ISC

Original Author: Deivid de Oliveira Souza  
Maintained by: Ysh-rael
