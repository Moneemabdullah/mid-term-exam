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

**Marking scheme:** definition (1) + spatial location (1) + grayscale vs color (1).

A **pixel** (picture element) is the smallest individual element of a digital image. It represents the intensity or color at one spatial location, identified by its row and column coordinates `(x, y)`. In a grayscale image, a pixel holds one intensity value; in a color image, it holds a combination of channel values (for example, red, green, and blue).

---

## Q1(b). Define a digital image. [CO1→C1]

**Answer.**

**Marking scheme:** 2D representation (1) + finite set of pixels (1) + mathematical notation `f(x, y)` (1).

A **digital image** is a two-dimensional representation of an image formed by a finite set of pixels arranged in rows and columns. Each pixel has a discrete intensity or color value. Mathematically, it can be written as `f(x, y)`, where `x` and `y` are discrete spatial coordinates and `f` is the intensity at that point.

---

## Q1(c). What does the number `0` usually represent in a digital image? [CO1→C1]

**Answer.**

**Marking scheme:** grayscale = black (1) + RGB `(0,0,0)` = black (1) + general meaning no light/signal (1).

In a grayscale image, `0` usually represents the **lowest intensity**, which is displayed as **black**. In an RGB color image, a pixel with `(0, 0, 0)` represents black because all three color channels are at their minimum. In general, `0` means no light/signal contribution at that pixel.

---

## Q2. Explain in your own words why a computer sees an image as numbers. [CO1→C2] [2]

**Answer.**

**Marking chain:** light → sensor → electrical signal → sampling → quantization → numeric matrix → processing/display (2 marks).

A computer cannot directly store or process light. During **image acquisition**, a sensor (CCD/CMOS) converts light intensity into an electrical signal. The signal is then **sampled** (measured at discrete spatial locations) and **quantized** (rounded to a finite set of intensity levels). The result is a matrix of numbers, where each number represents the intensity or color of a pixel. The computer processes these numbers using algorithms, and a display converts the numbers back into visible light.

---

## Q3. Calculate the storage requirements in bytes for a 500×500 grayscale image with 8-bit pixels and a 500×500 color image with 8 bits per channel. [5]

**Answer.**

**Marking scheme:** grayscale pixels/bits/bytes (2) + color bytes (2) + combined total (1).

**Formula:** `Storage (bytes) = W × H × k / 8`, where `k` = bits per pixel (per channel for color).

### Grayscale image
- Pixels: `500 × 500 = 250,000`
- Bits per pixel: `8`
- Total bits: `250,000 × 8 = 2,000,000 bits`
- Total bytes: `2,000,000 / 8 = 250,000 bytes`

\[
\boxed{250{,}000\ \text{bytes} \approx 244.14\ \text{KiB}}
\]

### Color image (3 channels, 8 bits per channel)
- Bits per pixel: `3 × 8 = 24 bits`
- Total bits: `250,000 × 24 = 6,000,000 bits`
- Total bytes: `6,000,000 / 8 = 750,000 bytes`

\[
\boxed{750{,}000\ \text{bytes} \approx 732.42\ \text{KiB}}
\]

### Combined
\[
250{,}000 + 750{,}000 = \boxed{1{,}000{,}000\ \text{bytes} \approx 953.67\ \text{KiB}}
\]

**Exam tip:** Always state the channel assumption. If the color image is not RGB, the number of channels may differ.

---

## Exam tips

- Pixel = smallest picture element; digital image = matrix of pixels.
- `0` = black/lowest intensity in grayscale; `(0,0,0)` = black in RGB.
- Storage = width × height × bits per pixel / 8.
- For color, multiply by the number of channels.
- Keep units clear: bits vs bytes.

---

## Previous-semester questions (scanned papers)

> [!info] Source
> Scanned CSE 4-2 previous Mid Term/Final papers from `../Previous QW/` were OCR’d. Only Digital Image Processing (CSE 443) questions are included below.

### IP — Final Spring 2026, CSE 443 (page 1)

**Q1(a).** State the Fourier Theorem. Explain the roles of fundamental frequency and harmonics in representing a complex signal. [10]

**Q1(b).** Differentiate among Fourier Series, Fourier Transform, and Discrete Fourier Transform. [10]

**Q1(c) (OR).** Compare low-pass, high-pass, and band-pass frequency-domain filters. [10]

**Q1(d) (OR).** Describe the frequency-domain image-processing workflow from input image to processed spatial-domain image. [10]

**Answer.**

**Marking scheme (Q1a):** theorem statement (3) + fundamental frequency (2) + harmonics (2) + image example (3).
**Marking scheme (Q1b):** three transforms defined with input/output (6) + comparison summary (4).
**Marking scheme (Q1c):** three filters defined with effect (6) + example use (4).
**Marking scheme (Q1d):** four steps in order (4) + purpose of each step (6).

**(a) Fourier Theorem:** Any periodic signal can be represented as a sum of sinusoids (sines and cosines). The **fundamental frequency** is the lowest frequency / common repetition rate of the signal. **Harmonics** are integer multiples of the fundamental frequency. A complex image intensity profile (e.g., along a scanline) is approximated by adding these sinusoidal components; low frequencies capture broad smooth regions, high frequencies capture sharp edges and fine detail.

**(b)** 
- **Fourier Series:** periodic continuous-time signal → discrete harmonic coefficients.
- **Fourier Transform:** non-periodic continuous-time signal → continuous frequency spectrum.
- **DFT (Discrete Fourier Transform):** finite discrete samples → discrete frequency bins; the form used for digital images.

**(c)**
- **Low-pass filter:** attenuates high frequencies → smooths/blurs image, reduces noise, removes fine detail.
- **High-pass filter:** attenuates low frequencies → sharpens edges, enhances fine detail, amplifies noise.
- **Band-pass filter:** passes a middle frequency band → useful for texture or specific feature enhancement.

**(d) Frequency-domain workflow:**
1. Convert the spatial image to the frequency domain using the DFT → `F(u, v)`.
2. Apply a frequency-domain filter `H(u, v)` by multiplying: `G(u, v) = F(u, v) × H(u, v)`.
3. Apply the inverse DFT → enhanced spatial-domain image `g(x, y)`.

---

### IP — Mid Term Spring 2026, CSE 443 (page 7)

**Q2(a).** Discuss two limitations/failures of histogram equalization and how Adaptive Histogram Equalization (AHE) and CLAHE solve them. [10]

**Answer.**

**Marking scheme:** two limitations (4) + how AHE solves (3) + how CLAHE solves (3).

**Limitation 1 — Over-amplification of noise in nearly constant regions:** Global histogram equalization stretches the narrow histogram of a flat region, amplifying sensor noise and creating visible banding.
**Limitation 2 — One histogram for the whole image:** A single global transformation can over-change overall brightness or wash out local contrast, because it does not account for local image content.

**How AHE solves it:** AHE computes histogram equalization **locally** around each pixel (using a small neighborhood), so contrast is enhanced according to local content rather than one global histogram. This improves local contrast but can over-amplify noise in homogeneous areas.

**How CLAHE solves it:** **Contrast Limited Adaptive Histogram Equalization** clips the histogram at a predefined threshold before redistribution. The clipped excess is redistributed uniformly, which limits noise amplification while retaining local contrast enhancement. CLAHE is therefore preferred for medical and low-contrast images.

**Lecture link:** Lectures 7–8 — intensity transformations, histogram equalization, gamma correction, sRGB; Lecture Notes — histogram equalization limitations.
