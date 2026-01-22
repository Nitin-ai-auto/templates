# How to Integrate Global Components (The Standard Process)

This guide provides a step-by-step standard operating procedure for adding global R2 assets (CSS, Header, Footer, CTA, JS) to **any new web page** in this project.

Follow these steps to ensure all components load visually and interactively without race conditions.

---

## Step 1: Add Global CSS
In the `<head>` of your HTML document, add the link to the global stylesheet. This ensures styles are available immediately before content renders.

```html
<head>
    <!-- ... meta tags ... -->
    
    <!-- 1. Global CSS -->
    <link rel="stylesheet" href="https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/css/global.min.css">
    
    <!-- ... other styles ... -->
</head>
```

## Step 2: Create Component Placeholders
In your `<body>`, add empty `<div>` containers with specific IDs. The JavaScript will look for these exact IDs to inject the HTML content.

**Required IDs:**
*   Header: `global-header`
*   CTA Section: `cta-container`
*   Footer: `footer-container`

```html
<body>
    <!-- 2. Header Placeholder -->
    <div id="global-header" class="ot-navbar"></div>

    <main>
        <!-- Your unique page content goes here -->
    </main>

    <!-- 2. CTA Placeholder -->
    <div id="cta-container"></div>
    
    <!-- 2. Footer Placeholder -->
    <div id="footer-container"></div>

    <!-- ... scripts follow ... -->
</body>
```

## Step 3: Add the Universal Loader Script
Copy and paste this exact script block at the very bottom of your `<body>` tag. This script handles:
1.  **Fetching** html content.
2.  **Sequencing** (Wait for HTML -> Then load JS).
3.  **Executing** scripts found inside the fetched HTML.

```html
<script>
    // Helper: Fetches and injects HTML into a target Div
    async function loadComponent(url, elementId) {
        try {
            const response = await fetch(url);
            if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
            const html = await response.text();
            const el = document.getElementById(elementId);
            if (el) el.innerHTML = html;
        } catch (error) {
            console.error('Error loading component:', url, error);
        }
    }

    // Helper: Fetches a script file, parses it, and re-injects scripts so they execute
    async function loadScripts(url) {
        try {
            const response = await fetch(url);
            if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
            const html = await response.text();

            // Create temp container to parse scripts
            const div = document.createElement('div');
            div.innerHTML = html;
            const scripts = div.querySelectorAll('script');

            // Re-create and append scripts to force execution
            for (const oldScript of scripts) {
                const newScript = document.createElement('script');
                Array.from(oldScript.attributes).forEach(attr => newScript.setAttribute(attr.name, attr.value));
                newScript.async = false; // Execute in order
                newScript.textContent = oldScript.textContent;
                document.body.appendChild(newScript);
            }
        } catch (error) {
            console.error('Error loading scripts:', url, error);
        }
    }

    // Main Execution Logic
    document.addEventListener('DOMContentLoaded', () => {
        // A. Load all Visual Components first (Parallel)
        Promise.all([
            loadComponent('https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/components/header.html', 'global-header'),
            loadComponent('https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/components/cta.html', 'cta-container'),
            loadComponent('https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/components/footer.html', 'footer-container')
        ]).then(() => {
            // B. ONLY after HTML is in place, load the global scripts
            loadScripts('https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/js/scripts.html');
        });
    });
</script>
```

## Summary of URLs Used
| Component | URL |
| :--- | :--- |
| **CSS** | `https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/css/global.min.css` |
| **JS** | `https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/js/scripts.html` |
| **Header** | `https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/components/header.html` |
| **Footer** | `https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/components/footer.html` |
| **CTA** | `https://pub-4045c43a30dd450b9e4b15e094bc8f07.r2.dev/components/cta.html` |
