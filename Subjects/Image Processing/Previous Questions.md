---
type: previous-questions
subject: Image Processing
source: ClassTestQuestions.pdf
last_updated: 2026-11-23
---

# Image Processing — Previous Questions

> [!info] Source
> Transcribed from `ClassTestQuestions.pdf` (5-page scanned class-test paper, scanned 17 November 2026). This is **CT-1** for Digital Image Processing.

## Question bank

| Question | Marks | Topic | Status |
|---|---|---|---|
| 1(a) What is a pixel? | Part of 3 | Image basics | Answered |
| 1(b) Define a digital image. | Part of 3 | Image basics | Answered |
| 1(c) What does `0` usually represent? | Part of 3 | Intensity | Answered |
| 2. Why does a computer see an image as numbers? | 2 | Digitization | Answered |
| 3. Storage for 500×500 grayscale and color images | 5 | Storage | Answered |

**Total:** 10 marks · 30 minutes.

## Q1(a). What is a pixel? [CO1→C1]

**Answer.**

A **pixel** (picture element) is the smallest individual element of a digital image. It represents the intensity or color at one spatial location, identified by its row and column coordinates. In a grayscale image, a pixel holds one intensity value; in a color image, it holds a combination of channel values (for example, red, green, and blue).

## Q1(b). Define a digital image. [CO1→C1]

**Answer.**

A **digital image** is a two-dimensional representation of an image formed by a finite set of pixels arranged in rows and columns. Each pixel has a discrete intensity or color value. Mathematically, it can be written as `f(x, y)`, where `x` and `y` are discrete spatial coordinates and `f` is the intensity at that point.

## Q1(c). What does the number `0` usually represent in a digital image? [CO1→C1]

**Answer.**

In a grayscale image, `0` usually represents the **lowest intensity**, which is displayed as **black**. In an RGB color image, a pixel with `(0, 0, 0)` represents black because all three color channels are at their minimum. In general, `0` means no light/signal contribution at that pixel.

## Q2. Explain in your own words why a computer sees an image as numbers. [CO1→C2] [2]

**Answer.**

A computer cannot directly store or process light. During **image acquisition**, a sensor converts light intensity into an electrical signal. The signal is then **sampled** (measured at discrete spatial locations) and **quantized** (rounded to a finite set of intensity levels). The result is a matrix of numbers, where each number represents the intensity or color of a pixel. The computer processes these numbers using algorithms, and a display converts the numbers back into visible light.

**Key chain:** light → sensor → electrical signal → sampling → quantization → numeric matrix → processing/display.

## Q3. Calculate the storage requirements in bytes for a 500×500 grayscale image with 8-bit pixels and a 500×500 color image with 8 bits per channel. [5]

**Answer.**

### Grayscale image

- Pixels: `500 × 500 = 250,000`
- Bits per pixel: `8`
- Total bits: `250,000 × 8 = 2,000,000 bits`
- Total bytes: `2,000,000 / 8 = 250,000 bytes`

\[
\boxed{250{,}000\ \text{bytes} \approx 244.14\ \text{KiB}}
\]

### Color image

Assume three channels (R, G, B), each 8 bits:

- Bits per pixel: `3 × 8 = 24 bits`
- Total bits: `250,000 × 24 = 6,000,000 bits`
- Total bytes: `6,000,000 / 8 = 750,000 bytes`

\[
\boxed{750{,}000\ \text{bytes} \approx 732.42\ \text{KiB}}
\]

### Combined

\[
250{,}000 + 750{,}000 = \boxed{1{,}000{,}000\ \text{bytes}}
\]

**Exam tip:** always state the channel assumption. If the color image is not RGB, the number of channels may differ.

## Exam tips

- Pixel = smallest picture element; digital image = matrix of pixels.
- `0` = black/lowest intensity in grayscale; `(0,0,0)` = black in RGB.
- Storage = width × height × bits per pixel / 8.
- For color, multiply by the number of channels.
- Keep units clear: bits vs bytes.
