# Meeting Platform Integration Setup Guide

This guide will help you configure the OAuth credentials for Google Meet, Microsoft Teams, and Zoom integrations in MeetAcross.

## Overview

MeetAcross now supports direct meeting creation on three major platforms:
- 📹 **Google Meet** - Create meetings with Google Calendar integration
- 💼 **Microsoft Teams** - Create Teams meetings with calendar integration
- 🎥 **Zoom** - Create Zoom meetings with scheduling

## Features

- **Organizer Information**: Capture meeting organizer's name, email, and timezone
- **OAuth Authentication**: Secure authentication with each platform
- **Direct Meeting Creation**: Create meetings directly on each platform with all attendee information
- **Demo Mode**: Test the interface without OAuth setup
- **Persistent Authentication**: Stay logged in across sessions

## Setup Instructions

### 1. Google Meet Integration

#### Step 1: Create Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Enable the **Google Calendar API**:
   - Go to "APIs & Services" → "Library"
   - Search for "Google Calendar API"
   - Click "Enable"

#### Step 2: Create OAuth 2.0 Credentials

1. Go to "APIs & Services" → "Credentials"
2. Click "Create Credentials" → "OAuth client ID"
3. Configure the consent screen if prompted:
   - User Type: External (or Internal for workspace)
   - Add app name, user support email, and developer contact
   - Add scopes: `https://www.googleapis.com/auth/calendar.events`
4. Create OAuth client ID:
   - Application type: Web application
   - Name: MeetAcross Google Meet Integration
   - Authorized redirect URIs: Add your domain (e.g., `https://yourdomain.com` or `http://localhost:8000` for testing)
5. Copy the **Client ID**

#### Step 3: Configure in MeetAcross

1. Open MeetAcross and scroll to the "Schedule Meeting" section
2. Click "Connect Google" under Google Meet
3. When prompted, paste your **Client ID**
4. For testing, you can use **Demo Mode** (click OK when asked)
5. For production, click Cancel and the app will redirect to Google for authentication

#### API Endpoints Used:
- Authentication: `https://accounts.google.com/o/oauth2/v2/auth`
- Calendar Events: `https://www.googleapis.com/calendar/v3/calendars/primary/events`

---

### 2. Microsoft Teams Integration

#### Step 1: Register Application in Azure

