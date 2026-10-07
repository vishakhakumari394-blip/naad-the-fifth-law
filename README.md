[README.md](https://github.com/user-attachments/files/33157427/README.md)
# NAAD — Noise Adaptive AI for Defence

**Team The Fifth Law · Smart India Hackathon 2026**

A hybrid AI-driven active noise cancellation (ANC) system for defence communication. It combines lightweight deep-learning speech enhancement (DeepFilterNet3) with real-time signal processing to suppress both continuous and sudden impulsive noise while preserving speech intelligibility, running fully on the edge.

**Live demo:** https://naad-the-fifth-law.onrender.com

## What this website shows

- **How NAAD works:** a scroll-driven animation that follows a speech waveform through STFT analysis, DeepFilterNet3 and post-processing. Click Play or scroll to trace the signal.
- **Live demo:** listen to a real ~0 dB SNR recording before and after enhancement. Switch between noisy and enhanced audio while it plays and compare their waveforms and spectrograms.
- **Pipeline, challenges vs solution, and hardware/software stack.**

The audio demo uses a pre-processed sample (`audio/noisy_0db.wav` and `audio/enhanced.wav`). The enhanced file is the output of our fine-tuned DeepFilterNet3 model. The website does not run the model live; it is a static presentation of our results.

## Signal pipeline

Audio capture → pre-processing and framing (resampling, pre-emphasis, framing, windowing, normalization) → STFT + ERB filterbank → DeepFilterNet3 (ERB features, encoder, temporal model, decoder, mask + filter coefficients) → post-processing (inverse STFT) → clear audio.

## Hardware and software

- **Hardware:** Raspberry Pi 5 (edge processing), USB or I2S microphone, speaker or headphones, optional USB sound card, 5V 3A power supply.
- **Software:** Python, PyTorch, Rust, with ONNX / TensorRT for edge deployment.

## Run the website locally

The site is plain HTML, CSS and JavaScript with no build step. Audio will not load when `index.html` is opened directly from disk, so use a local server:

```bash
git clone https://github.com/vishakhakumari394-blip/naad-the-fifth-law.git
cd naad-the-fifth-law
python3 -m http.server 8000
```

Then open http://localhost:8000.

## Project structure

```
index.html            the whole website
audio/                noisy and enhanced sample recordings
cleaned_clip1-5/      animation frames for the "How NAAD works" section
render.yaml           Render static-site configuration
```

## Deployment

Deployed as a static site on Render. Pushing to `main` redeploys automatically.


