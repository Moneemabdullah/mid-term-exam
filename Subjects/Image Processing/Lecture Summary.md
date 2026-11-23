---
type: lecture-summary
subject: Image Processing
last_updated: 2026-11-23
---

# Image Processing — Lecture Summary

> [!info] Scope
> Based on the Introduction and Lectures 1–8. All lecture PDFs are image-only; OCR was used and may contain errors. The official syllabus was not provided.

## Source map

| Source | Topics |
|---|---|
| `Study Materials/Slides/Introduction.pdf` | DIP overview, stages, applications |
| `Study Materials/Slides/lec 1.pdf` | Pixels, resolution, RGB, imaging pipeline |
| `Study Materials/Slides/lec 2.pdf` | Storage, bit depth, neighborhoods, distance, interpolation |
| `Study Materials/Slides/lec 3.pdf` | Image acquisition, illumination, lenses, sensors, digitization |
| `Study Materials/Slides/lec 4.pdf` | Sampling and quantization |
| `Study Materials/Slides/lec 5.pdf` | Resampling, interpolation, aliasing, Nyquist |
| `Study Materials/Slides/Lec 6.pdf` | Human visual perception |
| `Study Materials/Slides/lec 7.pdf` | Intensity transformations |
| `Study Materials/Slides/lec 8.pdf` | Gamma correction, sRGB, applications |
| Shared notebook pp. 5–6, 18, 29–30, 37–38 | Sampling, perception, intensity transformations, gamma |

## Introduction

