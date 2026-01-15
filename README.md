# 🕷️ DOM Data Collector

A powerful, browser-based data extraction tool that automatically collects phone numbers and email addresses from any webpage. Built with vanilla JavaScript, this tool runs directly in your browser console and provides a beautiful floating UI for real-time data collection.

![Version](https://img.shields.io/badge/version-2.1-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow)

<iframe src="https://player.vimeo.com/video/1154570746?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" width="400" height="300" frameborder="0" allow="autoplay; fullscreen; web-share" title="How Lead Collector Work"></iframe>

## ✨ Features

### 🔍 **Intelligent Data Extraction**
- **Phone Number Detection**: Automatically detects phone numbers in various formats:
  - International formats: `+91 9876543210`, `+1-800-555-0199`
  - National formats: `(555) 123-4567`, `98765 43210`
  - With country codes: `0091 9876543210`, `+44 20 7946 0958`
- **Email Extraction**: Captures all valid email addresses from the DOM
- **Smart Duplicate Prevention**: Prevents adding the same number even with different formatting

### 🎯 **Advanced Country Code Detection**
- Intelligent country code recognition with validation
- Supports 50+ country codes with proper national number length validation
- Prevents false positives (e.g., won't mistake a 10-digit local number as having a country code)

### 🔄 **Real-Time Collection**
- Auto-refresh every 2 seconds to catch dynamically loaded content
- Continuous monitoring of page changes
- Extracts from:
  - Page text content
  - `tel:` links (`<a href="tel:...">`)
  - `mailto:` links (`<a href="mailto:...">`)

### 💾 **Supabase Integration**
- **Secure Authentication**: Login with Supabase credentials
- **Auto-Sync**: Automatically syncs collected data to your Supabase database
- **Duplicate Detection**: Checks existing records before inserting
- **Visual Feedback**: Shows newly added vs. already existing records
- **Persistent Storage**: Credentials saved in localStorage for convenience

### 🎨 **Beautiful UI**
- Modern, dark-themed floating control panel
- Real-time statistics display
- Tabbed interface for phones and emails
- Export to JSON functionality
- Copy to clipboard feature
- Minimize/maximize controls

## 🚀 Quick Start

### Method 1: Using the Web Interface

1. **Open the HTML file** in your browser (`index1.html`)
2. **Login to Supabase** (optional):
   - Enter your Supabase REST URL
   - Enter your Anon Key (saved once)
   - Enter your email and password
   - Click "Login"
3. **Copy the Script**:
   - Click "Copy Script to Clipboard"
4. **Navigate to any webpage** you want to scrape
5. **Open Developer Tools** (`F12` or `Ctrl+Shift+I`)
6. **Go to Console tab**
7. **Paste and run** the script
8. **Start collecting** using the floating panel

### Method 2: Direct Console Usage

1. Copy the script from `index1.html`
2. Navigate to your target webpage
3. Open browser console
4. Paste and execute the script
5. Use the floating UI to collect data

## 📋 How It Works

### Data Collection Flow

```
Webpage → Script Injection → DOM Scanning → Pattern Matching → 
Data Normalization → Duplicate Check → Storage → UI Update
```

### Phone Number Processing

1. **Pattern Matching**: Uses multiple regex patterns to catch various formats
2. **Normalization**: Extracts digits and identifies country codes
3. **Validation**: Validates national number length based on country code
4. **Deduplication**: Checks normalized digits to prevent duplicates
5. **Storage**: Stores both formatted (for display) and normalized (for checking) versions

### Email Processing

1. **Pattern Matching**: Uses standard email regex
2. **Normalization**: Converts to lowercase and trims whitespace
3. **Deduplication**: Checks against existing emails
4. **Storage**: Stores in Set for O(1) lookup

## 🔧 Configuration

### Supabase Setup

1. **Create a Supabase Project** at [supabase.com](https://supabase.com)
2. **Create a Table**:
   ```sql
   CREATE TABLE data_collection (
     id BIGSERIAL PRIMARY KEY,
     phoneNumber TEXT,
     email TEXT,
     pageUrl TEXT,
     created_at TIMESTAMP DEFAULT NOW()
   );
   ```
3. **Enable RLS** (Row Level Security) if needed
4. **Get your credentials**:
   - REST URL: Found in Project Settings → API
   - Anon Key: Found in Project Settings → API

### Local Storage

The tool automatically saves:
- `supabaseUrl`: Your Supabase project URL
- `supabaseAnonKey`: Your anon/public key
- `supabaseToken`: Your authentication token (after login)
- `supabaseUser`: Your user information (after login)

## 📊 Export & Sync

### Export to JSON

Click the "Export" button in the floating UI to download collected data as JSON:

```json
{
  "phones": ["+91 9876543210", "555-123-4567"],
  "emails": ["info@example.com", "support@company.org"],
  "exportedAt": "2025-01-15T10:30:00.000Z",
  "source": "https://example.com"
}
```

### Sync to Supabase

1. **Export data** from the collector script
2. **Paste JSON** into the sync textarea
3. **Click "Sync to Supabase"**
4. **View results**:
   - ✅ Newly Added: Records successfully inserted
   - ℹ️ Already Exists: Records that were already in database

## 🛠️ Technical Details

### Technologies Used

- **Vanilla JavaScript**: No dependencies, runs anywhere
- **Tailwind CSS**: Modern, responsive styling
- **Font Awesome**: Beautiful icons
- **Supabase**: Backend database and authentication
- **localStorage API**: Client-side persistence

### Browser Compatibility

- ✅ Chrome/Edge (recommended)
- ✅ Firefox
- ✅ Safari
- ✅ Opera

### Performance

- **Lightweight**: ~50KB total (including UI)
- **Efficient**: Uses Set data structures for O(1) lookups
- **Non-blocking**: Runs asynchronously without freezing the page

## 🔒 Privacy & Security

- **Client-Side Only**: All data processing happens in your browser
- **No External Calls**: The collector script doesn't send data anywhere (unless you sync)
- **Secure Authentication**: Uses Supabase's secure auth system
- **Local Storage**: Credentials stored locally, never transmitted

## 📝 Use Cases

- **Lead Generation**: Extract contact information from directories
- **Market Research**: Collect business contact details
- **Data Migration**: Gather data for database migration
- **Competitor Analysis**: Extract contact information from competitor sites
- **Email List Building**: Collect email addresses for marketing (with consent)

## ⚠️ Important Notes

1. **Respect Terms of Service**: Always check website ToS before scraping
2. **Rate Limiting**: Be mindful of request frequency
3. **Legal Compliance**: Ensure you have permission to collect data
4. **GDPR/Privacy**: Respect privacy regulations when collecting personal data
5. **Ethical Use**: Use responsibly and ethically

## 🐛 Troubleshooting

### Script Not Working
- Ensure JavaScript is enabled
- Check browser console for errors
- Try refreshing the page

### Supabase Sync Failing
- Verify your credentials are correct
- Check Supabase dashboard for API errors
- Ensure table exists and RLS policies allow access

### Duplicate Numbers Being Added
- The tool normalizes numbers for duplicate checking
- If duplicates appear, they may have different formatting that wasn't normalized
- Check the normalized digits in the code

## 🎯 Future Enhancements

- [ ] Support for more data types (addresses, social media links)
- [ ] Custom regex pattern support
- [ ] Batch export options (CSV, Excel)
- [ ] Scheduled syncing
- [ ] Data filtering and search
- [ ] Analytics dashboard

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 👨‍💻 Author

**Ronak Bokaria** ([@ronakjain2012](https://ronakjain2012.netlify.app))

- 🌐 [Portfolio](https://ronakjain2012.netlify.app)
- 💼 [LinkedIn](https://linkedin.com/in/ronakjain2012)
- 💻 [GitHub](https://github.com/ronakjain2012)

---

<div align="center">

**Made with ❤️ by [@ronakjain2012](https://ronakjain2012.netlify.app)**

⭐ Star this repo if you find it helpful!

</div>
