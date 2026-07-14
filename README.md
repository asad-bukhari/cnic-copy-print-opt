# CNIC Copy Generator

A single-page web application for generating optimized PDF layouts of CNIC (Computerized National Identity Card) copies for printing. Designed for Pakistani CNIC cards with optimized layout for A4/A5 paper sizes.

## Features

- **Add Multiple Customers** - Add multiple customers with name, copy count, and front/back CNIC images
- **Flexible Page Sizes** - Support for A4 (portrait) and A5 (landscape) paper sizes
- **Optimized Layout** - Automatically arranges 2 CNICs per page (front + back) for efficient printing
- **Drag & Drop Image Upload** - Easy drag-and-drop or click-to-upload for CNIC front/back images
- **Customer Management** - Add, remove, and track multiple customers with copy counts
- **PDF Generation** - Generates optimized PDF using jsPDF with automatic page duplication for double-sided printing
- **Real-time Stats** - Live counters for total customers and total copies
- **Responsive Design** - Works on desktop and mobile devices
- **Offline Capable** - Single HTML file with CDN dependency (jsPDF via CDN)

## Features Overview

| Feature | Description |
|---------|-------------|
| **Page Sizes** | A4 (210mm × 297mm, portrait) • A5 (148mm × 210mm, landscape) |
| **CNIC Dimensions** | 99.5mm × 68mm (standard Pakistani CNIC size) |
| **Layout** | 2 columns × dynamic rows per page |
| **Output** | PDF with pages duplicated for double-sided printing |
| **Max Copies per Customer** | 10 |
| **Image Formats** | JPEG, PNG, WebP (via browser FileReader) |

## Quick Start

1. **Download/Clone** this repository
2. **Open** `index.html` in any modern browser (Chrome, Firefox, Edge, Safari)
3. **Select** page size (A4 or A5)
4. **Add Customers**:
   - Enter customer name
   - Set number of copies (1-10)
   - Upload CNIC front image
   - Upload CNIC back image
   - Click "Add Customer"
5. **Generate PDF** - Click "Generate PDF" to download the optimized PDF

## Usage

### Adding Customers
1. Fill in the customer name (optional - auto-generates "Customer N")
2. Set number of copies needed (1-10)
3. Upload front and back images of the CNIC
4. Click "Add Customer"
5. Repeat for additional customers

### Generating PDF
1. Ensure at least one customer is added
2. Select page size (A4 or A5)
3. Click "Generate PDF"
4. PDF downloads automatically as `All_Customers_CNIC_Copies.pdf`

### Managing Customers
- **View Stats**: Total customers and total copies displayed in real-time
- **Remove Customer**: Click the red trash icon next to any customer
- **Reset All**: Click "Reset All" to clear all data

## Technical Details

### Architecture
- **Single HTML file** - No build step, no dependencies to install
- **Vanilla JavaScript** (ES6+) - No frameworks required
- **jsPDF v2.5.1** via CDN (cdnjs) for PDF generation
- **CSS Grid/Flexbox** for responsive layout
- **Vanilla JS modules** pattern (IIFE-style modules)

### CNIC Layout Calculation
```
CNIC Size: 99.5mm × 68mm → 282pt × 193pt (at 72 DPI)
Layout: 2 columns × dynamic rows per page
Margin: 10pt | Spacing: 10pt
```

**A4 Page** (595pt × 842pt): ~12 CNICs per page (6 front + 6 back)  
**A5 Page** (595pt × 420pt): ~6 CNICs per page (3 front + 3 back)

### PDF Output
- Each CNIC copy = 2 pages (front + back)
- Pages are duplicated for double-sided printing
- Output: `All_Customers_CNIC_Copies.pdf`

### Browser Support
- Chrome 60+
- Firefox 55+
- Safari 11+
- Edge 79+

Requires: `FileReader API`, `Canvas API`, `Blob/URL API`, `ES6 Modules`

## Project Structure

```
cnic-copy-print-opt/
├── index.html    # Main application (single-file)
└── README.md          # This file
```

## Development

No build step required. Simply edit `index.html` and open in browser.

### Code Structure (inside the HTML)
```javascript
CONFIG        // Configuration constants (page sizes, CNIC dims, layout)
ELEMENTS      // DOM element references
state         // Application state management
utils         // Utility functions (alerts, file reading, loading)
ui            // UI rendering and updates
customerManager // Customer CRUD operations
pdfGenerator  // PDF generation with jsPDF
initEventListeners // Event binding
```

### Key Constants (CONFIG)
```javascript
CONFIG = {
  PAGE_SIZES: {
    A4: { width: 595, height: 842, orientation: "portrait" },
    A5: { width: 595, height: 420, orientation: "landscape" }
  },
  CNIC: { MM: { width: 99.5, height: 68 } },
  LAYOUT: { MARGIN: 10, SPACING: 10, COLUMNS: 2 }
}
```

## Deployment

### GitHub Pages / Netlify / Vercel
1. Deploy `index.html` to any static hosting

### Local Network
Host via any static server:
```bash
# Python
python -m http.server 8000

# Node.js
npx serve

# PHP
php -S localhost:8000
```

## Browser Permissions

The app requires:
- **File Access** - For uploading CNIC images
- **Downloads** - For saving generated PDF

No camera/microphone/location permissions needed.

## Known Limitations

| Limitation | Details |
|------------|---------|
| **jsPDF CDN** | Requires internet on first load (cached after) |
| **Image Format** | Output PDF uses JPEG compression |
| **Large Batches** | Browser memory limits large PDFs (50+ customers) |
| **Mobile Safari** | PDF download may need "Allow Downloads" permission |

## Developer

**Asad Bukhari**  
📞 +92 349 159 0380

## License

MIT License - Free for personal and commercial use.

---

**Built for efficient CNIC copy printing in Pakistan** 🇵🇰