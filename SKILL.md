---
name: take-a-peek
description: >-
  Enforces a 'Preview-First, Zero-Waste' workflow across two major generative domains:
  1) AI Image Generation: Prioritizes generating draft images without providing an API key
     (using free-ai-image-generator / Puter.js models) to protect quota-limited tools like generate_image (Imagen).
  2) Complex Tasks (CAD standard annotations, multi-page PDF compilation, large document rendering):
     Mandates producing lightweight thumbnail drafts (thumb_*.jpg) or layout wireframes first.
  Halts for explicit user approval before calling expensive tools or compiling full deliverables.
---

# take-a-peek: Draft-First & Quota-Protected Workflow

## 1. Core Principles
1. **Quota Protection (AI Images)**: Imagen and production AI image tools have strict quota caps. Never burn credits on unverified prompts. Always generate a zero-cost draft first without providing an API key, let the user "take a peek", and only generate final artwork upon approval.
2. **Prevent Rework (CAD & PDF Layouts)**: Never directly generate full-size 4K images or compile multi-page PDFs without review. Always produce a lightweight `thumb_*.jpg` preview first to verify text alignment, leader lines, and formatting.

## 2. Standard Protocols by Task Domain

### Domain A: AI Image Generation
- **Drafting (Zero Quota)**:
  - Do NOT call `generate_image` (Imagen) on initial request.
  - Priority: Use `free-ai-image-generator` (works completely without providing an API key via Puter.js) to generate free draft images.
  - Include prompt, style, and composition rationale.
- **Approval Gate**:
  - Halt. Ask: "Here is the free draft image. Does this composition meet your expectations?"
  - Wait for explicit user confirmation.
- **Production Generation**:
  - Call `generate_image` (Imagen) only after explicit user approval.

### Domain B: CAD Annotations & Multi-page PDF Compilation
- **Drafting (Lightweight Thumbnails)**:
  - Do NOT compile full multi-megabyte PDFs or export only full-scale raw drawings on the first attempt.
  - Generate a lightweight thumbnail preview: width 800~1200px, `.jpg` format, prefixed with `thumb_` (file size < 200KB).
  - Present the thumbnail in chat for immediate inspection of text legibility and leader line clarity.
- **Approval Gate**:
  - Halt. Ask the user for confirmation (e.g. "满意继续").
  - Do NOT proceed to full compilation or subsequent sheets without user sign-off.
- **Production Generation**:
  - Upon user approval, render full-resolution lossless PNGs or compile the formal PDF document.
  - At the end of the turn, offer a convenient 1-click option to clean up `thumb_*` cache files.
