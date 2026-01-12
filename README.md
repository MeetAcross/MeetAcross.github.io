# 🌍 MeetAcross

**Connect Teams Across Time Zones**

A powerful, intuitive web application that helps you find the perfect meeting time across multiple time zones. No more mental math or timezone confusion!

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## 📋 Table of Contents

- [Features](#features)
- [Demo](#demo)
- [Quick Start](#quick-start)
- [Detailed Setup Guide](#detailed-setup-guide)
- [How It Works](#how-it-works)
- [Usage Instructions](#usage-instructions)
- [API Integration](#api-integration)
- [Customization](#customization)
- [Browser Support](#browser-support)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## ✨ Features

### Core Features
- **Multi-timezone Support**: Add unlimited attendees from 418+ time zones worldwide covering all countries and cities
- **Visual Timeline**: Color-coded 24-hour timeline showing working hours for each attendee
- **Smart Recommendations**: Algorithm finds the best meeting windows based on:
  - Working hours (9 AM - 5 PM local time)
  - Lunch breaks (12 PM - 1 PM)
  - Early/late hours (8-9 AM, 5-7 PM)
  - Night hours (avoid scheduling during sleep time)
  - Weekend detection and penalties
- **Direct Meeting Platform Integration**: 
  - 📹 **Google Meet** - Create meetings with OAuth authentication
  - 💼 **Microsoft Teams** - Create Teams meetings directly
  - 🎥 **Zoom** - Schedule Zoom meetings with one click
  - Organizer information capture (name, email, timezone)
  - Demo mode for testing without OAuth setup
- **Calendar Integration**: 
  - Google Calendar direct link generation
  - ICS file download for any calendar app (Outlook, Apple Calendar, etc.)
- **Responsive Design**: Works perfectly on desktop, tablet, and mobile devices
- **No Backend Required**: Pure client-side application - no server needed!

### User Experience
- 🎨 Beautiful gradient UI with Tailwind CSS
- 🔄 Smooth animations and transitions
- 📱 Mobile-friendly responsive layout
- 🎯 Intuitive drag-and-drop interface
- 💾 No data stored - complete privacy

## 🚀 Quick Start

### Option 1: Direct Browser Open (Simplest)

1. Download the `index.html` file
2. Double-click the file to open it in your default browser
3. Start adding attendees!

### Option 2: Local Web Server (Recommended for Development)

```bash
# If you have Python 3 installed:
python -m http.server 8000

# If you have Python 2:
python -m SimpleHTTPServer 8000

# If you have Node.js installed:
npx http-server

# If you have PHP installed:
php -S localhost:8000
```

Then open `http://localhost:8000/index.html` in your browser.

### Option 3: Deploy to Web Server

Upload the single HTML file to any web hosting service:
- GitHub Pages
- Netlify
- Vercel
- AWS S3
- Any traditional web host

## 📖 Detailed Setup Guide

### Prerequisites

**Required:**
- Modern web browser (Chrome 90+, Firefox 88+, Safari 14+, Edge 90+)
- Internet connection (for Tailwind CSS CDN)

**Optional (for development):**
- Text editor (VS Code, Sublime Text, Atom, etc.)
- Local web server (Python, Node.js, PHP, etc.)

### Step-by-Step Installation

#### 1. Download the Application

```bash
# Clone from repository
git clone https://github.com/MeetAcross/MeetAcross.github.io.git
cd MeetAcross.github.io

# Or simply download the HTML file directly
```

#### 2. Open in Browser

**Method A: Direct Open**
```bash
# On macOS
open index.html

# On Linux
xdg-open index.html

# On Windows
start index.html
```

**Method B: Using a Local Server**
```bash
# Python 3
python3 -m http.server 8000

# Then visit: http://localhost:8000/index.html
```

#### 3. Verify It's Working

You should see:
- A gradient blue background
- MeetAcross logo and header
- "Connect Teams Across Time Zones" tagline
- Input fields for adding attendees
- Date selector

If you see these elements, you're all set! 🎉

## 🔧 How It Works

### Architecture

```
index.html
├── HTML Structure
│   ├── Header Section (with MeetAcross logo)
│   ├── Attendee Input Form
│   ├── Date Selector
│   ├── Timeline Visualization
│   ├── Best Times Recommendations
│   └── Calendar Integration
├── CSS Styling (Tailwind CSS CDN)
│   ├── Responsive Grid Layout
│   ├── Color Coding System
│   └── Animations
└── JavaScript Logic
    ├── Timezone Management
    ├── Timeline Generation
    ├── Scoring Algorithm
    └── Calendar Export Functions
```

### The Scoring Algorithm

The application uses a smart scoring system to find optimal meeting times:

```javascript
// Scoring breakdown:
- Working hours (9 AM - 12 PM, 2 PM - 5 PM): +10 points per attendee
- Lunch time (12 PM - 1 PM): +3 points per attendee
- Early/Late hours (8-9 AM, 5-7 PM): +1 point per attendee
- Night hours (7 PM - 8 AM): -20 points per attendee
- Weekend meetings: -50 points total
```

The algorithm:
1. Generates all 24 possible hourly slots
2. Calculates local time for each attendee
3. Scores each time slot based on working hours
4. Sorts and presents top 5 options
5. Highlights the best option with a purple badge

### Color Coding System

| Color | Meaning | Hours (Local Time) |
|-------|---------|-------------------|
| 🟢 Green | Optimal working hours | 9 AM - 12 PM, 2 PM - 5 PM |
| 🔵 Blue | Lunch time | 12 PM - 1 PM |
| 🟡 Yellow | Early/Late but acceptable | 8-9 AM, 5-7 PM |
| 🔴 Red | Night hours (avoid) | 7 PM - 8 AM |
| ⬜ Gray | Weekend | Saturday/Sunday |

## 📚 Usage Instructions

### Setting Up Meeting Platforms

For direct meeting creation with Google Meet, Microsoft Teams, or Zoom, see our comprehensive [Meeting Platform Setup Guide](MEETING_PLATFORM_SETUP.md).

**Quick Setup Options:**
- **Demo Mode**: Test the interface without OAuth credentials
- **Production Mode**: Configure OAuth for real meeting creation

### Adding Attendees

1. **Enter Name**: Type the attendee's name (e.g., "John Smith")
2. **Select Timezone**: Choose from 418+ timezones worldwide
3. **Click "Add Attendee"**: The attendee appears in the list below
4. **Repeat**: Add as many attendees as needed

**Example:**
```
Name: Sarah Chen
Timezone: Asia/Hong_Kong
→ Click "Add Attendee"

Name: Michael Brown
Timezone: America/New_York
→ Click "Add Attendee"
```

### Generating the Timeline

1. **Select Date**: Choose your desired meeting date
   - Weekends are automatically detected
   - Defaults to today's date
2. **Click "Generate Timeline"**: View the 24-hour visualization
3. **Analyze**: Each row shows one attendee's local times

**Reading the Timeline:**
- Horizontal axis: UTC hours (00:00 to 23:00)
- Each cell shows: Local time for that attendee
- Hover over cells: See detailed time information

### Selecting a Meeting Time

1. **Review Recommendations**: Top 5 best times are shown
2. **Check Details**: Each option shows local time for all attendees
3. **Look for the Purple Badge**: "BEST" indicates the optimal choice
4. **Consider Scores**: Higher scores = better meeting times

### Scheduling the Meeting

#### Option A: Google Calendar

1. Enter meeting title (required)
2. Add description (optional)
3. Select a recommended time from dropdown
4. Click "Add to Google Calendar"
5. Google Calendar opens with pre-filled event
6. Review and save

#### Option B: Download ICS File

1. Enter meeting title (required)
2. Add description (optional)
3. Select a recommended time from dropdown
4. Click "Download .ics File"
5. Open the downloaded file with your calendar app:
   - **Outlook**: Double-click the .ics file
   - **Apple Calendar**: Double-click or drag to Calendar app
   - **Gmail**: Upload via Settings → Import & Export
   - **Thunderbird**: File → Import → Events

## 🔌 API Integration

### Current Implementation (No API Required)

The application currently uses **client-side only** functionality:
- JavaScript Date API for timezone calculations
- No external API calls needed
- 100% privacy - no data sent to servers

### Optional: Adding Calendar Platform APIs

You can enhance the application with direct API integration:

#### Google Calendar API

```javascript
// Add to <head>
<script src="https://apis.google.com/js/api.js"></script>

// Initialize Google Calendar API
function initGoogleCalendar() {
    gapi.load('client:auth2', function() {
        gapi.client.init({
            apiKey: 'YOUR_API_KEY',
            clientId: 'YOUR_CLIENT_ID',
            discoveryDocs: ["https://www.googleapis.com/discovery/v1/apis/calendar/v3/rest"],
            scope: "https://www.googleapis.com/auth/calendar.events"
        });
    });
}

// Create event directly
function createCalendarEvent(eventDetails) {
    gapi.client.calendar.events.insert({
        'calendarId': 'primary',
        'resource': eventDetails
    }).then(function(response) {
        console.log('Event created: ' + response.result.htmlLink);
    });
}
```

**Setup Steps:**
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project
3. Enable Google Calendar API
4. Create OAuth 2.0 credentials
5. Add authorized JavaScript origins
6. Replace `YOUR_API_KEY` and `YOUR_CLIENT_ID`

#### Microsoft Graph API (Outlook)

```javascript
// Add Microsoft Authentication Library
<script src="https://alcdn.msauth.net/browser/2.14.2/js/msal-browser.min.js"></script>

// Initialize MSAL
const msalConfig = {
    auth: {
        clientId: 'YOUR_CLIENT_ID',
        authority: 'https://login.microsoftonline.com/common',
        redirectUri: window.location.origin
    }
};

const msalInstance = new msal.PublicClientApplication(msalConfig);

// Create event
async function createOutlookEvent(eventDetails) {
    const account = msalInstance.getAllAccounts()[0];
    const response = await msalInstance.acquireTokenSilent({
        scopes: ['Calendars.ReadWrite'],
        account: account
    });
    
    const graphResponse = await fetch('https://graph.microsoft.com/v1.0/me/events', {
        method: 'POST',
        headers: {
            'Authorization': `Bearer ${response.accessToken}`,
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(eventDetails)
    });
    
    return await graphResponse.json();
}
```

**Setup Steps:**
1. Go to [Azure Portal](https://portal.azure.com/)
2. Register a new application
3. Add Microsoft Graph API permissions
4. Configure redirect URIs
5. Replace `YOUR_CLIENT_ID`

### Supported Timezones

The application includes **418 comprehensive timezones** covering all countries and cities worldwide:

**Complete Global Coverage:**
- **Africa**: 52 timezones including Cairo, Johannesburg, Lagos, Nairobi, and more
- **Americas**: 147 timezones covering North, Central, and South America
- **Antarctica**: 11 research station timezones
- **Arctic**: Longyearbyen
- **Asia**: 84 timezones including Dubai, Tokyo, Singapore, Hong Kong, and more
- **Atlantic**: 10 island and coastal timezones
- **Australia**: 11 timezones covering all territories
- **Europe**: 62 timezones covering all European countries
- **Indian Ocean**: 11 island timezones
- **Pacific**: 30 timezones covering Pacific islands and territories

**Major Cities and Countries Include:**
All capital cities, major metropolitan areas, and countries worldwide are represented.

### Adding More Timezones

To add additional timezones, edit the `populateTimezones()` function:

```javascript
function populateTimezones() {
    const timezones = [
        // ... existing timezones ...
        'Your/New_Timezone',  // Add here
        'Another/Timezone'    // Add here
    ];
    // ... rest of function
}
```

**Finding Valid Timezone Names:**
```javascript
// Run in browser console to see all available timezones:
console.log(Intl.supportedValuesOf('timeZone'));
```

## 🎨 Customization

### Changing Colors

Edit the Tailwind CSS classes in the HTML:

```html
<!-- Change primary color from indigo to purple -->
<button class="bg-purple-600 hover:bg-purple-700">

<!-- Change background gradient -->
<body class="bg-gradient-to-br from-purple-50 to-pink-100">

<!-- Change success color from green to teal -->
<button class="bg-teal-600 hover:bg-teal-700">
```

### Modifying Work Hours

Edit the `getHourColor()` function:

```javascript
function getHourColor(hour, isWeekend) {
    if (isWeekend) return 'bg-gray-200';
    if (hour >= 10 && hour < 13) return 'bg-green-400'; // Changed to 10 AM - 1 PM
    if (hour === 13 || hour === 14) return 'bg-blue-300'; // Changed lunch time
    if (hour >= 15 && hour < 18) return 'bg-green-400'; // Changed to 3 PM - 6 PM
    // ... rest of logic
}
```

### Adjusting Meeting Duration

By default, meetings are 1 hour. To change:

```javascript
// In createGoogleCalendarEvent() and downloadICS()
const endDate = new Date(startDate.getTime() + 120 * 60 * 1000); // 2 hours
```

### Custom Scoring Weights

Modify the scoring algorithm in `findBestMeetingWindows()`:

```javascript
// Change scoring values
if (localHour >= 9 && localHour < 12) {
    score += 15; // Increased from 10 (prioritize morning meetings)
} else if (localHour >= 14 && localHour < 17) {
    score += 8;  // Decreased from 10 (de-prioritize afternoon)
}
```

### Adding Your Logo

The application now uses the MeetAcross logo from Cloudinary. To customize:

```html
<!-- Update the logo source in the header -->
<img src="your-logo-url.png" alt="Your Logo" class="h-16 w-16 md:h-20 md:w-20 object-contain">
```

## 🌐 Browser Support

| Browser | Minimum Version | Status |
|---------|----------------|---------|
| Chrome | 90+ | ✅ Fully Supported |
| Firefox | 88+ | ✅ Fully Supported |
| Safari | 14+ | ✅ Fully Supported |
| Edge | 90+ | ✅ Fully Supported |
| Opera | 76+ | ✅ Fully Supported |
| Samsung Internet | 14+ | ✅ Fully Supported |
| IE 11 | N/A | ❌ Not Supported |

### Required Browser Features
- ES6 JavaScript support
- Intl.DateTimeFormat API
- CSS Grid and Flexbox
- Local Storage (optional)

## 🐛 Troubleshooting

### Common Issues

#### 1. Timezone Dropdown is Empty

**Problem**: The timezone selector shows no options.

**Solution**:
- Check internet connection (Tailwind CSS needs CDN access)
- Verify JavaScript is enabled in browser
- Check browser console for errors (F12)

#### 2. Timeline Not Generating

**Problem**: Clicking "Generate Timeline" does nothing.

**Solution**:
```javascript
// Check if attendees are added:
- Add at least one attendee first
- Ensure both name AND timezone are selected
- Verify date is selected
```

#### 3. Calendar Export Not Working

**Problem**: Google Calendar link or ICS download fails.

**Solution**:
- Ensure meeting title is filled
- Select a time from the dropdown
- Check pop-up blocker settings
- For ICS: Check browser download permissions

#### 4. Colors Not Showing Correctly

**Problem**: Timeline appears without colors or styling.

**Solution**:
- Check internet connection (Tailwind CSS CDN)
- Clear browser cache (Ctrl+Shift+Delete)
- Try a different browser
- Verify no ad blockers are interfering

#### 5. Incorrect Time Calculations

**Problem**: Times shown don't match expected values.

**Solution**:
- Verify correct timezone selected
- Check system date/time settings
- Consider daylight saving time transitions
- Test with known timezone combinations

### Debug Mode

Enable console logging for troubleshooting:

```javascript
// Add to script section
const DEBUG = true;

function debugLog(message, data) {
    if (DEBUG) {
        console.log(`[DEBUG] ${message}:`, data);
    }
}

// Use throughout code:
debugLog('Attendees added', attendees);
debugLog('Timeline generated', attendeeHours);
```

### Getting Help

If you encounter issues:

1. **Check Browser Console**: Press F12 and look for errors
2. **Verify Prerequisites**: Ensure modern browser and internet connection
3. **Test in Different Browser**: Rule out browser-specific issues
4. **Clear Cache**: Sometimes old files cause problems
5. **Create an Issue**: Report bugs with:
   - Browser and version
   - Steps to reproduce
   - Console error messages
   - Screenshots

## 🚢 Deployment Options

### 1. GitHub Pages (Free)

```bash
# Create repository
git init
git add index.html
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/MeetAcross/MeetAcross.github.io.git
git push -u origin main

# Enable GitHub Pages
# Go to Settings → Pages → Source: main branch → Save
# Access at: https://meetacross.github.io/
```

### 2. Netlify (Free)

1. Drag and drop the HTML file to [Netlify Drop](https://app.netlify.com/drop)
2. Your site is instantly live!
3. Optional: Connect to Git repository for continuous deployment

### 3. Vercel (Free)

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
vercel

# Follow prompts and your site is live!
```

### 4. AWS S3 + CloudFront

```bash
# Create S3 bucket
aws s3 mb s3://meetacross

# Enable static website hosting
aws s3 website s3://meetacross --index-document index.html

# Upload file
aws s3 cp index.html s3://meetacross/ --acl public-read

# Optional: Set up CloudFront for CDN
```

### 5. Traditional Web Hosting

Simply upload via FTP/SFTP to any web host:
- GoDaddy
- Bluehost
- HostGator
- DreamHost
- Any shared hosting provider

## 📊 Performance Optimization

### Current Performance
- **Load Time**: < 1 second
- **File Size**: ~30 KB (single HTML file with comprehensive timezone support)
- **Dependencies**: Tailwind CSS CDN (~50 KB gzipped)

### Optimization Tips

#### 1. Self-Host Tailwind CSS

```html
<!-- Download Tailwind CSS and host locally -->
<link rel="stylesheet" href="tailwind.min.css">
```

#### 2. Minimize HTML

```bash
# Use HTML minifier
npm install -g html-minifier
html-minifier --collapse-whitespace --remove-comments index.html -o index.min.html
```

#### 3. Enable Compression

```apache
# .htaccess for Apache
<IfModule mod_deflate.c>
    AddOutputFilterByType DEFLATE text/html text/css text/javascript application/javascript
</IfModule>
```

#### 4. Add Service Worker (PWA)

```javascript
// Add offline support
if ('serviceWorker' in navigator) {
    navigator.serviceWorker.register('/sw.js');
}
```

## 🔒 Security & Privacy

### Data Privacy
- ✅ **No data storage**: Everything runs in your browser
- ✅ **No tracking**: No analytics or cookies
- ✅ **No external calls**: Except calendar export (user-initiated)
- ✅ **Open source**: Code is transparent and auditable

### Security Best Practices

When deploying:
1. **Use HTTPS**: Always serve over secure connection
2. **CSP Headers**: Add Content Security Policy
3. **CORS**: Configure properly if adding APIs
4. **Input Validation**: Already implemented in code

## 🤝 Contributing

We welcome contributions! Here's how:

### Reporting Bugs

Create an issue with:
- Clear description
- Steps to reproduce
- Expected vs actual behavior
- Browser and version
- Screenshots if applicable

### Suggesting Features

Open an issue with:
- Feature description
- Use case / motivation
- Proposed implementation (optional)

### Code Contributions

1. Fork the repository
2. Create feature branch: `git checkout -b feature/amazing-feature`
3. Make changes and test thoroughly
4. Commit: `git commit -m 'Add amazing feature'`
5. Push: `git push origin feature/amazing-feature`
6. Open Pull Request

### Code Style

- Use 4 spaces for indentation
- Comment complex logic
- Follow existing naming conventions
- Test in multiple browsers

## 📄 License

MIT License

Copyright (c) 2025 Meeting Time Zone Coordinator

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

## 🙏 Acknowledgments

- **Tailwind CSS**: For the amazing utility-first CSS framework
- **Google Calendar API**: For calendar integration capabilities
- **IANA Time Zone Database**: For accurate timezone information (418 timezones supported)
- **MDN Web Docs**: For excellent JavaScript documentation
- **Cloudinary**: For reliable image hosting

## 📞 Support

- **Documentation**: [GitHub Issues](https://github.com/MeetAcross/MeetAcross.github.io/issues)
- **Discussions**: [GitHub Discussions](https://github.com/MeetAcross/MeetAcross.github.io/discussions)

## 🗺️ Roadmap

### Version 1.2 (Current - Meeting Platform Integration)
- [x] Direct meeting creation on Google Meet
- [x] Direct meeting creation on Microsoft Teams
- [x] Direct meeting creation on Zoom
- [x] Organizer information fields (name, email, timezone)
- [x] OAuth2 authentication flow
- [x] Demo mode for testing
- [x] Setup documentation

### Version 1.3 (Planned)
- [ ] Recurring meeting support
- [ ] More calendar integrations (Outlook Calendar, Apple Calendar)
- [ ] Multiple language support
- [ ] Mobile app (PWA)
- [ ] Meeting preferences per attendee

### Version 2.0 (Future)
- [ ] Backend integration option
- [ ] User accounts
- [ ] Meeting history
- [ ] Advanced analytics

## 📈 Changelog

### Version 1.2.0 (2026-01-12)
- Added direct meeting platform integration
- Integrated Google Meet with OAuth2 authentication
- Integrated Microsoft Teams with OAuth2 authentication
- Integrated Zoom with OAuth2 authentication
- Added organizer information capture (name, email, timezone)
- Added demo mode for testing without OAuth credentials
- Created comprehensive setup documentation
- Enhanced UI with platform connection cards
- Auto-detect and save organizer timezone

### Version 1.1.0 (2026-01-12)
- Added comprehensive global timezone support (418 timezones)
- Updated branding to "MeetAcross - Connect Teams Across Time Zones"
- Added MeetAcross logo and favicon
- Enhanced timezone coverage for all countries and cities worldwide

### Version 1.0.0 (2025-01-12)
- Initial release
- Multi-timezone support
- Visual timeline
- Smart recommendations
- Google Calendar integration
- ICS file export
- Responsive design

---

**Made with ❤️ for teams working across time zones**

Need help? Found a bug? Have a suggestion? Open an issue!
