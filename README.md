# Pack - Alternative Extension Store for Chrome

🚀 **Pack** is a revolutionary Chrome extension that serves as an alternative extension store, allowing you to install and run extensions that bypass Manifest V3 restrictions through advanced sandboxing technology.

## 🌟 Features

### 🔥 Core Features
- **Alternative Extension Store** - Browse and install extensions from our curated store
- **Manifest V3 Bypass** - Run Manifest V2 extensions (like uBlock Origin) in a sandboxed environment
- **Advanced Sandboxing** - Isolate extensions in secure containers while maintaining full functionality
- **GitHub & Discord Integration** - Login and upload extensions with OAuth authentication
- **Pack Format** - Convert any Chrome/Firefox extension to the optimized `.pack` format
- **Enhanced Privacy** - Extensions run in isolated environments with enhanced security

### 🛡️ Security & Privacy
- **Sandboxed Execution** - Extensions run in isolated iframes with controlled API access
- **Permission Control** - Fine-grained permission management for each extension
- **Local Processing** - Many operations happen locally to protect your data
- **Manifest V2 Support** - Run older, more powerful extensions safely

### 🎨 User Experience
- **Beautiful Animated UI** - Modern, glassmorphism design with smooth animations
- **Real-time Search** - Instantly find extensions with advanced filtering
- **Installation Progress** - Visual feedback during extension installation
- **Extension Management** - Easy install, uninstall, and configuration

## 📦 Installation

