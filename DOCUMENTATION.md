# Resizo Embed Widgets — Integration Documentation

> **Version:** 1.0 · **Last updated:** May 2026 · **Base URL:** `https://www.resizo.in`

Drop a free, privacy-first image tool into any website with a single `<iframe>`. No API key, no backend, no signup — every operation runs entirely in your visitor's browser.

---

## Table of Contents

1. [Quick Start](#1-quick-start)
2. [Available Widgets](#2-available-widgets)
3. [Embed URL Reference](#3-embed-url-reference)
4. [Configuration Options](#4-configuration-options)
5. [Theming](#5-theming)
6. [Auto-Resize (Dynamic Height)](#6-auto-resize-dynamic-height)
7. [Platform Integration Guides](#7-platform-integration-guides)
8. [Advanced Usage](#8-advanced-usage)
9. [Styling & Customization](#9-styling--customization)
10. [Security & Privacy](#10-security--privacy)
11. [Browser Compatibility](#11-browser-compatibility)
12. [Troubleshooting](#12-troubleshooting)
13. [FAQ](#13-faq)
14. [Changelog](#14-changelog)

---

## 1. Quick Start

Paste this snippet anywhere that accepts custom HTML — and you're done:

```html
<iframe
  src="https://www.resizo.in/embed/image-resizer/"
  width="100%"
  height="640"
  loading="lazy"
  title="Resizo — Image Resizer"
  style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
></iframe>
```

**That's it.** The widget loads, your visitors resize images, and nothing ever leaves their device.

### What just happened?

| Step | What happens |
| --- | --- |
| 1. Iframe loads | A lightweight HTML page (~5 KB) is fetched from `resizo.in`. |
| 2. Visitor drops an image | The file is read into memory using the browser's `FileReader` API. |
| 3. Processing runs locally | The Canvas API resizes / compresses / converts the image entirely in the browser tab. |
| 4. Download triggers | The result is offered via an `ObjectURL` download — no data leaves the device. |

---

## 2. Available Widgets

Resizo offers **6 embeddable tools**. Each has its own dedicated embed route.

| Widget | Embed Path | Description |
| --- | --- | --- |
| **Image Resizer** | `/embed/image-resizer/` | Resize images by exact pixel dimensions with aspect-ratio lock. |
| **JPG Compressor** | `/embed/compress-image/` | Shrink JPG, PNG, and WebP file sizes with a quality slider. |
| **WebP Converter** | `/embed/webp-converter/` | Convert PNG and JPG images to the modern WebP format. |
| **Passport Photo** | `/embed/passport-photo/` | Generate passport/visa photos to official specs (US, UK, India, EU, Canada, etc.). |
| **Batch Resize** | `/embed/batch-resize/` | Bulk-resize many images at once — results download as a ZIP. |
| **Watermark Tool** | `/embed/watermark/` | Add text watermarks to images with position, color, opacity, and rotation controls. |

### Embed Snippets for Every Widget

#### Image Resizer

```html
<iframe
  src="https://www.resizo.in/embed/image-resizer/"
  width="100%"
  height="640"
  loading="lazy"
  title="Resizo — Image Resizer"
  style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
></iframe>
```

#### JPG Compressor

```html
<iframe
  src="https://www.resizo.in/embed/compress-image/"
  width="100%"
  height="640"
  loading="lazy"
  title="Resizo — JPG Compressor"
  style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
></iframe>
```

#### WebP Converter

```html
<iframe
  src="https://www.resizo.in/embed/webp-converter/"
  width="100%"
  height="640"
  loading="lazy"
  title="Resizo — WebP Converter"
  style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
></iframe>
```

#### Passport Photo

```html
<iframe
  src="https://www.resizo.in/embed/passport-photo/"
  width="100%"
  height="700"
  loading="lazy"
  title="Resizo — Passport Photo Maker"
  style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
></iframe>
```

#### Batch Resize

```html
<iframe
  src="https://www.resizo.in/embed/batch-resize/"
  width="100%"
  height="700"
  loading="lazy"
  title="Resizo — Batch Resize"
  style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
></iframe>
```

#### Watermark Tool

```html
<iframe
  src="https://www.resizo.in/embed/watermark/"
  width="100%"
  height="700"
  loading="lazy"
  title="Resizo — Watermark Tool"
  style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
></iframe>
```

---

## 3. Embed URL Reference

### URL Pattern

```
https://www.resizo.in/embed/{tool-id}/[?theme={light|dark}]
```

### URL Parameters

| Parameter | Values | Default | Description |
| --- | --- | --- | --- |
| `theme` | `light`, `dark` | `auto` | Forces a specific color theme. Omit the parameter to let the widget follow the visitor's system preference (`prefers-color-scheme`). |

### Examples

```
# Auto theme (follows system preference) — recommended
https://www.resizo.in/embed/image-resizer/

# Force light mode
https://www.resizo.in/embed/image-resizer/?theme=light

# Force dark mode
https://www.resizo.in/embed/compress-image/?theme=dark
```

---

## 4. Configuration Options

You can customize the embed via **iframe attributes** and **URL parameters**.

### Iframe Attributes

| Attribute | Recommended Value | Notes |
| --- | --- | --- |
| `width` | `"100%"` | Use `100%` to fill the parent container. Fixed widths like `"600"` work too. Minimum recommended: `320px`. |
| `height` | `"640"` | Height in pixels. Most tools work well between `600`–`700px`. The Passport Photo and Batch tools may need `700`–`800px`. |
| `loading` | `"lazy"` | Defers loading until the iframe scrolls into the viewport. Improves page performance. |
| `title` | `"Resizo — {Tool Name}"` | Required for accessibility. Screen readers announce this text. |
| `style` | See below | Controls borders, rounding, overflow. |
| `allow` | Not needed | No camera, mic, or geolocation permissions are used. |
| `sandbox` | **Do not add** | Sandbox restrictions will prevent file downloads. |

### Recommended Inline Styles

```css
border: none;            /* Remove the default iframe border */
border-radius: 12px;     /* Rounded corners to match the widget UI */
overflow: hidden;        /* Clip the content to the rounded corners */
display: block;          /* Remove inline spacing below the iframe */
max-width: 100%;         /* Prevent horizontal overflow on narrow screens */
```

### Height Recommendations by Tool

| Widget | Minimum Height | Recommended Height |
| --- | --- | --- |
| Image Resizer | `500px` | `640px` |
| JPG Compressor | `500px` | `640px` |
| WebP Converter | `500px` | `640px` |
| Passport Photo | `600px` | `700px` |
| Batch Resize | `600px` | `700px` |
| Watermark Tool | `600px` | `700px` |

---

## 5. Theming

### Auto Theme (Default)

When you omit the `?theme=` parameter, the widget reads the visitor's `prefers-color-scheme` media query. If the visitor has their OS or browser set to dark mode, the widget renders in dark mode. Light OS? Light widget. No extra code needed.

```html
<!-- Auto theme — just omit the parameter -->
<iframe src="https://www.resizo.in/embed/image-resizer/" ...></iframe>
```

### Force Light Mode

```html
<iframe src="https://www.resizo.in/embed/image-resizer/?theme=light" ...></iframe>
```

### Force Dark Mode

```html
<iframe src="https://www.resizo.in/embed/image-resizer/?theme=dark" ...></iframe>
```

### Theme Behavior Details

| Scenario | Behavior |
| --- | --- |
| No `?theme` param | Widget follows `prefers-color-scheme`. Changes dynamically if the OS theme changes mid-session. |
| `?theme=light` | Widget is always light, regardless of OS preference. |
| `?theme=dark` | Widget is always dark, regardless of OS preference. |
| Visitor toggles the sun/moon icon inside the widget | Overrides the current theme for that session only. Does not persist across page reloads. |

### Design Tokens

The widget uses CSS custom properties internally. Here are the key tokens:

| Token | Light Value | Dark Value |
| --- | --- | --- |
| `--bg` | `#ffffff` | `#0a0e1a` |
| `--surface` | `#f8fafc` | `#0f172a` |
| `--border` | `#e2e8f0` | `#1e293b` |
| `--text` | `#0f172a` | `#f1f5f9` |
| `--brand` | `#1B70E0` | `#3b8eff` |

---

## 6. Auto-Resize (Dynamic Height)

By default, an iframe has a fixed height — which can cause internal scrollbars if the widget content grows (e.g., after an image is loaded and controls expand). Resizo widgets solve this by posting their content height to the parent page.

### How It Works

The widget uses `window.postMessage` to send a message to the parent window every time its height changes:

```json
{
  "source": "resizo-embed",
  "type": "size",
  "height": 742
}
```

### Implementation

Add this listener to your page to auto-resize the iframe:

```html
<iframe
  id="resizo-widget"
  src="https://www.resizo.in/embed/image-resizer/"
  width="100%"
  height="640"
  loading="lazy"
  title="Resizo — Image Resizer"
  style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
></iframe>

<script>
  window.addEventListener('message', function (event) {
    // Only handle messages from Resizo embeds
    if (event.data && event.data.source === 'resizo-embed' && event.data.type === 'size') {
      var iframe = document.getElementById('resizo-widget');
      if (iframe) {
        iframe.style.height = event.data.height + 'px';
      }
    }
  });
</script>
```

### Multiple Widgets on One Page

If you have multiple Resizo iframes on the same page, use a more targeted approach:

```html
<iframe class="resizo-embed" src="https://www.resizo.in/embed/image-resizer/" ...></iframe>
<iframe class="resizo-embed" src="https://www.resizo.in/embed/compress-image/" ...></iframe>

<script>
  window.addEventListener('message', function (event) {
    if (event.data && event.data.source === 'resizo-embed' && event.data.type === 'size') {
      // Find the iframe that sent this message
      var iframes = document.querySelectorAll('.resizo-embed');
      for (var i = 0; i < iframes.length; i++) {
        if (iframes[i].contentWindow === event.source) {
          iframes[i].style.height = event.data.height + 'px';
          break;
        }
      }
    }
  });
</script>
```

---

## 7. Platform Integration Guides

### WordPress

**Method 1 — Custom HTML Block (Gutenberg)**

1. Open your post or page in the WordPress editor.
2. Click **+** → Search for **"Custom HTML"** → Add block.
3. Paste the iframe snippet.
4. Click **Preview** to verify.
5. Publish.

**Method 2 — Classic Editor**

1. Switch to the **"Text"** tab (not "Visual").
2. Paste the iframe snippet where you want the widget.
3. Switch back to "Visual" to confirm it renders.
4. Publish.

**Method 3 — Shortcode Plugin**

If your theme strips iframes, install a plugin like **"iframe"** or **"Advanced iFrame"** and use:

```
[iframe src="https://www.resizo.in/embed/image-resizer/" width="100%" height="640" scrolling="no" frameborder="0"]
```

### Ghost

1. In the Ghost editor, click **+** → **HTML** card.
2. Paste the iframe snippet.
3. Publish.

### Webflow

1. Drag an **Embed** element into your layout.
2. Paste the iframe snippet.
3. Adjust width in the Webflow style panel if needed.
4. Publish.

### Wix

1. Go to **Add** → **Embed Code** → **Embed HTML**.
2. Paste the iframe snippet in the code editor.
3. Resize the container to fit your design.
4. Publish.

### Squarespace

1. Add a **Code Block** to your page.
2. Paste the iframe snippet.
3. Uncheck "Display Source" if shown.
4. Save.

### Notion

1. Type `/embed` and select **Embed**.
2. Paste the direct embed URL: `https://www.resizo.in/embed/image-resizer/`
3. Notion will render it in an iframe automatically.
4. Resize the block as needed.

### Substack

1. In the post editor, click **+** → **Embed**.
2. Paste the direct embed URL.
3. If that doesn't render, use the **Code Block** option and paste the full iframe snippet.

### Shopify (Online Store)

1. Go to **Online Store** → **Pages** → Edit your page.
2. Click **"<>"** (Show HTML) in the rich text editor.
3. Paste the iframe snippet.
4. Save.

### HTML / Static Sites

Just paste the iframe snippet directly into your HTML file. No build step, no dependencies.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Image Tools</title>
</head>
<body>
  <h1>Resize Your Images</h1>
  <iframe
    src="https://www.resizo.in/embed/image-resizer/"
    width="100%"
    height="640"
    loading="lazy"
    title="Resizo — Image Resizer"
    style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
  ></iframe>
</body>
</html>
```

### React / Next.js

```jsx
export default function ImageResizer() {
  return (
    <iframe
      src="https://www.resizo.in/embed/image-resizer/"
      width="100%"
      height={640}
      loading="lazy"
      title="Resizo — Image Resizer"
      style={{
        border: 'none',
        borderRadius: '12px',
        overflow: 'hidden',
        display: 'block',
        maxWidth: '100%',
      }}
    />
  );
}
```

**With auto-resize (React hook):**

```jsx
import { useEffect, useRef } from 'react';

export default function ResizoEmbed({ tool = 'image-resizer', theme }) {
  const iframeRef = useRef(null);

  useEffect(() => {
    function handleMessage(event) {
      if (
        event.data?.source === 'resizo-embed' &&
        event.data?.type === 'size' &&
        iframeRef.current?.contentWindow === event.source
      ) {
        iframeRef.current.style.height = `${event.data.height}px`;
      }
    }
    window.addEventListener('message', handleMessage);
    return () => window.removeEventListener('message', handleMessage);
  }, []);

  const src = `https://www.resizo.in/embed/${tool}/${theme ? `?theme=${theme}` : ''}`;

  return (
    <iframe
      ref={iframeRef}
      src={src}
      width="100%"
      height={640}
      loading="lazy"
      title={`Resizo — ${tool}`}
      style={{
        border: 'none',
        borderRadius: '12px',
        overflow: 'hidden',
        display: 'block',
        maxWidth: '100%',
      }}
    />
  );
}

// Usage:
// <ResizoEmbed tool="image-resizer" />
// <ResizoEmbed tool="compress-image" theme="dark" />
```

### Vue.js

```vue
<template>
  <iframe
    ref="iframe"
    :src="embedSrc"
    width="100%"
    :height="height"
    loading="lazy"
    :title="`Resizo — ${tool}`"
    :style="iframeStyle"
  />
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue';

const props = defineProps({
  tool: { type: String, default: 'image-resizer' },
  theme: { type: String, default: null },
});

const iframe = ref(null);
const height = ref(640);

const embedSrc = computed(() => {
  const base = `https://www.resizo.in/embed/${props.tool}/`;
  return props.theme ? `${base}?theme=${props.theme}` : base;
});

const iframeStyle = {
  border: 'none',
  borderRadius: '12px',
  overflow: 'hidden',
  display: 'block',
  maxWidth: '100%',
};

function handleMessage(event) {
  if (
    event.data?.source === 'resizo-embed' &&
    event.data?.type === 'size' &&
    iframe.value?.contentWindow === event.source
  ) {
    height.value = event.data.height;
  }
}

onMounted(() => window.addEventListener('message', handleMessage));
onBeforeUnmount(() => window.removeEventListener('message', handleMessage));
</script>

<!-- Usage: <ResizoEmbed tool="webp-converter" theme="dark" /> -->
```

### Angular

```typescript
// resizo-embed.component.ts
import { Component, Input, ElementRef, ViewChild, OnInit, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-resizo-embed',
  template: `
    <iframe
      #resizoIframe
      [src]="safeUrl"
      width="100%"
      [height]="height"
      loading="lazy"
      [title]="'Resizo — ' + tool"
      [style]="iframeStyle"
    ></iframe>
  `,
})
export class ResizoEmbedComponent implements OnInit, OnDestroy {
  @Input() tool = 'image-resizer';
  @Input() theme: 'light' | 'dark' | null = null;
  @ViewChild('resizoIframe') iframe!: ElementRef<HTMLIFrameElement>;

  height = 640;
  iframeStyle = 'border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%';

  private listener = (event: MessageEvent) => {
    if (
      event.data?.source === 'resizo-embed' &&
      event.data?.type === 'size' &&
      this.iframe?.nativeElement?.contentWindow === event.source
    ) {
      this.height = event.data.height;
    }
  };

  get safeUrl(): string {
    const base = `https://www.resizo.in/embed/${this.tool}/`;
    return this.theme ? `${base}?theme=${this.theme}` : base;
  }

  ngOnInit() {
    window.addEventListener('message', this.listener);
  }
  ngOnDestroy() {
    window.removeEventListener('message', this.listener);
  }
}

// Usage: <app-resizo-embed tool="compress-image" theme="dark" />
```

---

## 8. Advanced Usage

### Lazy Loading

Use the `loading="lazy"` attribute so the browser defers fetching the widget until it scrolls into view. This is the default in the generated embed code and is recommended for below-the-fold placements.

```html
<iframe ... loading="lazy"></iframe>
```

### Responsive Container

Wrap the iframe in a responsive container for consistent aspect-ratio control:

```html
<div style="position:relative;width:100%;max-width:800px;margin:0 auto;">
  <iframe
    src="https://www.resizo.in/embed/image-resizer/"
    width="100%"
    height="640"
    loading="lazy"
    title="Resizo — Image Resizer"
    style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
  ></iframe>
</div>
```

### Loading Multiple Tools

You can embed multiple widgets on a single page — each is independent:

```html
<h2>Resize Images</h2>
<iframe src="https://www.resizo.in/embed/image-resizer/" width="100%" height="640" loading="lazy" title="Resizo — Image Resizer" style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;margin-bottom:2rem;"></iframe>

<h2>Compress Images</h2>
<iframe src="https://www.resizo.in/embed/compress-image/" width="100%" height="640" loading="lazy" title="Resizo — JPG Compressor" style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"></iframe>
```

### Tab / Accordion Pattern

Show one tool at a time with tabs — only render the active iframe to save resources:

```html
<div id="tool-tabs">
  <button onclick="showTool('image-resizer')" class="active">Resizer</button>
  <button onclick="showTool('compress-image')">Compressor</button>
  <button onclick="showTool('webp-converter')">WebP Converter</button>
</div>

<iframe
  id="resizo-tool"
  src="https://www.resizo.in/embed/image-resizer/"
  width="100%"
  height="640"
  loading="lazy"
  title="Resizo Tool"
  style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;"
></iframe>

<script>
  function showTool(toolId) {
    document.getElementById('resizo-tool').src =
      'https://www.resizo.in/embed/' + toolId + '/';
  }
</script>
```

---

## 9. Styling & Customization

### Removing Rounded Corners

```html
<iframe ... style="border:none;overflow:hidden;display:block;max-width:100%;"></iframe>
```

### Adding a Shadow

```html
<iframe ... style="border:none;border-radius:12px;overflow:hidden;display:block;max-width:100%;box-shadow:0 4px 24px rgba(0,0,0,0.12);"></iframe>
```

### Adding a Border

```html
<iframe ... style="border:1px solid #e2e8f0;border-radius:12px;overflow:hidden;display:block;max-width:100%;"></iframe>
```

### Centering the Widget

```html
<div style="max-width:700px;margin:0 auto;">
  <iframe ... width="100%" height="640"></iframe>
</div>
```

### Full-Width (Edge-to-Edge)

```html
<iframe ... width="100%" height="640" style="border:none;display:block;"></iframe>
```

---

## 10. Security & Privacy

### Client-Side Architecture

Every Resizo embed widget processes images **entirely inside the visitor's browser**. Here's what that means:

| Concern | Answer |
| --- | --- |
| **Are images uploaded?** | No. The file is read with `FileReader` and drawn on an in-memory `<canvas>`. |
| **Does Resizo see filenames or dimensions?** | No. No telemetry about file content, names, or metadata is transmitted. |
| **Is it GDPR-compliant?** | By design — no personal data (images) are collected, processed, or stored on any server. |
| **Is it CCPA-compliant?** | Yes — same rationale. No consumer data is sold or shared. |
| **Does it work offline?** | After the first load, yes. The widget functions fully with the network disconnected. |
| **Can I verify this?** | Open DevTools → Network tab. You'll see zero requests during image processing. All code is visible in the page source. |

### Content Security Policy (CSP)

If your site uses a strict CSP, add these directives:

```
frame-src https://www.resizo.in;
```

If you also need the widget to post height messages to your page:

```
frame-src https://www.resizo.in;
```

The `postMessage` API does not require additional CSP rules — it's permitted by default on modern browsers.

### Sandboxing Warning

> **⚠️ Do NOT add `sandbox` to the iframe.**
>
> The `sandbox` attribute restricts downloads and file uploads — both of which are essential for the widget to function. If you must sandbox, use:
>
> ```html
> sandbox="allow-scripts allow-same-origin allow-downloads allow-forms"
> ```
>
> But the simplest and safest approach is to omit `sandbox` entirely.

---

## 11. Browser Compatibility

| Browser | Minimum Version | Notes |
| --- | --- | --- |
| Chrome | 80+ | Full support including WebP export. |
| Firefox | 78+ | Full support. |
| Safari | 14+ | Full support including WebP (added in Safari 14). |
| Edge | 80+ | Full support (Chromium-based). |
| Samsung Internet | 13+ | Full support. |
| Opera | 67+ | Full support. |
| iOS Safari | 14+ | Touch-friendly. File picker opens camera roll. |
| Chrome Android | 80+ | Touch-friendly. File picker opens camera/gallery. |

### Requirements

- **JavaScript must be enabled** — the widgets are vanilla JS applications.
- **No third-party dependencies** — no React, no jQuery, no external tracking SDKs.
- **No cookies** — the widgets do not set any cookies.

---

## 12. Troubleshooting

### Widget shows a blank white/black box

| Possible Cause | Fix |
| --- | --- |
| CSP blocking the iframe | Add `frame-src https://www.resizo.in;` to your Content Security Policy. |
| `sandbox` attribute present | Remove the `sandbox` attribute from the iframe or add the required permissions. |
| JavaScript disabled | Ensure JS is enabled in the browser. |
| Ad blocker interference | Some aggressive ad blockers may flag iframes. Add `resizo.in` to the whitelist. |

### File download doesn't work inside the widget

| Possible Cause | Fix |
| --- | --- |
| `sandbox` attribute too restrictive | Remove `sandbox` or ensure `allow-downloads` is included. |
| iOS "Open in new tab" behavior | This is an iOS Safari limitation. The file will open in a new tab — the user can long-press to save. |

### Widget has internal scrollbars

| Possible Cause | Fix |
| --- | --- |
| `height` too small | Increase the iframe height. See the [Height Recommendations](#height-recommendations-by-tool) table. |
| Content expanded after image load | Implement the [Auto-Resize listener](#6-auto-resize-dynamic-height) to dynamically adjust height. |

### Widget looks different from my site's theme

| Possible Cause | Fix |
| --- | --- |
| No `?theme` parameter set | The widget defaults to `auto` (system preference). Pin it with `?theme=light` or `?theme=dark`. |
| Visitor's OS preference differs | Use `?theme=light` or `?theme=dark` to force a consistent look. |

### Embed doesn't appear in WordPress Visual Editor

| Possible Cause | Fix |
| --- | --- |
| WordPress strips iframes in Visual mode | Switch to **Text/Code** mode and paste there. Or use a Custom HTML block in Gutenberg. |
| Security plugin blocks iframes | Whitelist `resizo.in` in your security plugin's iframe settings. |

### Console error: "Blocked a frame with origin…"

This is normal and harmless. It occurs when the auto-resize `postMessage` listener tries to access `event.source` but the iframe's origin doesn't match. The listener already guards against this — the message is simply ignored.

---

## 13. FAQ

### General

**Q: Is it really free?**
A: Yes. All 6 embed widgets are free to use on any website — personal, commercial, or enterprise. No API key, no usage limits, no pay walls.

**Q: Is there an attribution requirement?**
A: Each widget shows a small "Powered by Resizo" link in the footer. Please keep it visible — it's the only thing we ask in exchange for the free embed.

**Q: Can I remove the "Powered by Resizo" link?**
A: No. The attribution link must remain visible. This is a condition of the free embed license.

**Q: Will you add more widgets in the future?**
A: Yes. Planned widgets include a Crop tool, Format converter (multi-format), and a Background remover. Follow [@resizo](https://www.resizo.in/) for updates.

### Technical

**Q: Does the widget work on mobile?**
A: Yes. Every widget is touch-friendly and responsive down to ~320px wide. The drag-and-drop area accepts taps, and the file picker opens the camera roll on iOS and Android.

**Q: Can I control the widget programmatically from my page?**
A: The widget exposes limited control via `window.__embed` inside the iframe context, but cross-origin restrictions prevent direct access from the parent page. Use `postMessage` for communication. Currently, the widget only sends height data outward.

**Q: Does the embed affect my page's SEO?**
A: Minimally. The iframe content is served with `noindex, nofollow` meta tags, so search engines won't index the widget page or follow its links. The iframe itself doesn't affect your page's content indexing.

**Q: How large is the widget?**
A: Each widget is approximately 5–10 KB of HTML, CSS, and vanilla JS. The shared stylesheet (`embed.css`) is ~8 KB, and the shared script (`embed-base.js`) is ~2 KB. No heavy frameworks, no tracking SDKs.

**Q: Does it set cookies?**
A: No. The embed widgets do not set any cookies. Theme preference is handled via URL parameter and system preference detection.

**Q: Will the widget auto-update?**
A: Yes. Because the embed is loaded from `resizo.in` at render time, any improvements or bug fixes are deployed automatically. Your embed code doesn't need to change.

### Privacy

**Q: Do embedded widgets upload my visitors' images to a server?**
A: No. Each widget uses the browser's Canvas API to resize, compress, or convert images locally. Files never leave the device.

**Q: Is the embed GDPR-compliant?**
A: Yes. No image data, personal data, or tracking identifiers are collected or transmitted. The embed loads a static page — no cookies, no analytics SDKs, no server-side processing.

**Q: Can I use this on a healthcare / legal / government site?**
A: Yes. Since no data leaves the device, the widgets are suitable for environments with strict data-handling requirements. However, please consult your own compliance team for final approval.

---

## 14. Changelog

### v1.0 — May 2026

- Initial release of 6 embeddable widgets: Image Resizer, JPG Compressor, WebP Converter, Passport Photo, Batch Resize, Watermark Tool.
- Theme support: auto (system preference), light, dark.
- `postMessage`-based auto-resize.
- Responsive design down to 320px.
- Client-side processing — zero server uploads.

---

## Support

- **Embed generator (visual):** [resizo.in/embed/](https://www.resizo.in/embed/)
- **Contact:** [resizo.in/contact/](https://www.resizo.in/contact/)
- **Privacy Policy:** [resizo.in/privacy-policy/](https://www.resizo.in/privacy-policy/)
- **Terms:** [resizo.in/terms/](https://www.resizo.in/terms/)

---

<p align="center"><em>Built with ❤️ by <a href="https://www.resizo.in">Resizo</a> — Images never leave your device.</em></p>
