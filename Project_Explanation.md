# SanHub Project Analysis

This document provides a detailed analysis of the **SanHub** project found in `in.html`.

## 1. Executive Summary

**SanHub** is a sophisticated, single-page application (SPA) designed as a personal portfolio and project showcase. It heavily draws inspiration from the GitHub user interface but is customized with a unique "Royal" theme (Gold/Dark Navy).

The project is entirely **client-side**, meaning it runs directly in the browser without a backend server. All data (repositories, projects, profile information) is persisted using the browser's **Local Storage**.

## 2. Technology Stack

The project is built using modern web technologies, avoiding heavy frameworks in favor of a lightweight, performance-focused approach:

*   **Core Structure**: HTML5 (Semantic).
*   **Styling**: 
    *   **Tailwind CSS** (via CDN script): Used for layout, spacing, and utility classes.
    *   **Custom CSS**: Specific styling for the scrollbar, glassmorphism effects, and the 3D viewer container.
    *   **Configuration**: Tailwind is configured at runtime with a custom color palette (`san.dark`, `san.gold`, etc.).
*   **Scripting**: Vanilla JavaScript (ES6+). No build step is required.
*   **Icons**: **Lucide Icons** (via CDN) for consistent, crisp SVG iconography.
*   **3D Graphics**: **Three.js** (via ES Module import) for rendering 3D models (`.glb`/`.gltf`).

## 3. Key Functionality & Modules

The application logic is encapsulated within a global `app` object and several helper modules:

### A. Data Management (`store`)
*   **Centralized State**: All application data (profile, repos, projects) is stored in a single JSON object.
*   **Persistence**: Data is automatically saved to `localStorage` ('sanhub_data') whenever a change occurs (e.g., adding a repo, changing theme).
*   **Default Data**: Initializes with a preset "SanStudio" profile if no local data is found.

### B. Routing & Navigation
*   **Hash-Based Routing**: Uses URL hashes (`#overview`, `#repositories`, `#projects`) to handle navigation without page reloads.
*   **Dynamic Rendering**: The properties of the `views` object correspond to the hash routes. When the hash changes, the main container (`#router-view`) is cleared and repopulated with the HTML string returned by the matching view function.

### C. 3D Model Viewer (`window.initSanHub3D`)
*   **Three.js Integration**: Located mainly in the "Overview" tab.
*   **Features**:
    *   Loads 3D models (GLB/GLTF format).
    *   Orbit controls (rotate, zoom).
    *   Auto-rotation.
    *   **File Upload**: Users can upload their own `.glb` file to view it instantly in the browser.
*   **Default Model**: Attempts to load `Sword.glb` by default.

### D. Features by Tab
1.  **Overview**:
    *   **Portfolio Spotlight**: Highlights the most recently added project.
    *   **Popular Repo**: Displays the repository with the most stars.
    *   **Activity Feed**: A timeline of user actions (created repo, starred repo, etc.).
    *   **3D Showcase**: Interactive 3D viewer.
2.  **Repositories**:
    *   **List View**: Searchable list of all repositories.
    *   **Drawer Details**: Clicking a repo opens a side drawer showing the README (rendered from Markdown), tags, language, and star count.
    *   **Create Functionality**: Users can add new repositories via a modal.
3.  **Projects**:
    *   **Gallery Grid**: Display of hosted web projects.
    *   **Preview**: "Demo" button opens the project URL in a modal iframe (or new tab if embedding is blocked).

### E. User Customization
*   **Profile Editing**: Users can change their avatar by clicking the camera icon (images are converted to Base64 and stored).
*   **Theme Toggle**: Button to switch between Light and Dark modes.

## 4. File Analysis (`in.html`)

Access the file at: [in.html](file:///d:/HTML/20-02-2026/SanHub-main/in.html)

*   **Lines 1-117 (Head)**: Setup of Tailwind config, custom CSS variables, font imports, and Three.js import map.
*   **Lines 118-246 (Body - Layout)**:
    *   **Header**: Sticky navigation bar.
    *   **Sidebar**: Static profile information area.
    *   **Main**: The `#router-view` div where dynamic content is injected.
*   **Lines 267-392 (Modals)**: Hidden HTML structures for "New Repo", "New Project", and "Preview" modals.
*   **Lines 395-1130 (Main Script)**:
    *   `DEFAULT_DATA`: Initial mock data.
    *   `store`: State management methods.
    *   `views`: HTML template literal generators for each tab.
    *   `app`: Controller logic (event listeners, routing, initialization).
*   **Lines 1132-1270 (3D Script)**: Module script handling the Three.js scene, camera, renderer, and model loading.

## 5. How to Run
1.  **Simply Open the File**: Double-click `in.html` to open it in any modern web browser.
2.  **Local Server (Recommended)**: For the 3D model (`Sword.glb`) to load correctly without CORS policies blocking it, it is best to run this via a local server (e.g., generic `http-server` or VS Code's "Live Server" extension).
    *   If simply opening the file, the 3D viewer might show a loading error depending on browser strictness regarding local file access, but the rest of the app will work perfectly.

## 6. How to Use
1.  **Navigate**: Click tabs to switch views.
2.  **Add Content**:
    *   Click the **+** (Plus) icon in the header.
    *   Select "New repository" or "New project".
    *   Fill in the details and submit.
3.  **Interact**:
    *   **Star** repositories to see the count increase.
    *   **Search** repositories using the search bar.
    *   **Upload 3D Model**: In the Overview tab, use the "Load Your Model" button to view any `.glb` file from your computer.

## 7. Future Recommendations
*   **Data Export/Import**: The app currently has `exportData` and `importData` functions hooked up in the "Plus" menu. This is excellent for backing up the LocalStorage data.
*   **Markdown Parsing**: The current parser is a simple Regex replacement. Integrating a library like `marked.js` would provide robust README rendering.