### Method 1: Download from GitHub (Recommended)
1. Go to [6em/pack](https://github.com/6em/pack) repository
2. Download the latest release
3. Extract the ZIP file
4. Open Chrome and go to `chrome://extensions/`
5. Enable "Developer mode"
6. Click "Load unpacked" and select the extracted folder

### Method 2: Build from Source
```bash
git clone https://github.com/6em/pack.git
cd pack
npm install
npm run build
```

## 🔧 Converting Extensions to Pack Format

Pack includes a powerful Node.js converter that can transform any Chrome or Firefox extension into the optimized `.pack` format.

### Installation
```bash
npm install -g pack-converter
```

### Usage

#### Convert Extension to Pack
```bash
# Convert from ZIP file
pack-converter convert extension.zip -o extension.pack

# Convert from directory
pack-converter convert ./my-extension/ -o my-extension.pack

# Convert Firefox XPI
pack-converter convert addon.xpi -o addon.pack

# Convert with metadata
pack-converter convert extension.zip -a "Your Name" -d "Custom description"
```

#### Extract Pack File
```bash
pack-converter extract extension.pack ./output-directory
```

#### Validate Pack File
```bash
pack-converter validate extension.pack
```

### Supported Input Formats
- **Chrome Extensions** (`.zip`, `.crx`)
- **Firefox Add-ons** (`.xpi`)
- **Extension Directories**

## 🏗️ Architecture

### Core Components

1. **Main Extension** (`manifest.json`)
   - Manages the Pack store interface
   - Handles authentication and user management
   - Coordinates extension installations

2. **Background Script** (`background.js`)
   - Manages sandboxed extension instances
   - Handles OAuth authentication
   - Processes extension installations and conversions

3. **Content Script** (`content.js`)
   - Injects Pack runtime into web pages
   - Manages extension sandboxes
   - Provides Chrome API emulation

4. **Pack Converter** (`pack-converter.js`)
   - Converts extensions to Pack format
   - Validates and extracts Pack files
   - Handles manifest version conversions

### Sandboxing Technology

Pack uses advanced sandboxing to run extensions safely:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Main Page     │    │  Pack Runtime   │    │  Sandboxed Ext  │
│                 │    │                 │    │                 │
│  ┌───────────┐  │    │  ┌───────────┐  │    │  ┌───────────┐  │
│  │ Content   │──┼────┼──│ API Proxy │──┼────┼──│ Extension │  │
│  │ Script    │  │    │  │           │  │    │  │ Code      │  │
│  └───────────┘  │    │  └───────────┘  │    │  └───────────┘  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🔌 Extension Store

The Pack store is powered by a JSON configuration file that defines available extensions:

### `extensions.json` Structure
```json
{
  "version": "1.0.0",
  "extensions": [
    {
      "id": "ublock-origin-pack",
      "name": "uBlock Origin (Pack Version)",
      "version": "1.54.0",
      "description": "Ad blocker with Manifest V3 bypass",
      "author": "Raymond Hill (Pack: Pack Team)",
      "downloadUrl": "https://github.com/6em/pack/releases/download/v1.0.0/ublock-origin-1.54.0.pack",
      "permissions": ["storage", "webRequest", "webRequestBlocking", "<all_urls>"],
      "pack_features": {
        "v3_bypass": true,
        "sandboxed": true,
        "enhanced_blocking": true
      }
    }
  ]
}
```

## 🚀 Development

### Prerequisites
- Node.js 16+
- Chrome/Chromium browser
- Git

### Setup Development Environment
```bash
# Clone the repository
git clone https://github.com/6em/pack.git
cd pack

# Install dependencies
npm install

# Install converter tool
cd converter
npm install
npm link

# Build extension
npm run build

# Watch for changes
npm run dev
```

### Project Structure
```
pack/
├── manifest.json          # Extension manifest
├── popup.html            # Store interface
├── popup.js             # Store functionality
├── background.js        # Background service worker
├── content.js          # Content script injector
├── sandbox.html        # Extension sandbox template
├── converter/          # Pack converter tool
│   ├── pack-converter.js
│   └── package.json
├── icons/             # Extension icons
├── extensions.json    # Store catalog
└── README.md
```

### Adding Extensions to the Store

1. **Convert Extension**
   ```bash
   pack-converter convert original-extension.zip -o new-extension.pack
   ```

2. **Upload to Releases**
   - Upload the `.pack` file to GitHub releases
   - Note the download URL

3. **Update Store Catalog**
   ```bash
   # Edit extensions.json
   {
     "id": "unique-extension-id",
     "name": "Extension Name",
     "downloadUrl": "https://github.com/6em/pack/releases/download/v1.0.0/extension.pack",
     ...
   }
   ```

4. **Test Installation**
   - Reload Pack extension
   - Search for your extension in the store
   - Test installation and functionality

## 🔐 Security Considerations

### Sandboxing Security
- Extensions run in isolated iframes with restricted DOM access
- API calls are proxied and validated
- No direct access to sensitive Chrome APIs
- Local storage isolation between extensions

### Pack File Integrity
- SHA-256 checksums for all extension files
- Digital signatures for verification
- Metadata validation during installation
- Secure conversion process

### Privacy Protection
- Extensions cannot access each other's data
- Limited cross-origin capabilities
- Optional offline mode for sensitive extensions
- User consent for all permissions

## 🤝 Contributing

We welcome contributions to Pack! Here's how you can help:

### Ways to Contribute
1. **Add Popular Extensions** - Convert and submit popular extensions
2. **Improve Sandboxing** - Enhance security and compatibility
3. **UI/UX Improvements** - Make the interface even better
4. **Bug Fixes** - Report and fix issues
5. **Documentation** - Improve guides and tutorials

### Contribution Process
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test thoroughly
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Guidelines
- Follow the existing code style
- Add tests for new features
- Update documentation as needed
- Ensure backward compatibility
- Test with multiple extensions

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Chrome Extension Developers** - For creating amazing extensions
- **uBlock Origin Team** - For inspiration on ad blocking technology
- **Mozilla** - For Firefox extension compatibility
- **Open Source Community** - For tools and libraries used

## 📞 Support

### Getting Help
- **GitHub Issues** - Report bugs and request features
- **Discussions** - General questions and community support
- **Discord** - Real-time chat with developers and users
- **Documentation** - Comprehensive guides and tutorials

### Known Issues
- Some Manifest V3 features may not be fully compatible
- Large extensions may take longer to load
- Limited support for native messaging
- Chrome Web Store extensions cannot be directly imported

### Roadmap
- [ ] Firefox support
- [ ] Extension sync across devices
- [ ] Advanced permission management
- [ ] Extension analytics and monitoring
- [ ] Community ratings and reviews
- [ ] Automated extension updates
- [ ] Pack extension development tools

---

**⚡ Pack - Empowering users with unrestricted extension capabilities while maintaining security and privacy.**
