# Women Safety System

A responsive web application designed for women safety in zero-network zones, featuring two separate interfaces: User Interface (Smart Safety Pole Simulation) and Admin Interface (Control Center Dashboard).

## 🚀 Features

### User Interface - Smart Safety Pole Simulation
- **Emergency Alert Button**: Large red panic/SOS button with 3-second long-press functionality
- **Visual Feedback**: Screen turns red when emergency is triggered
- **Push-to-Talk (PTT)**: Voice communication channel with Control Center (enabled after emergency trigger)
- **Status Indicators**: 
  - Network Status (Offline Mode - LoRa Simulated)
  - Pole ID
  - Location
  - Real-time timestamp
- **Offline Capability**: Simulates LoRa technology for zero-network zones

### Admin Interface - Control Center Dashboard
- **Real-Time Alert Panel**: 
  - Live alert monitoring with priority levels (High/Medium/Low)
  - Color-coded alerts (Red for High, Yellow for Medium, Gray for Low)
  - Time tracking and location information
- **Alert Aggregation**: Zone-based alert grouping with count display
- **Push-to-Talk Control**: Enable/disable voice communication with emergency poles
- **Response Actions**:
  - Notify Police
  - Notify Campus Security
  - Mark as Resolved
- **Alert History Logs**: Complete timestamped alert history with search capability

## 🎯 Technology Stack

- **Framework**: React 18 with TypeScript
- **UI Components**: shadcn/ui
- **Styling**: Tailwind CSS
- **Build Tool**: Vite
- **State Management**: React Hooks + Context API
- **Data Storage**: Browser localStorage
- **Real-time Sync**: CustomEvent API

## 📁 Project Structure

```
src/
├── components/
│   ├── admin/
│   │   ├── AlertPanel.tsx          # Real-time alert display
│   │   ├── AlertAggregation.tsx    # Zone-based alert grouping
│   │   ├── AlertHistory.tsx        # Alert logs
│   │   └── ActionButtons.tsx       # Response action buttons
│   ├── emergency/
│   │   ├── EmergencyButton.tsx     # Long-press panic button
│   │   ├── PTTButton.tsx           # Push-to-talk button
│   │   └── StatusIndicators.tsx    # Status display panel
│   └── ui/                         # shadcn/ui components
├── pages/
│   ├── UserInterface.tsx           # Smart Safety Pole page
│   └── AdminDashboard.tsx          # Control Center page
├── services/
│   └── alertService.ts             # Alert management service
├── types/
│   └── safety.ts                   # Type definitions
└── routes.tsx                      # Route configuration
```

## 🚦 Getting Started

### Prerequisites
- Node.js 18+ 
- pnpm (recommended) or npm

### Installation

1. Clone the repository
2. Install dependencies:
   ```bash
   pnpm install
   ```

3. Start the development server:
   ```bash
   pnpm dev
   ```

4. Open your browser:
   - User Interface: `http://localhost:5173/`
   - Admin Dashboard: `http://localhost:5173/admin`

## 📖 Usage Guide

### User Interface (Smart Safety Pole)

1. **Trigger Emergency Alert**:
   - Press and hold the red "EMERGENCY SOS" button for 3 seconds
   - Screen will turn red and display confirmation message
   - Alert is automatically sent to Admin Dashboard

2. **Use Push-to-Talk**:
   - After triggering emergency, the PTT button becomes enabled
   - Tap "Push to Talk" to connect voice channel
   - Tap again to disconnect

### Admin Dashboard (Control Center)

1. **Monitor Alerts**:
   - View all active alerts in the Real-Time Alert Panel
   - Alerts are color-coded by priority level
   - See location, pole ID, and timestamp for each alert

2. **Respond to Alerts**:
   - Click on an alert to select it
   - Use action buttons to:
     - Notify Police
     - Notify Campus Security
     - Mark as Resolved

3. **Voice Communication**:
   - Click "Connect" button on any alert to enable voice channel
   - Status updates in real-time on both interfaces

4. **View History**:
   - Scroll through Alert History Logs section
   - See all past alerts with their status and resolution time

5. **Clear Data**:
   - Use "Clear All" button to reset all alerts (for testing)

## 🎨 Design System

### Color Scheme
- **Emergency**: Red (`hsl(0 84.2% 60.2%)`) - High priority alerts
- **Warning**: Orange/Yellow (`hsl(38 92% 50%)`) - Medium priority alerts
- **Success**: Green (`hsl(142 76% 36%)`) - Resolved alerts
- **Info**: Blue (`hsl(217 91% 60%)`) - Information messages

### Responsive Design
- Mobile-first approach
- Desktop-optimized admin dashboard
- Breakpoints: 640px (sm), 768px (md), 1024px (lg), 1280px (xl)

## 🔧 Technical Details

### Real-Time Synchronization
The system uses browser's CustomEvent API for real-time communication between User Interface and Admin Dashboard:

```typescript
// Alert updates
window.dispatchEvent(new CustomEvent('safety_alert_update', { detail: { alerts } }));

// PTT updates
window.dispatchEvent(new CustomEvent('ptt_status_update', { detail: { poleId, active } }));
```

### Data Persistence
All alert data is stored in browser localStorage:
- Key: `women_safety_alerts`
- Format: JSON array of Alert objects
- Persists across page refreshes

### Alert Priority Logic
- **High Priority**: All new emergency alerts (red highlight)
- **Medium Priority**: Alerts requiring verification (yellow highlight)
- **Low Priority**: Logged alerts (gray highlight)

## 🧪 Testing

### Manual Testing Workflow

1. **Open two browser windows**:
   - Window 1: User Interface (`/`)
   - Window 2: Admin Dashboard (`/admin`)

2. **Test Emergency Alert**:
   - In Window 1, press and hold the emergency button for 3 seconds
   - Verify alert appears immediately in Window 2

3. **Test PTT**:
   - In Window 1, activate PTT button
   - In Window 2, verify voice channel status updates

4. **Test Response Actions**:
   - In Window 2, select an alert
   - Click "Notify Police" or "Notify Campus Security"
   - Verify status updates in alert panel and history

5. **Test Resolution**:
   - Click "Mark as Resolved"
   - Verify alert moves to resolved state in history

## 🚀 Deployment

### Build for Production

```bash
pnpm build
```

The build output will be in the `dist/` directory.

### Environment Variables
No environment variables required for demo functionality.

## 📝 Future Enhancements

- [ ] Integration with actual LoRa network
- [ ] GPS location tracking
- [ ] Real audio streaming for PTT
- [ ] SMS/Email notifications
- [ ] Mobile app version
- [ ] Multi-language support
- [ ] Analytics dashboard
- [ ] User authentication for admin panel

## 🤝 Contributing

This is a demo/hackathon project. For production use, consider:
- Backend API integration
- Database for persistent storage
- Authentication and authorization
- Real-time WebSocket connections
- Security hardening

## 📄 License

© 2026 Women Safety System

## 👥 Support

For questions or issues, please refer to the documentation or contact the development team.

---

**Note**: This is a demonstration system. In real deployment, it would use LoRa technology for offline communication and integrate with actual emergency response systems.