1. Go to [Azure Portal](https://portal.azure.com/)
2. Navigate to "Azure Active Directory" → "App registrations"
3. Click "New registration"
4. Configure:
   - Name: MeetAcross Teams Integration
   - Supported account types: Accounts in any organizational directory and personal Microsoft accounts
   - Redirect URI: Web, add your domain (e.g., `https://yourdomain.com`)

#### Step 2: Configure API Permissions

1. Go to your app → "API permissions"
2. Click "Add a permission" → "Microsoft Graph"
3. Add **Delegated permissions**:
   - `Calendars.ReadWrite` - Create and manage calendar events
   - `OnlineMeetings.ReadWrite` - Create Teams meetings
   - `offline_access` - Maintain access
4. Click "Grant admin consent" (if you have admin rights)

#### Step 3: Get Client ID

1. Go to "Overview" in your app registration
2. Copy the **Application (client) ID**

#### Step 4: Configure in MeetAcross

1. Open MeetAcross and scroll to the "Schedule Meeting" section
2. Click "Connect Teams" under Microsoft Teams
3. When prompted, paste your **Application (client) ID**
4. For testing, use **Demo Mode** (click OK when asked)
5. For production, click Cancel and the app will redirect to Microsoft for authentication

#### API Endpoints Used:
- Authentication: `https://login.microsoftonline.com/common/oauth2/v2.0/authorize`
- Create Event: `https://graph.microsoft.com/v1.0/me/events`

---

### 3. Zoom Integration

#### Step 1: Create Zoom App

1. Go to [Zoom App Marketplace](https://marketplace.zoom.us/)
2. Sign in and click "Develop" → "Build App"
3. Choose "OAuth" app type
4. Fill in app information:
   - App Name: MeetAcross Zoom Integration
   - Short Description: Create Zoom meetings from MeetAcross
   - Company Name: Your company
   - Developer Contact: Your email

#### Step 2: Configure OAuth

1. In "App Credentials" tab:
   - Copy the **Client ID** (you'll need this)
   - Add redirect URL: Your domain (e.g., `https://yourdomain.com`)
2. In "Scopes" tab, add:
   - `meeting:write` - Create meetings
   - `meeting:read` - Read meeting details
   - `user:read` - Read user profile

#### Step 3: Activate App

1. Complete all required information
2. Submit app for activation (or use in development mode)

#### Step 4: Configure in MeetAcross

1. Open MeetAcross and scroll to the "Schedule Meeting" section
2. Click "Connect Zoom" under Zoom
3. When prompted, paste your **Client ID**
4. For testing, use **Demo Mode** (click OK when asked)
5. For production, click Cancel and the app will redirect to Zoom for authentication

#### API Endpoints Used:
- Authentication: `https://zoom.us/oauth/authorize`
- Create Meeting: `https://api.zoom.us/v2/users/me/meetings`

---

## Usage

### Creating a Meeting

1. **Add Attendees**: Add all meeting participants with their timezones
2. **Generate Timeline**: Click "Generate Timeline" to see optimal meeting times
3. **Fill Organizer Information**:
   - Enter your name
   - Enter your email address
   - Select your timezone (auto-detected if available)
4. **Enter Meeting Details**:
   - Meeting title (required)
   - Description (optional)
   - Select recommended time
5. **Connect to Platform**: Click "Connect" button for your preferred platform
6. **Create Meeting**: Once connected, click the corresponding "Create" button

### Demo Mode vs Production

**Demo Mode** (For Testing):
- No OAuth credentials required
- Simulates authentication
- Generates sample meeting links
- Great for testing the interface
- Data is not actually sent to platforms

**Production Mode** (For Real Use):
- Requires OAuth credentials
- Real authentication with platforms
- Creates actual meetings
- Meetings appear in your calendar
- Attendees receive invitations

---

## Security Notes

1. **Never commit OAuth credentials** to version control
2. **Store credentials securely** - Use environment variables or secure storage
3. **Use HTTPS** in production - OAuth requires secure connections
4. **Regularly rotate credentials** - Update Client IDs/Secrets periodically
5. **Limit scope permissions** - Only request necessary permissions
6. **Review consent screens** - Ensure users understand what they're granting access to

---

## Troubleshooting

### "Authentication error" message
- **Solution**: Check that your redirect URI matches exactly in the OAuth app configuration
- Ensure your domain uses HTTPS in production

### "Please connect to [Platform] first" message
- **Solution**: Click the "Connect" button for the platform before trying to create a meeting
- If authentication failed, try disconnecting and reconnecting

### Meeting creation fails
- **Solution**: 
  - Verify all required fields are filled (organizer info, meeting title, time)
  - Check that your OAuth token hasn't expired (reconnect if needed)
  - Ensure you have proper API permissions configured

### "Invalid email address" error
- **Solution**: Enter a valid email in the organizer email field

### Can't see meeting in calendar
- **Production Mode**: Check that you granted calendar permissions
- **Demo Mode**: Demo meetings are not actually created

---

## Privacy & Data Handling

- **Organizer information** is saved in browser's localStorage for convenience
- **OAuth tokens** are stored locally and expire after the session
- **No data is sent to external servers** except during OAuth authentication
- **Meeting information** is only sent to the selected platform when creating a meeting
- All data stays in your browser and the platforms you choose

---

## Browser Support

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Opera 76+

---

## Server-Side Setup (Optional)

For production deployments, you may want to implement server-side token exchange for enhanced security:

### Node.js Example (Express)

```javascript
const express = require('express');
const axios = require('axios');
const app = express();

// Google OAuth token exchange
app.get('/auth/google/callback', async (req, res) => {
  const { code } = req.query;
  const response = await axios.post('https://oauth2.googleapis.com/token', {
    code,
    client_id: process.env.GOOGLE_CLIENT_ID,
    client_secret: process.env.GOOGLE_CLIENT_SECRET,
    redirect_uri: process.env.REDIRECT_URI,
    grant_type: 'authorization_code'
  });
  
  // Store token securely and redirect back to app
  res.redirect(`/?access_token=${response.data.access_token}`);
});

app.listen(3000);
```

---

## Support

For issues or questions:
1. Check this documentation first
2. Review platform-specific OAuth documentation
3. Open an issue on the MeetAcross GitHub repository

---

## License

This integration is part of MeetAcross and follows the same MIT License.
