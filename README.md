<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Content / UG26FA Digital Systems (EE-4322-01)</title>
    <!-- Official Blackboard Ultra Gold/Plum Course Silhouette Favicon -->
    <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Crect width='32' height='32' rx='6' fill='%231E1E1E'/%3E%3Cpath d='M8 7h7v8H8zm9 0h7v8h-7zm0 10h7v8h-7zm-9 0h7v8H8z' fill='%23C56FD5'/%3E%3C/svg%3E">

    <style>
        * {
            box-sizing: border-box;
        }

        html, body {
            margin: 0;
            padding: 0;
            height: 100vh;
            width: 100vw;
            overflow: hidden;
            font-family: 'Open Sans', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: #F8F9FA;
        }

        /* ========================================================
           FULL-WIDTH BACKGROUND: BLACKBOARD ULTRA WORKSPACE
           ======================================================== */
        #pageBackground {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow-y: auto;
            background-color: #F8F9FA;
            z-index: 1;
        }

        /* 1. Ultra Top Header Bar */
        .bb-app-bar {
            background-color: #212121;
            color: #FFFFFF;
            height: 48px;
            display: flex;
            align-items: center;
            padding: 0 24px;
            gap: 16px;
            font-size: 14px;
            border-bottom: 1px solid #333333;
        }

        .bb-home-btn {
            background-color: #383838;
            border-radius: 4px;
            width: 30px;
            height: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            text-decoration: none;
        }

        .bb-home-btn svg {
            width: 17px;
            height: 17px;
            fill: #FFFFFF;
        }

        .bb-course-switch-btn {
            display: flex;
            align-items: center;
            gap: 6px;
            cursor: pointer;
            font-size: 14.5px;
            font-weight: 600;
            color: #FFFFFF;
        }

        .bb-pipe-separator {
            width: 1px;
            height: 18px;
            background-color: #4A4A4A;
        }

        .bb-course-name-top {
            font-size: 14.5px;
            color: #FFFFFF;
            font-weight: 600;
            letter-spacing: -0.1px;
        }

        .bb-status-pill {
            margin-left: auto;
            background-color: #C56FD5;
            color: #1A1A1A;
            font-size: 11px;
            font-weight: 800;
            letter-spacing: 0.5px;
            text-transform: uppercase;
            padding: 2.5px 12px;
            border-radius: 12px;
        }

        /* 2. Ribbon Navigation Tabs */
        .bb-tools-nav {
            background-color: #212121;
            display: flex;
            padding: 0 24px;
            border-bottom: 1px solid #4D4D4D;
            overflow-x: auto;
            align-items: center;
        }

        .bb-tool-item {
            color: #CDCDCD;
            font-size: 14px;
            font-weight: 500;
            padding: 12px 14px 10px 14px;
            text-decoration: none;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            border-bottom: 3.5px solid transparent;
            white-space: nowrap;
        }

        .bb-tool-item:hover {
            color: #FFFFFF;
        }

        .bb-tool-item.active {
            color: #FFFFFF;
            font-weight: 700;
            border-bottom-color: #C56FD5;
        }

        .bb-counter-badge {
            background-color: #B666C7;
            color: #1B1B1B;
            font-size: 11px;
            line-height: 1;
            width: 17px;
            height: 17px;
            border-radius: 50%;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            font-weight: 800;
        }

        /* 3. Desaturated Plum Wave Banner */
        .bb-hero-banner {
            position: relative;
            background: linear-gradient(90deg, #1A131E 0%, #29182E 40%, #1F1523 100%);
            height: 220px;
            overflow: hidden;
            display: flex;
            align-items: flex-end;
            padding: 0 48px 34px 48px;
        }

        .bb-banner-curves {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }

        .bb-hero-title {
            position: relative;
            z-index: 2;
            color: #FFFFFF;
            margin: 0;
            font-size: 26px;
            font-weight: 600;
            letter-spacing: -0.2px;
        }

        /* 4. Fluid Edge-to-Edge Grid Container */
        .bb-main-grid {
            display: flex;
            width: 100%;
            padding: 28px 48px;
            gap: 36px;
            align-items: flex-start;
        }

        .bb-content-section {
            flex: 1 1 auto;
            min-width: 0;
        }

        .bb-sidebar-section {
            width: 320px;
            flex-shrink: 0;
            display: flex;
            flex-direction: column;
            gap: 24px;
        }

        /* 5. Course Content Column */
        .bb-section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 14px;
        }

        .bb-section-header h2 {
            margin: 0;
            font-size: 18px;
            font-weight: 600;
            color: #262626;
        }

        .bb-search-btn {
            background: none;
            border: none;
            cursor: pointer;
            padding: 6px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #262626;
            border-radius: 50%;
        }

        .bb-search-btn:hover {
            background: #E5E5E5;
        }

        /* Expandable Accordion Folders */
        .bb-accordion-card {
            background: #FFFFFF;
            border: 1px solid #E5E5E5;
            border-radius: 4px;
            margin-bottom: 14px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.04);
            overflow: hidden;
            transition: border-color 0.15s ease;
        }

        .bb-accordion-card.open {
            border-color: #CDCDCD;
        }

        .bb-card-header {
            padding: 16px 20px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            cursor: pointer;
            user-select: none;
            background: #FFFFFF;
        }

        .bb-card-header:hover {
            background: #F8F9FA;
        }

        .bb-card-title-group {
            display: flex;
            align-items: center;
            gap: 16px;
        }

        .bb-folder-icon {
            width: 22px;
            height: 22px;
            fill: none;
            stroke: #333333;
            stroke-width: 1.8;
            stroke-linejoin: round;
            flex-shrink: 0;
        }

        .bb-folder-label {
            font-size: 15px;
            font-weight: 600;
            color: #262626;
        }

        .bb-card-header:hover .bb-folder-label {
            text-decoration: underline;
        }

        .bb-chevron-icon {
            width: 16px;
            height: 16px;
            fill: none;
            stroke: #444444;
            stroke-width: 2;
            stroke-linecap: round;
            stroke-linejoin: round;
            transition: transform 0.2s ease;
        }

        .bb-accordion-card.open .bb-chevron-icon {
            transform: rotate(180deg);
        }

        /* Folder Sub-drawer */
        .bb-folder-drawer {
            display: none;
            padding: 4px 20px 16px 58px;
            background: #FFFFFF;
            border-top: 1px solid #F0F0F0;
        }

        .bb-accordion-card.open .bb-folder-drawer {
            display: block;
        }

        .bb-subitem-row {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 11px 0;
            border-bottom: 1px solid #F4F4F4;
            color: #262626;
            font-size: 14px;
            cursor: pointer;
        }

        .bb-subitem-row:last-child {
            border-bottom: none;
        }

        .bb-subitem-row:hover {
            color: #006DC7;
            text-decoration: underline;
        }

        .bb-subitem-icon {
            width: 18px;
            height: 18px;
            fill: none;
            stroke: #4A5568;
            stroke-width: 1.6;
            flex-shrink: 0;
        }

        /* 6. Sidebar Panels */
        .bb-card-panel {
            background: #FFFFFF;
            border: 1px solid #E5E5E5;
            border-radius: 4px;
            padding: 18px 20px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.03);
        }

        .bb-card-panel h3 {
            margin: 0 0 16px 0;
            font-size: 15px;
            font-weight: 700;
            color: #262626;
        }

        .bb-faculty-profile {
            display: flex;
            align-items: center;
            gap: 14px;
        }

        .bb-faculty-avatar {
            width: 46px;
            height: 46px;
            border-radius: 50%;
            background: #2D3748;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
        }

        .bb-faculty-avatar svg {
            width: 100%;
            height: 100%;
        }

        .bb-faculty-text {
            flex: 1;
            min-width: 0;
        }

        .bb-faculty-name {
            font-size: 14.5px;
            font-weight: 700;
            color: #262626;
            margin: 0;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .bb-faculty-badge {
            display: inline-block;
            background: #EFEFEF;
            color: #4A4A4A;
            font-size: 10px;
            font-weight: 800;
            padding: 2px 8px;
            border-radius: 2px;
            text-transform: uppercase;
            margin-top: 3px;
        }

        .bb-envelope-btn {
            background: none;
            border: none;
            cursor: pointer;
            padding: 6px;
            color: #262626;
            border-radius: 4px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .bb-envelope-btn:hover {
            background: #F0F0F0;
        }

        .bb-envelope-btn svg {
            width: 19px;
            height: 19px;
            fill: currentColor;
        }

        .bb-actions-list {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .bb-action-entry {
            display: flex;
            align-items: flex-start;
            gap: 14px;
            padding: 12px 0;
            border-bottom: 1px solid #F0F0F0;
            cursor: pointer;
        }

        .bb-action-entry:last-child {
            border-bottom: none;
        }

        .bb-action-entry svg {
            width: 18px;
            height: 18px;
            margin-top: 2px;
            flex-shrink: 0;
        }

        .bb-action-heading {
            font-size: 14px;
            font-weight: 700;
            color: #262626;
            margin: 0 0 2px 0;
        }

        .bb-action-sublink {
            font-size: 12.5px;
            color: #2073A1;
            margin: 0;
            text-decoration: underline;
        }

        /* Fixed Question Mark Beacon */
        .bb-floating-help {
            position: fixed;
            bottom: 20px;
            right: 24px;
            width: 34px;
            height: 34px;
            background: #FFFFFF;
            border: 1px solid #CDCDCD;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 6px rgba(0,0,0,0.18);
            cursor: pointer;
            z-index: 100;
        }

        .bb-floating-help svg {
            width: 19px;
            height: 19px;
            fill: #333333;
        }

        /* ========================================================
           NOTEPAD++ FLOATING APPLICATION WINDOW
           ======================================================== */
        .npp-window {
            position: absolute;
            top: 75px;
            left: 120px;
            width: 880px;
            height: 580px;
            background-color: #FFFFFF;
            border: 1px solid #707070;
            box-shadow: 0 16px 42px rgba(0, 0, 0, 0.45);
            display: flex;
            flex-direction: column;
            border-radius: 3px;
            overflow: hidden;
            min-width: 480px;
            min-height: 320px;
            z-index: 10000;
        }

        .npp-window.maximized {
            top: 0 !important;
            left: 0 !important;
            width: 100vw !important;
            height: 100vh !important;
            border: none;
            border-radius: 0;
        }

        .npp-titlebar {
            background-color: #FFFFFF;
            color: #000000;
            padding: 5px 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 12px;
            cursor: move;
            user-select: none;
            border-bottom: 1px solid #F0F0F0;
        }

        .npp-controls {
            display: flex;
            gap: 14px;
            font-size: 11px;
            padding-right: 4px;
        }

        .npp-controls span {
            cursor: pointer;
            display: inline-block;
            padding: 2px 4px;
        }

        .npp-controls span:hover {
            background-color: #E5E5E5;
        }

        .npp-menubar {
            background-color: #F0F0F0;
            padding: 2px 6px;
            display: flex;
            gap: 12px;
            font-size: 11.5px;
            color: #000000;
            user-select: none;
        }

        .menu-item {
            position: relative;
            cursor: pointer;
            padding: 2px 6px;
        }

        .menu-item:hover {
            background-color: #E5E5E5;
        }

        .dropdown-content {
            display: none;
            position: absolute;
            top: 100%;
            left: 0;
            background-color: #F9F9F9;
            min-width: 150px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.15);
            border: 1px solid #CCCCCC;
            z-index: 10010;
        }

        .dropdown-content div {
            padding: 6px 14px;
            font-size: 11.5px;
            color: #000000;
            text-align: left;
        }

        .dropdown-content div:hover {
            background-color: #007ACC;
            color: white;
        }

        .menu-item:hover .dropdown-content {
            display: block;
        }

        .npp-toolbar {
            background-color: #F5F5F5;
            border-top: 1px solid #E0E0E0;
            border-bottom: 1px solid #D0D0D0;
            padding: 4px 8px;
            display: flex;
            gap: 4px;
            user-select: none;
            align-items: center;
        }

        .icon-group {
            display: flex;
            border-right: 1px solid #D0D0D0;
            padding-right: 6px;
            margin-right: 4px;
            gap: 4px;
            height: 22px;
            align-items: center;
        }

        .t-btn {
            cursor: pointer;
            padding: 3px;
            border: 1px solid transparent;
            border-radius: 2px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: none;
        }

        .t-btn:hover {
            background-color: #EDF2F7;
            border: 1px solid #CBD5E0;
        }

        .t-btn svg {
            width: 14px;
            height: 14px;
            display: block;
        }

        .npp-tabs-bar {
            background-color: #F0F0F0;
            display: flex;
            align-items: flex-end;
            padding: 3px 6px 0 6px;
            border-bottom: 1px solid #CCCCCC;
            user-select: none;
            overflow-x: auto;
        }

        .tab-list {
            display: flex;
            gap: 2px;
        }

        .npp-tab {
            background-color: #E1E1E1;
            color: #4A4A4A;
            padding: 4px 10px;
            font-size: 11.5px;
            border-top: 2px solid transparent;
            border-left: 1px solid #C4C4C4;
            border-right: 1px solid #C4C4C4;
            border-top-left-radius: 2px;
            border-top-right-radius: 2px;
            display: flex;
            align-items: center;
            gap: 6px;
            cursor: pointer;
            white-space: nowrap;
        }

        .npp-tab.active {
            background-color: #FFFFFF;
            color: #000000;
            border-top: 3px solid #FF3B30;
            border-bottom: 1px solid #FFFFFF;
            margin-bottom: -1px;
        }

        .npp-tab svg {
            width: 10px;
            height: 10px;
            flex-shrink: 0;
        }

        .npp-tab .tab-close {
            font-size: 10px;
            color: #888888;
            border-radius: 50%;
            padding: 1px 3px;
            margin-left: 2px;
        }

        .npp-tab .tab-close:hover {
            background-color: #E2E8F0;
            color: #E53E3E;
        }

        .tab-add-btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 14px;
            font-weight: bold;
            color: #555555;
            padding: 2px 8px;
            margin-left: 4px;
            border-radius: 2px;
        }

        .tab-add-btn:hover {
            background-color: #E0E0E0;
        }

        .npp-editor-container {
            display: flex;
            flex: 1;
            overflow: hidden;
            position: relative;
            background-color: #FFFFFF;
        }

        .npp-linenumbers {
            background-color: #ECE9D8;
            color: #777777;
            font-family: 'Consolas', 'Courier New', monospace;
            font-size: 13px;
            padding: 6px 5px;
            text-align: right;
            min-width: 38px;
            user-select: none;
            border-right: 1px solid #A0A0A0;
            line-height: 1.5;
            white-space: pre;
            overflow-y: hidden;
        }

        .npp-foldmargin {
            background-color: #F0F0F0;
            width: 14px;
            border-right: 1px solid #D0D0D0;
            flex-shrink: 0;
        }

        .npp-textarea {
            flex: 1;
            background-color: #FFFFFF;
            color: #000000;
            font-family: 'Consolas', 'Courier New', monospace;
            font-size: 13px;
            padding: 6px 8px;
            line-height: 1.5;
            outline: none;
            border: none;
            resize: none;
            white-space: pre;
            overflow-x: auto;
            overflow-y: scroll;
            tab-size: 4;
        }

        .npp-statusbar {
            background-color: #F0F0F0;
            color: #000000;
            padding: 3px 10px;
            font-size: 11.5px;
            display: flex;
            justify-content: space-between;
            border-top: 1px solid #CCCCCC;
            user-select: none;
        }

        .npp-status-right span {
            border-left: 1px solid #CCCCCC;
            padding: 0 10px;
        }

        .resize-handle {
            position: absolute;
            width: 12px;
            height: 12px;
            right: 0;
            bottom: 0;
            cursor: se-resize;
            z-index: 200;
            background: linear-gradient(135deg, transparent 4px, #999 4px);
        }
    </style>
</head>
<body>

    <input type="file" id="fileLoader" style="position:absolute; width:1px; height:1px; opacity:0; z-index:-1;" onchange="handleFileImport(event)">

    <!-- ========================================================
         INTERACTIVE BLACKBOARD BACKGROUND
         ======================================================== -->
    <div id="pageBackground">
        <!-- Top App Bar -->
        <header class="bb-app-bar">
            <div class="bb-home-btn" title="Institutional Home">
                <svg viewBox="0 0 16 16"><path d="M15.46 14.46c0 .85-.69 1.54-1.54 1.54H10.15c-.55 0-1-.45-1-1v-4.31a.08.08 0 0 0-.08-.08H6.92a.08.08 0 0 0-.08.08V15c0 .55-.45 1-1 1H2.08c-.85 0-1.54-.69-1.54-1.54V6.38c0-.3.13-.58.36-.77L7.36.23l.07-.05a1 1 0 0 1 1.21.05l6.46 5.39c.23.19.36.47.36.76zM11.15 14h2.31V6.85L8 2.3 2.54 6.85V14h2.31v-3.31c0-1.15.93-2.08 2.08-2.08h2.15c1.15 0 2.08.93 2.08 2.08z"/></svg>
            </div>
            <div class="bb-course-switch-btn">
                <span>Courses</span>
                <svg viewBox="0 0 16 16" style="width:10px; height:10px; fill:#fff;"><path d="M12.5 5h-9L8 11z"/></svg>
            </div>
            <div class="bb-pipe-separator"></div>
            <span class="bb-course-name-top">UG26FA Digital Systems (EE-4322-01)</span>
            <span class="bb-status-pill">OPEN</span>
        </header>

        <!-- Navigation Tabs Ribbon -->
        <nav class="bb-tools-nav">
            <a class="bb-tool-item active">Content</a>
            <a class="bb-tool-item">Calendar</a>
            <a class="bb-tool-item">Announcements <span class="bb-counter-badge">6</span></a>
            <a class="bb-tool-item">Discussions</a>
            <a class="bb-tool-item">Gradebook</a>
            <a class="bb-tool-item">Messages <span class="bb-counter-badge">1</span></a>
            <a class="bb-tool-item">Groups</a>
            <a class="bb-tool-item">Achievements</a>
        </nav>

        <!-- Blackboard Hero Plum Banner with Muted Dark Gradient Curves -->
        <div class="bb-hero-banner">
            <svg class="bb-banner-curves" viewBox="0 0 1440 220" preserveAspectRatio="none">
                <path d="M0,0 C380,110 760,20 1140,130 C1280,170 1380,150 1440,110 L1440,220 L0,220 Z" fill="rgba(61, 35, 71, 0.45)"/>
                <path d="M0,45 C440,165 820,35 1200,165 C1320,205 1400,195 1440,170 L1440,220 L0,220 Z" fill="rgba(42, 23, 51, 0.7)"/>
                <path d="M550,0 C800,120 1120,50 1440,105 L1440,0 Z" fill="rgba(182, 102, 199, 0.08)"/>
            </svg>
            <h1 class="bb-hero-title">UG26FA Digital Systems (EE-4322-01)</h1>
        </div>

        <!-- Full-Width Page Layout -->
        <div class="bb-main-grid">
            <!-- Left: Interactive Content Outline -->
            <main class="bb-content-section">
                <div class="bb-section-header">
                    <h2>Course Content</h2>
                    <button class="bb-search-btn" title="Search course content">
                        <svg viewBox="0 0 16 16" style="width:18px; height:18px; fill:#262626;"><path fill-rule="evenodd" d="M6.5 0C2.91 0 0 2.91 0 6.5S2.91 13 6.5 13c1.43 0 2.76-.46 3.83-1.25l3.96 3.96c.39.39 1.02.39 1.41 0s.39-1.02 0-1.41l-3.96-3.96C12.54 9.26 13 7.93 13 6.5 13 2.91 10.09 0 6.5 0M2 6.5C2 4.01 4.01 2 6.5 2S11 4.01 11 6.5 8.99 11 6.5 11 2 8.99 2 6.5" clip-rule="evenodd"/></svg>
                    </button>
                </div>

                <!-- Folder 1: Syllabus -->
                <div class="bb-accordion-card open" id="folder1">
                    <div class="bb-card-header" onclick="toggleFolder('folder1')">
                        <div class="bb-card-title-group">
                            <svg class="bb-folder-icon" viewBox="0 0 24 24"><path d="M3 5h6l2 2h10v12H3V5z"/></svg>
                            <span class="bb-folder-label">Syllabus & Course Information</span>
                        </div>
                        <svg class="bb-chevron-icon" viewBox="0 0 16 16"><path d="M3 6l5 5 5-5"/></svg>
                    </div>
                    <div class="bb-folder-drawer">
                        <div class="bb-subitem-row">
                            <svg class="bb-subitem-icon" viewBox="0 0 16 16"><path d="M3 1h7l3 3v11H3V1z"/><path d="M10 1v3h3"/></svg>
                            <span>EE-4322 Syllabus - Fall Semester.pdf</span>
                        </div>
                        <div class="bb-subitem-row">
                            <svg class="bb-subitem-icon" viewBox="0 0 16 16"><circle cx="8" cy="8" r="7"/><path d="M8 5v1M8 8v4" stroke-linecap="round"/></svg>
                            <span>Course Overview, Office Hours & Grading Criteria</span>
                        </div>
                    </div>
                </div>

                <!-- Folder 2: Projects, Homeworks, & Labs -->
                <div class="bb-accordion-card open" id="folder2">
                    <div class="bb-card-header" onclick="toggleFolder('folder2')">
                        <div class="bb-card-title-group">
                            <svg class="bb-folder-icon" viewBox="0 0 24 24"><path d="M3 5h6l2 2h10v12H3V5z"/></svg>
                            <span class="bb-folder-label">Projects, Homeworks, & Labs</span>
                        </div>
                        <svg class="bb-chevron-icon" viewBox="0 0 16 16"><path d="M3 6l5 5 5-5"/></svg>
                    </div>
                    <div class="bb-folder-drawer">
                        <div class="bb-subitem-row">
                            <svg class="bb-subitem-icon" viewBox="0 0 16 16"><path d="M2 2h9l3 3v9H2V2z"/><path d="M5 8h6M5 11h4"/></svg>
                            <span>Lab 1: HDL Synthesis & FPGA Development Board Setup</span>
                        </div>
                        <div class="bb-subitem-row">
                            <svg class="bb-subitem-icon" viewBox="0 0 16 16"><path d="M2 2h9l3 3v9H2V2z"/><path d="M5 8h6M5 11h4"/></svg>
                            <span>Lab 2: Finite State Machine (FSM) Sequential Circuits</span>
                        </div>
                        <div class="bb-subitem-row">
                            <svg class="bb-subitem-icon" viewBox="0 0 16 16"><path d="M4 1h8v14H4z"/><path d="M6 4h4M6 7h4M6 10h2"/></svg>
                            <span>Homework Assignment 3 - Logic Minimization</span>
                        </div>
                    </div>
                </div>

                <!-- Folder 3: Lecture Materials -->
                <div class="bb-accordion-card" id="folder3">
                    <div class="bb-card-header" onclick="toggleFolder('folder3')">
                        <div class="bb-card-title-group">
                            <svg class="bb-folder-icon" viewBox="0 0 24 24"><path d="M3 5h6l2 2h10v12H3V5z"/></svg>
                            <span class="bb-folder-label">Lecture Materials</span>
                        </div>
                        <svg class="bb-chevron-icon" viewBox="0 0 16 16"><path d="M3 6l5 5 5-5"/></svg>
                    </div>
                    <div class="bb-folder-drawer">
                        <div class="bb-subitem-row">
                            <svg class="bb-subitem-icon" viewBox="0 0 16 16"><path d="M1 3h14v10H1z"/><path d="M4 7l3 2-3 2V7z" fill="#4A5568"/></svg>
                            <span>Lecture 01 - Intro to Synchronous Logic.pptx</span>
                        </div>
                        <div class="bb-subitem-row">
                            <svg class="bb-subitem-icon" viewBox="0 0 16 16"><path d="M1 3h14v10H1z"/><path d="M4 7l3 2-3 2V7z" fill="#4A5568"/></svg>
                            <span>Lecture 02 - Timing Constraints & Setup/Hold Times.pptx</span>
                        </div>
                    </div>
                </div>
            </main>

            <!-- Right: Details & Faculty Side Column -->
            <aside class="bb-sidebar-section">
                <!-- Faculty Widget -->
                <div class="bb-card-panel">
                    <h3>Course Faculty</h3>
                    <div class="bb-faculty-profile">
                        <div class="bb-faculty-avatar">
                            <svg viewBox="0 0 32 32">
                                <circle cx="16" cy="16" r="16" fill="#3D4A5C"/>
                                <path d="M16 8a5 5 0 1 0 0 10 5 5 0 0 0 0-10zm-8 18c0-4 4-6 8-6s8 2 8 6v1H8v-1z" fill="#CBD5E0"/>
                            </svg>
                        </div>
                        <div class="bb-faculty-text">
                            <p class="bb-faculty-name" title="Timothy Gilmour">Timothy Gilmour</p>
                            <span class="bb-faculty-badge">INSTRUCTOR</span>
                        </div>
                        <button class="bb-envelope-btn" title="Send Message">
                            <svg viewBox="0 0 16 16"><path fill-rule="evenodd" d="M1 2c-.55 0-1 .45-1 1v10c0 .55.45 1 1 1h14c.55 0 1-.45 1-1V3c0-.55-.45-1-1-1zm3.59 6L2 5.41v5.17zm8 4H3.41L6 9.41l1.29 1.3c.39.39 1.03.39 1.42 0L10 9.41zM14 10.59V5.41L11.41 8zM3.41 4 8 8.59 12.59 4z" clip-rule="evenodd"/></svg>
                        </button>
                    </div>
                </div>

                <!-- Details & Actions Widget -->
                <div class="bb-card-panel">
                    <h3>Details & Actions</h3>
                    <ul class="bb-actions-list">
                        <li class="bb-action-entry">
                            <svg viewBox="0 0 16 16" fill="none"><path stroke="#262626" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6.5 10C7.88 10 9 8.88 9 7.5S7.88 5 6.5 5 4 6.12 4 7.5 5.12 10 6.5 10M12 15c0-2.5-2.23-5-5.5-5S1 12.5 1 15M11.5 6C12.88 6 14 4.88 14 3.5S12.88 1 11.5 1 9 2.12 9 3.5 10.12 6 11.5 6M15 9c0-1-1.5-3-3-3"/></svg>
                            <div>
                                <p class="bb-action-heading">Roster</p>
                                <p class="bb-action-sublink">View everyone in your course</p>
                            </div>
                        </li>
                        <li class="bb-action-entry">
                            <svg viewBox="0 0 16 16"><g fill="#262626"><path d="M7 6c-.55 0-1 .45-1 1s.45 1 1 1v2H6c-.55 0-1 .45-1 1s.45 1 1 1h4c.55 0 1-.45 1-1s-.45-1-1-1H9V7c0-.55-.45-1-1-1zM9 4c0 .55-.45 1-1 1s-1-.45-1-1 .45-1 1-1 1 .45 1 1"/><path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8s3.58 8 8 8 8-3.58 8-8-3.58-8-8-8M2 8c0-3.31 2.69-6 6-6s6 2.69 6 6-2.69 6-6 6-6-2.69-6-6" clip-rule="evenodd"/></g></svg>
                            <div>
                                <p class="bb-action-heading">Course Description</p>
                                <p class="bb-action-sublink">View the course description</p>
                            </div>
                        </li>
                        <li class="bb-action-entry">
                            <svg viewBox="0 0 16 16"><g fill="#262626"><path fill-rule="evenodd" d="M12 0c.55 0 1 .45 1 1h2a1 1 0 0 1 1 1v3c0 .55-.45 1-1 1H2v8h7.47c.55 0 1 .45 1 1s-.45 1-1 1H1c-.55 0-1-.45-1-1V2c0-.55.45-1 1-1h2C3 .45 3.45 0 4 0s1 .45 1 1h6c0-.55.45-1 1-1M3 3H2v1h12V3h-1c0 .55-.45 1-1 1s-1-.45-1-1l-6 .01C5 3.55 4.55 4 4 4s-1-.45-1-1" clip-rule="evenodd"/><path d="M7 8c0-.55.45-1 1-1h1c.55 0 1 .45 1 1v1c0 .55-.45 1-1 1H8c-.55 0-1-.45-1-1zm8.83 2.55c.31-.46.18-1.08-.28-1.38s-1.08-.19-1.38.27l-1.84 2.76-.5-.76c-.31-.46-.93-.58-1.39-.27s-.58.92-.27 1.38l1.33 2a1 1 0 0 0 1.66 0zM4 10c-.55 0-1 .45-1 1v1c0 .55.45 1 1 1h1c.55 0 1-.45 1-1v-1c0-.55-.45-1-1-1 .55 0 1-.45 1-1V8c0-.55-.45-1-1-1H4c-.55 0-1 .45-1 1v1c0 .55.45 1 1 1"/></g></svg>
                            <div>
                                <p class="bb-action-heading">Attendance</p>
                                <p class="bb-action-sublink">View your attendance</p>
                            </div>
                        </li>
                        <li class="bb-action-entry">
                            <svg viewBox="0 0 16 16"><path fill="#262626" fill-rule="evenodd" d="M14 5.43c-.49.49-.98.99-1.49 1.46a8.6 8.6 0 0 1-.45.39c-.18.14-.39.3-.62.43-.19.11-.54.29-.94.29C9.12 8 8 6.88 8 5.5c0-.4.18-.75.29-.94.13-.23.29-.45.43-.62.14-.18.29-.34.39-.45.47-.51.97-.99 1.46-1.49A4 4 0 0 0 10.5 2C8.57 2 7 3.57 7 5.5c0 .34.06.7.15 1.02a1 1 0 0 1-.24.98c-1.54 1.6-3.09 3.2-4.63 4.81A1 1 0 0 0 2 13c0 .55.45 1 1 1 .29 0 .53-.12.73-.32l4.77-4.59a1 1 0 0 1 .98-.24C9.8 8.94 10.16 9 10.5 9 12.43 9 14 7.43 14 5.5v-.07m-8.88 9.7A3 3 0 0 1 3 16c-1.66 0-3-1.34-3-3 0-.8.32-1.54.84-2.08 1.42-1.47 2.84-2.94 4.25-4.42A5.57 5.57 0 0 1 5 5.5C5 2.46 7.46 0 10.5 0a5.48 5.48 0 0 1 2.45.57 1 1 0 0 1 .26 1.6c-.87.89-1.78 1.76-2.63 2.67a6.6 6.6 0 0 0-.3.35c-.1.12-.2.25-.27.39a.5.5 0 0 0 .41.41c.14-.07.27-.17.4-.27a6.6 6.6 0 0 0 .34-.3c.92-.85 1.79-1.76 2.68-2.63a1 1 0 0 1 1.6.26A5.48 5.48 0 0 1 16 5.5c0 3.04-2.46 5.5-5.5 5.5-.34 0-.68-.03-1.01-.09-1.46 1.4-2.94 2.79-4.38 4.22" clip-rule="evenodd"/></svg>
                            <div>
                                <p class="bb-action-heading">Books & Tools</p>
                                <p class="bb-action-sublink">View course & institution tools</p>
                            </div>
                        </li>
                    </ul>
                </div>
            </aside>
        </div>

        <!-- Help Button -->
        <div class="bb-floating-help" title="Help">
            <svg viewBox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm1 16h-2v-2h2v2zm1.07-7.75l-.9.92C12.45 11.9 12 12.5 12 14h-2v-.5c0-1.1.45-2.1 1.17-2.83l1.24-1.26c.37-.36.59-.86.59-1.41 0-1.1-.9-2-2-2s-2 .9-2 2H7c0-2.76 2.24-5 5-5s5 2.24 5 5c0 1.04-.42 1.99-1.07 2.75z"/></svg>
        </div>
    </div>


    <!-- ========================================================
         NOTEPAD++ FLOATING APPLICATION WINDOW
         ======================================================== -->
    <div class="npp-window" id="windowContainer">
        <!-- Titlebar -->
        <div class="npp-titlebar" id="windowDragHeader">
            <span id="windowTitle">digital_systems_notes.v - Notepad++</span>
            <div class="npp-controls">
                <span onclick="minimizeSimulation()">━</span>
                <span onclick="toggleMaximize(event)">🗖</span>
                <span onclick="hideNotepad()">✕</span>
            </div>
        </div>
        
        <!-- Menu -->
        <div class="npp-menubar">
            <div class="menu-item">File
                <div class="dropdown-content">
                    <div onclick="createNewTab()">New</div>
                    <div onclick="triggerFileInput(event)">Open...</div>
                    <div onclick="exportCurrentTab()">Save</div>
                    <div onclick="closeCurrentTab()">Close</div>
                </div>
            </div>
            <div class="menu-item">Edit</div>
            <div class="menu-item">Search</div>
            <div class="menu-item">View</div>
            <div class="menu-item">Encoding</div>
            <div class="menu-item">Language</div>
            <div class="menu-item">Settings</div>
            <div class="menu-item">Tools</div>
            <div class="menu-item">Macro</div>
            <div class="menu-item">Run</div>
        </div>

        <!-- Toolbar -->
        <div class="npp-toolbar">
            <div class="icon-group">
                <div class="t-btn" title="New file" onclick="createNewTab()">
                    <svg viewBox="0 0 16 16" fill="none"><path d="M3 1h7l3 3v11H3V1z" stroke="#4A5568" stroke-width="1.5"/><path d="M10 1v3h3" stroke="#4A5568" stroke-width="1.5"/></svg>
                </div>
                <div class="t-btn" title="Open file" onclick="triggerFileInput(event)">
                    <svg viewBox="0 0 16 16" fill="none"><path d="M1.5 3.5h4l1.5 1.5h7.5v8.5h-13V3.5z" stroke="#D69E2E" stroke-width="1.5" fill="#FEFCBF"/><path d="M1.5 6.5h13" stroke="#D69E2E" stroke-width="1.5"/></svg>
                </div>
                <div class="t-btn" title="Save file (Ctrl+S)" onclick="exportCurrentTab()">
                    <svg viewBox="0 0 16 16" fill="none"><path d="M2 2h10l2 2v10H2V2z" fill="#3182CE" stroke="#2B6CB0"/><rect x="5" y="2" width="6" height="4" fill="#FFF"/><rect x="5" y="9" width="6" height="5" fill="#E2E8F0"/></svg>
                </div>
                <div class="t-btn" title="Close current tab" onclick="closeCurrentTab()">
                    <svg viewBox="0 0 16 16" fill="none"><path d="M3 3l10 10M13 3L3 13" stroke="#E53E3E" stroke-width="2"/></svg>
                </div>
            </div>
            <div class="icon-group">
                <div class="t-btn" title="Cut" onclick="executeEditorCommand('cut')">
                    <svg viewBox="0 0 16 16" fill="none"><circle cx="4.5" cy="5.5" r="2" stroke="#4A5568" stroke-width="1.5"/><circle cx="4.5" cy="10.5" r="2" stroke="#4A5568" stroke-width="1.5"/><path d="M6.5 6.5l7 5.5M6.5 9.5l7-5.5" stroke="#4A5568" stroke-width="1.5"/></svg>
                </div>
                <div class="t-btn" title="Copy" onclick="executeEditorCommand('copy')">
                    <svg viewBox="0 0 16 16" fill="none"><rect x="4" y="4" width="9" height="10" stroke="#4A5568" stroke-width="1.5" fill="#FFF"/><path d="M3 11H2V2h9v1" stroke="#4A5568" stroke-width="1.5"/></svg>
                </div>
                <div class="t-btn" title="Paste" onclick="executeEditorCommand('paste')">
                    <svg viewBox="0 0 16 16" fill="none"><rect x="3" y="4" width="10" height="11" stroke="#4A5568" stroke-width="1.5" fill="#FFF"/><rect x="5" y="1" width="6" height="4" fill="#CBD5E0" stroke="#718096"/></svg>
                </div>
            </div>
            <div class="icon-group">
                <div class="t-btn" title="Zoom in" onclick="adjustZoom(1)">
                    <svg viewBox="0 0 16 16" fill="none"><circle cx="7" cy="7" r="5" stroke="#4A5568" stroke-width="1.5"/><path d="M7 4.5v5M4.5 7h5M11 11l3.5 3.5" stroke="#4A5568" stroke-width="1.5"/></svg>
                </div>
                <div class="t-btn" title="Zoom out" onclick="adjustZoom(-1)">
                    <svg viewBox="0 0 16 16" fill="none"><circle cx="7" cy="7" r="5" stroke="#4A5568" stroke-width="1.5"/><path d="M4.5 7h5M11 11l3.5 3.5" stroke="#4A5568" stroke-width="1.5"/></svg>
                </div>
            </div>
        </div>

        <!-- Tab Strip -->
        <div class="npp-tabs-bar">
            <div class="tab-list" id="tabList"></div>
            <button class="tab-add-btn" title="New file" onclick="createNewTab()">+</button>
        </div>

        <!-- Editor Work Area -->
        <div class="npp-editor-container">
            <div class="npp-linenumbers" id="lineNumbers">1</div>
            <div class="npp-foldmargin"></div>
            <textarea class="npp-textarea" id="editor" spellcheck="false" wrap="off"></textarea>
            <div class="resize-handle" id="resizableHandle"></div>
        </div>

        <!-- Status Ribbon -->
        <div class="npp-statusbar">
            <span id="statusFileMeta">Verilog source file  length : 0  lines : 1</span>
            <div class="npp-status-right">
                <span id="caretPos">Ln : 1  Col : 1  Sel : 0</span>
                <span>Windows (CRLF)</span>
                <span>UTF-8</span>
                <span>INS</span>
            </div>
        </div>
    </div>

    <!-- Background and Window Management Logic -->
    <script>
        function toggleFolder(folderId) {
            const card = document.getElementById(folderId);
            if (card) {
                card.classList.toggle('open');
            }
        }

        // Notepad++ Document Buffer & Tab Model
        let tabs = [
            {
                id: 1,
                name: 'digital_systems_notes.v',
                content: '// Module definition for Digital Systems course lab\nmodule counter_4bit (\n    input wire clk,\n    input wire rst_n,\n    output reg [3:0] count\n);\n    always @(posedge clk or negedge rst_n) begin\n        if (!rst_n)\n            count <= 4\'b0000;\n        else\n            count <= count + 1\'b1;\n    end\nendmodule'
            },
            {
                id: 2,
                name: 'lab_tasks.txt',
                content: 'Tasks for UG26FA Digital Systems:\n1. Verify simulation trace in ModelSim\n2. Program board through JTAG chain\n3. Push Verilog testbench to repo'
            }
        ];
        let activeTabId = 1;
        let tabCounter = 2;
        let fontZoomPx = 13;

        const editor = document.getElementById('editor');
        const lineNumbers = document.getElementById('lineNumbers');
        const tabList = document.getElementById('tabList');
        const windowTitle = document.getElementById('windowTitle');
        const statusMeta = document.getElementById('statusFileMeta');
        const caretPos = document.getElementById('caretPos');
        const win = document.getElementById('windowContainer');

        function renderTabs() {
            tabList.innerHTML = '';
            tabs.forEach(tab => {
                const tabEl = document.createElement('div');
                tabEl.className = `npp-tab ${tab.id === activeTabId ? 'active' : ''}`;
                tabEl.onclick = () => switchTab(tab.id);

                tabEl.innerHTML = `
                    <svg viewBox="0 0 16 16" fill="${tab.id === activeTabId ? '#FF3B30' : '#888888'}">
                        <circle cx="8" cy="8" r="7"/>
                    </svg>
                    <span>${tab.name}</span>
                    <span class="tab-close" onclick="event.stopPropagation(); closeTabById(${tab.id})">✕</span>
                `;
                tabList.appendChild(tabEl);
            });

            const current = getCurrentTab();
            if (current) {
                windowTitle.innerText = `${current.name} - Notepad++`;
            }
        }

        function getCurrentTab() {
            return tabs.find(t => t.id === activeTabId);
        }

        function switchTab(id) {
            const current = getCurrentTab();
            if (current) {
                current.content = editor.value;
            }
            activeTabId = id;
            const newTab = getCurrentTab();
            if (newTab) {
                editor.value = newTab.content;
            }
            renderTabs();
            syncEditor();
        }

        function createNewTab(initialName = null, initialContent = '') {
            tabCounter++;
            const name = initialName || `new ${tabCounter}`;
            const newTab = {
                id: Date.now(),
                name: name,
                content: initialContent
            };
            tabs.push(newTab);
            switchTab(newTab.id);
        }

        function closeTabById(id) {
            if (tabs.length === 1) {
                tabs[0].name = 'new 1';
                tabs[0].content = '';
                editor.value = '';
                renderTabs();
                syncEditor();
                return;
            }

            const index = tabs.findIndex(t => t.id === id);
            tabs = tabs.filter(t => t.id !== id);

            if (activeTabId === id) {
                const nextIndex = Math.max(0, index - 1);
                activeTabId = tabs[nextIndex].id;
                editor.value = tabs[nextIndex].content;
            }

            renderTabs();
            syncEditor();
        }

        function closeCurrentTab() {
            closeTabById(activeTabId);
        }

        function syncEditor() {
            const text = editor.value;
            const currentTab = getCurrentTab();
            if (currentTab) {
                currentTab.content = text;
            }

            const lineCount = text.split('\n').length;
            const currentLinesInGutter = lineNumbers.textContent.split('\n').length;

            if (lineCount !== currentLinesInGutter) {
                let linesStr = '';
                for (let i = 1; i <= lineCount; i++) {
                    linesStr += i + '\n';
                }
                lineNumbers.textContent = linesStr.slice(0, -1);
            }

            lineNumbers.scrollTop = editor.scrollTop;

            const charCount = text.length;
            const fileExt = currentTab ? currentTab.name.split('.').pop().toLowerCase() : '';
            const docType = fileExt === 'v' ? 'Verilog source file' : fileExt === 'py' ? 'Python file' : 'Normal text file';
            statusMeta.innerText = `${docType}  length : ${charCount}  lines : ${lineCount}`;

            updateCaretInfo();
        }

        function updateCaretInfo() {
            const pos = editor.selectionStart;
            const text = editor.value.substring(0, pos);
            const lines = text.split('\n');
            const row = lines.length;
            const col = lines[lines.length - 1].length + 1;
            const selLen = Math.abs(editor.selectionEnd - editor.selectionStart);
            caretPos.innerText = `Ln : ${row}  Col : ${col}  Sel : ${selLen}`;
        }

        editor.addEventListener('scroll', () => {
            lineNumbers.scrollTop = editor.scrollTop;
        });

        editor.addEventListener('input', syncEditor);
        editor.addEventListener('click', updateCaretInfo);
        editor.addEventListener('keyup', updateCaretInfo);

        editor.addEventListener('keydown', (e) => {
            if (e.key === 'Tab') {
                e.preventDefault();
                const start = editor.selectionStart;
                const end = editor.selectionEnd;
                editor.value = editor.value.substring(0, start) + '    ' + editor.value.substring(end);
                editor.selectionStart = editor.selectionEnd = start + 4;
                syncEditor();
            } else if ((e.ctrlKey || e.metaKey) && e.key.toLowerCase() === 's') {
                e.preventDefault();
                exportCurrentTab();
            }
        });

        function adjustZoom(direction) {
            fontZoomPx = Math.max(10, Math.min(28, fontZoomPx + direction));
            editor.style.fontSize = fontZoomPx + 'px';
            lineNumbers.style.fontSize = fontZoomPx + 'px';
        }

        function exportCurrentTab() {
            const current = getCurrentTab();
            if (!current) return;
            const blob = new Blob([editor.value], { type: 'text/plain;charset=utf-8' });
            const a = document.createElement('a');
            a.download = current.name;
            a.href = URL.createObjectURL(blob);
            a.style.display = 'none';
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(a.href);
        }

        function triggerFileInput(e) {
            if (e) e.stopPropagation();
            document.getElementById('fileLoader').click();
        }

        function handleFileImport(event) {
            const file = event.target.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = function(e) {
                createNewTab(file.name, e.target.result);
            };
            reader.readAsText(file);
            event.target.value = '';
        }

        async function executeEditorCommand(cmd) {
            editor.focus();
            if (cmd === 'copy') {
                const sel = editor.value.substring(editor.selectionStart, editor.selectionEnd);
                if (sel) await navigator.clipboard.writeText(sel);
            } else if (cmd === 'cut') {
                const sel = editor.value.substring(editor.selectionStart, editor.selectionEnd);
                if (sel) {
                    await navigator.clipboard.writeText(sel);
                    const start = editor.selectionStart;
                    editor.value = editor.value.substring(0, start) + editor.value.substring(editor.selectionEnd);
                    editor.selectionStart = editor.selectionEnd = start;
                    syncEditor();
                }
            } else if (cmd === 'paste') {
                try {
                    const text = await navigator.clipboard.readText();
                    const start = editor.selectionStart;
                    editor.value = editor.value.substring(0, start) + text + editor.value.substring(editor.selectionEnd);
                    editor.selectionStart = editor.selectionEnd = start + text.length;
                    syncEditor();
                } catch (err) {}
            }
        }

        // Window drag & resize engine
        const header = document.getElementById('windowDragHeader');
        const rHandle = document.getElementById('resizableHandle');
        let isDragging = false, isResizing = false;
        let startX, startY, startW, startH, startLeft, startTop;

        header.addEventListener('mousedown', (e) => {
            if (win.classList.contains('maximized') || e.target.closest('.npp-controls')) return;
            isDragging = true;
            startX = e.clientX;
            startY = e.clientY;
            startLeft = win.offsetLeft;
            startTop = win.offsetTop;
            document.body.style.userSelect = 'none';
        });

        rHandle.addEventListener('mousedown', (e) => {
            isResizing = true;
            startX = e.clientX;
            startY = e.clientY;
            startW = win.clientWidth;
            startH = win.clientHeight;
            document.body.style.userSelect = 'none';
            e.stopPropagation();
            e.preventDefault();
        });

        document.addEventListener('mousemove', (e) => {
            if (isDragging) {
                const nextX = startLeft + (e.clientX - startX);
                const nextY = startTop + (e.clientY - startY);
                win.style.left = Math.max(0, Math.min(window.innerWidth - 100, nextX)) + 'px';
                win.style.top = Math.max(0, Math.min(window.innerHeight - 50, nextY)) + 'px';
            } else if (isResizing) {
                win.style.width = Math.max(480, startW + (e.clientX - startX)) + 'px';
                win.style.height = Math.max(320, startH + (e.clientY - startY)) + 'px';
            }
        });

        document.addEventListener('mouseup', () => {
            isDragging = false;
            isResizing = false;
            document.body.style.userSelect = 'auto';
        });

        function toggleMaximize(e) {
            if (e) e.stopPropagation();
            win.classList.toggle('maximized');
        }

        function minimizeSimulation() {
            win.style.display = 'none';
            setTimeout(() => {
                alert('Window minimized. Click OK to restore.');
                win.style.display = 'flex';
            }, 250);
        }

        function hideNotepad() {
            win.style.display = 'none';
        }

        const initial = getCurrentTab();
        editor.value = initial ? initial.content : '';
        renderTabs();
        syncEditor();
    </script>
</body>
</html>
