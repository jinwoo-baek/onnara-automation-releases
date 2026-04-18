# OnNara Automation (온나라 자동화)

This project provides an automation layer for the "OnNara" (온나라) system, specifically designed for handling self-inspections and fire safety manager registrations. It bridges Excel-based data management with web-based form submission through a local coordination server and a browser extension.

## 🚀 Microsoft Edge Extension
The browser execution layer is available on the Microsoft Edge Add-ons store:
**[Install OnNara Automation Executor](https://microsoftedge.microsoft.com/addons/detail/gnaenedamdfcknbodbfdgkhhgonmcghc)***

## 🏗️ Architecture

The system consists of three main components:

1.  **VBA Macros (Excel):**
    *   Located in the `server/macro/` directory.
    *   Provides a user-friendly way to manage data in Excel.
    *   Sends record data to the local server via HTTP POST requests.
    *   Includes logic for timestamping and history tracking.

2.  **Local Coordination Server (Electron):**
    *   Located in the `server/` directory.
    *   An Electron application that acts as a central hub.
    *   Maintains an execution queue and manages the automation state.
    *   Provides a Control Panel UI for monitoring tasks, managing the scan directory (for PDF attachments), and manual entry.
    *   Communicates with the browser extension via WebSockets.

3.  **Browser Extension (Executor):**
    *   Located in the `executor/` directory.
    *   A Manifest V3 browser extension.
    *   Listens for signals from the local server to perform actions on the target OnNara pages (`http://10.191.0.54/*`).
    *   Automatically navigates through frames, clicks buttons, and fills form fields based on the payload received from the server.

## 🛠️ Getting Started

### Prerequisites
*   [Node.js](https://nodejs.org/) (recommended version 18 or higher)
*   [Microsoft Edge](https://www.microsoft.com/edge) browser

### Installation & Setup

1.  **Server Setup:**
    ```bash
    cd server
    npm install
    npm start
    ```
    *   This will launch the Electron application.
    *   The Control Panel will be available within the app window (loading `http://localhost:8080`).

2.  **Extension Setup:**
    *   Install the extension from the [Microsoft Edge Store](https://microsoftedge.microsoft.com/addons/detail/gnaenedamdfcknbodbfdgkhhgonmcghc).
    *   Alternatively, for development:
        1. Open Edge and go to `edge://extensions/`.
        2. Enable "Developer mode".
        3. Click "Load unpacked" and select the `executor/` folder.

3.  **Excel Integration:**
    *   Open the Server Control Panel.
    *   Navigate to the "VBA 매크로 복사" (VBA Macro Copy) section.
    *   Copy the relevant macro (Type A or Type B) and paste it into your Excel Workbook's VBA editor.

## 📁 Project Structure

```text
/
├── executor/             # Browser extension source code
│   ├── icons/            # Extension icons
│   ├── content.js        # Main execution logic (DOM manipulation)
│   └── manifest.json     # Extension manifest
├── server/               # Electron server source code
│   ├── macro/            # VBA macro source files (.vb)
│   ├── control_panel.html# UI for the server
│   ├── server.js         # Core server logic (WebSocket/HTTP/Electron)
│   └── package.json      # Node.js dependencies
├── helpers.md            # Reference snippets for VBA macros
└── prompts.md            # Project history and development notes
```

## 📄 License
This project is private and intended for internal use.