- **Video for this topic:** [Digital Image Processing Introduction](https://www.youtube.com/watch?v=F7NSNnd8-Ao) — GeeksforGeeks.
- **Digital image processing (DIP)** uses computers to process digital images.
- Main stages: acquisition → preprocessing → enhancement → segmentation → representation/description → recognition.
- Applications: medical imaging, remote sensing, industrial inspection, security, entertainment, robotics, document processing.
- A DIP system includes a sensor, digitizer, processor, memory, display, and software.

## Lecture 1 — Image basics

- **Video for this topic:** [How Computers Store Images: Pixels, Resolution and Colour Depth](https://www.youtube.com/watch?v=Z39Ohkzat70) — Prototype Education.
- A **digital image** is a 2D function `f(x, y)` sampled in space and quantized in intensity.
- A **pixel** is the smallest picture element; it has a location and an intensity/color value.
- **Spatial resolution:** number of pixels across width and height (for example, 1920×1080).
- **Intensity resolution / bit depth:** number of bits used per pixel (for example, 8-bit = 256 levels).
- **RGB:** additive color model with red, green, and blue channels; 8 bits per channel gives 24-bit color.
- **Imaging pipeline:** scene → illumination → sensor → digitizer → digital image → processing → display.
- More pixels and more bits give better quality but require more storage and processing.

## Lecture 2 — Storage, neighborhoods, distance, interpolation

- **Video for storage and bit depth:** [Digital Images, Bitmaps and Bit Depth](https://www.youtube.com/watch?v=sc0zV73gqy0) — Get Learnt w/ Chunck.
- **Video for distance metrics:** [Distance Measures Between Pixels](https://www.youtube.com/watch?v=NOIlN9Bexpk) — College Friendly.
- **Storage:** `width × height × bits per pixel / 8` bytes.
  - Grayscale 8-bit: one value per pixel.
  - Color 8-bit per channel: three values per pixel (24 bits).
- **Neighborhoods:**
  - 4-neighbors: north, south, east, west.
  - 8-neighbors: 4-neighbors plus diagonals.
- **Distance metrics:**
  - Euclidean: \(\sqrt{(x_2-x_1)^2 + (y_2-y_1)^2}\)
  - City-block/Manhattan: \(|x_2-x_1| + |y_2-y_1|\)
  - Chessboard: \(\max(|x_2-x_1|, |y_2-y_1|)\)
- **Indexing:** pixels are accessed by row and column; images can be stored row-major.
- **Interpolation:** estimates pixel values at non-integer coordinates; used in resizing and rotation.

## Lecture 3 — Image acquisition

- **Video for this topic:** [Image Sensing and Image Acquisition](https://www.youtube.com/watch?v=Za5wIGbE5mE) — Ekeeda.
- **Illumination:** light source; **reflectance:** fraction of light reflected by the object.
- A camera captures reflected light and focuses it through a **lens** onto a **sensor**.
- **Sensors:** CCD and CMOS convert light into electrical charge/voltage.
- **Digitizer:** converts the analog signal into digital values.
- **Saturation:** sensor element reaches its maximum value and loses detail.
- **Noise:** unwanted variation from sensor, electronics, or environment.
- **Spectrum:** imaging can use visible, infrared, X-ray, ultrasound, or other energy.
- **Sampling** and **quantization** convert the continuous signal into a digital image.

## Lecture 4 — Sampling and quantization

- **Video for this topic:** [Sampling and Quantization in Digital Image Processing](https://www.youtube.com/watch?v=KWc9SOOLfLw) — College Friendly.
- **Sampling:** discretizes spatial coordinates; determines the number of pixels.
- **Quantization:** discretizes intensity values; determines the number of gray levels.
- **Spatial resolution** is controlled by sampling; **intensity resolution** by quantization.
- More samples and levels give a closer approximation to the continuous image, but increase storage.
- **Aliasing** can occur if the sampling rate is too low.
- **Storage formula:** `M × N × k / 8` bytes, where `k` is bits per pixel.

## Lecture 5 — Resampling, interpolation, aliasing

- **Video for this topic:** [Nearest Neighbor, Bilinear and Bicubic Interpolation](https://www.youtube.com/watch?v=VjLPKq686Us) — Education journey.
- **Resampling:** changing the pixel grid (upsampling or downsampling).
- **Interpolation methods:**
  - Nearest-neighbor: fastest; blocky.
  - Bilinear: weighted average of 4 neighbors; smoother.
  - Bicubic: uses 16 neighbors; smoother but more computation.
- **Aliasing:** high-frequency detail appears as false low-frequency patterns when sampling is insufficient.
- **Nyquist theorem:** sampling rate must be at least twice the highest frequency in the signal.
- **Anti-aliasing:** low-pass filtering before sampling, or supersampling.

## Lecture 6 — Human visual perception

- **Video for this topic:** [Human Visual System and Elements of Visual Perception](https://www.youtube.com/watch?v=DSpDs4si3Os) — Study with Dr. Dafda.
- The eye focuses light through the cornea and lens onto the retina.
- **Rods:** sensitive to low light; no color; peripheral vision.
- **Cones:** color vision; high acuity; concentrated in the **fovea**.
- **Blind spot:** where the optic nerve leaves the retina; no photoreceptors.
- **Weber ratio:** \(\Delta I / I\) relates to brightness discrimination; the eye responds logarithmically.
- **Mach bands:** edge enhancement illusion caused by lateral inhibition.
- **Optical illusions:** show that perception is not a simple pixel-by-pixel recording.
- **8-bit/300 DPI:** common display/print standards; DPI relates to spatial resolution for printing.

## Lecture 7 — Intensity transformations

- **Video for this topic:** [Intensity Transformation Functions](https://www.youtube.com/watch?v=I-DnCh277xY) — The skill studio.
- An **intensity transformation** maps input intensity `r` to output intensity `s`: `s = T(r)`.
- **Negative:** `s = L - 1 - r`; reverses intensities; useful for medical/technical images.
- **Log transformation:** `s = c log(1 + r)`; compresses high dynamic range; expands dark values.
- **Inverse-log:** expands high values; compresses dark values.
- **Power-law/gamma:** `s = c r^γ`.
  - `γ < 1`: brightens the image, expands dark regions.
  - `γ > 1`: darkens the image, expands bright regions.
- **LUT (lookup table):** stores the mapping for fast implementation.
- **Contrast:** difference between light and dark values; transformations can stretch or compress it.
- **Monotonicity:** a monotonic transformation preserves intensity order; useful for avoiding artifacts.

## Lecture 8 — Gamma correction and sRGB

- **Video for this topic:** [What is Gamma Correction?](https://www.youtube.com/watch?v=wFx0d9c8WMs) — Video Tech Explained.
- **Gamma correction:** applies a power-law transform to compensate for nonlinear display/input response.
- Displays often have a gamma around 2.2; images may be encoded with an inverse gamma.
- **sRGB:** standard color space with a defined transfer function; widely used for web and displays.
- **Applications:** correct dark/bright images, improve visibility, prepare images for display.
- **Trade-offs:** gamma changes contrast and brightness; over-correction can wash out detail or amplify noise.
- Always apply gamma in the correct color space and bit depth.

## Quick formula sheet

| Concept | Formula |
|---|---|
| Storage (grayscale) | `W × H × k / 8` bytes |
| Storage (color) | `W × H × channels × k / 8` bytes |
| Negative | `s = L - 1 - r` |
| Log | `s = c log(1 + r)` |
| Power-law/gamma | `s = c r^γ` |
| Euclidean distance | \(\sqrt{(x_2-x_1)^2 + (y_2-y_1)^2}\) |
| Manhattan distance | \(|x_2-x_1| + |y_2-y_1|\) |
| Chessboard distance | \(\max(|x_2-x_1|, |y_2-y_1|)\) |

## Gaps

- Official syllabus not provided.
- Lab manual not provided.
- All lecture PDFs are image-only; OCR may contain errors.
- Confirm the overlap between `Introduction.pdf` and `lec 1.pdf`.
