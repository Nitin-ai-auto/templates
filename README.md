# Otto AI Templates

A clean, modular HTML template system with global components for building web pages quickly and efficiently.

## 🚀 Features

- **Component-Based Architecture**: Reusable header, footer, and CTA components
- **Webflow-Free**: Custom vanilla JavaScript implementation
- **Performance Optimized**: Async/defer script loading, minified CSS
- **Responsive Design**: Mobile-first approach with modern CSS
- **SEO Ready**: Proper meta tags and semantic HTML

## 📁 Project Structure

```
/Users/nitin/testing/
├── global-header/
│   └── header.html          # Global navigation header
├── global-cta/
│   └── cta.html            # Call-to-action section
├── global-footer/
│   └── footer.html         # Global footer with links
├── global-js/
│   └── scripts-optimized.html  # Optimized JavaScript
├── .vscode/
│   └── settings.json       # VS Code configuration
├── global.min.css          # Minified global styles (2.1MB)
├── global.purged.css       # Purged CSS (463KB)
├── template.html           # Clean base template
├── new.html               # Example page with components
├── TESTING_GUIDE.md       # Testing documentation
└── README.md              # This file
```

## 🎨 Components

### Global Header
- Responsive navigation with dropdowns
- Mobile menu support
- Sticky header on scroll

### Global CTA
- Dotted texture background pattern
- Customizable call-to-action section
- Responsive layout

### Global Footer
- Multi-column footer links
- Social media icons
- AI summary links (ChatGPT, Perplexity, Claude, Google, Grok)

## 🛠️ Usage

### Creating a New Page

1. **Copy the template:**
   ```bash
   cp template.html your-page.html
   ```

2. **Add your content** between the header and footer:
   ```html
   <body>
       <div id="global-header"></div>
       
       <!-- Your page content here -->
       <main>
           <h1>Your Page Title</h1>
           <p>Your content...</p>
       </main>
       
       <div id="global-cta"></div>
       <div id="global-footer"></div>
   </body>
   ```

3. **Run a local server** (required for component loading):
   ```bash
   python3 -m http.server 8000
   ```

4. **Open in browser:**
   ```
   http://localhost:8000/your-page.html
   ```

## 📝 Component Loading

Components are loaded dynamically using vanilla JavaScript:

```javascript
loadComponent('global-header', 'global-header/header.html');
loadComponent('global-cta', 'global-cta/cta.html');
loadComponent('global-footer', 'global-footer/footer.html');
```

**Note:** You must use a local server (not `file://`) due to CORS restrictions.

## 🎯 Key Features

### CSS
- **Global Styles**: `global.min.css` - Complete styling system
- **Dotted Background**: SVG texture pattern for CTA sections
- **Gradient Effects**: Conic gradient animations
- **Responsive**: Mobile-first breakpoints

### JavaScript
- **Navbar**: Sticky header, mobile menu, dropdowns
- **Component Loader**: Dynamic HTML component injection
- **Analytics**: Google Analytics, GTM, Facebook Pixel
- **Marketing**: LaunchList, Leadsy, FirstPromoter

## 🔧 Development

### Prerequisites
- Python 3 (for local server)
- Modern web browser
- Code editor (VS Code recommended)

### Local Development
```bash
# Navigate to project directory
cd /Users/nitin/testing

# Start local server
python3 -m http.server 8000

# Open browser
open http://localhost:8000/template.html
```

### Editing Components
1. Edit component files in their respective folders
2. Refresh browser to see changes
3. No build process required!

## 📦 Files

- **template.html** - Clean base template (11.7KB)
- **new.html** - Example page with content (97.7KB)
- **global.min.css** - All styles (2.1MB)
- **global.purged.css** - Optimized styles (463KB)

## 🌐 Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## 📄 License

This project is part of Otto AI's web infrastructure.

## 🤝 Contributing

1. Create a new branch
2. Make your changes
3. Test thoroughly
4. Submit a pull request

## 📞 Support

For issues or questions, contact: hello@joinotto.com

---

**Built with ❤️ by the Otto AI team**
