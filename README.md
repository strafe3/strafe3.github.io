<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Content / UG26FA Digital Systems (EE-4322-01) - Notepad++ Overlay</title>
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
            font-family: "Open Sans", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
            background-color: #f0f0f0;
        }

        /* --- Full Webpage Background Canvas (Blackboard Ultra Replica) --- */
        #pageBackground {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow-y: auto;
            background-color: #ffffff;
            z-index: 1;
            user-select: text;
        }

        .bb-top-header {
            background-color: #262626;
            color: #ffffff;
            height: 47px;
            display: flex;
            align-items: center;
            padding: 0 16px;
            gap: 16px;
            font-size: 14px;
            border-bottom: 1px solid #404040;
        }

        .bb-top-header a {
            color: inherit;
            text-decoration: none;
            display: flex;
            align-items: center;
        }

        .bb-nav-tabs {
            background-color: #262626;
            display: flex;
            padding: 0 16px;
            border-bottom: 1px solid #8c8c8c;
            gap: 20px;
        }

        .bb-nav-tab {
            color: #cdcdcd;
            font-size: 14px;
            padding: 12px 2px;
            text-decoration: none;
            border-bottom: 4px solid transparent;
        }

        .bb-nav-tab.active {
            color: #ffffff;
            font-weight: 600;
            border-bottom-color: #c56fd5;
        }

        .bb-banner {
            background: linear-gradient(135deg, #1b1b1b 0%, #2f2f2f 100%);
            min-height: 140px;
            position: relative;
            display: flex;
            align-items: flex-end;
            padding: 24px;
            color: #ffffff;
        }

        .bb-banner h1 {
            margin: 0;
            font-size: 24px;
            font-weight: 400;
        }

        .bb-main-layout {
            display: flex;
            max-width: 1400px;
            margin: 0 auto;
            padding: 24px;
            gap: 32px;
        }

        .bb-content-col {
            flex: 1;
            min-width: 0;
        }

        .bb-sidebar-col {
            width: 320px;
            flex-shrink: 0;
        }

        .bb-section-title {
            font-size: 18px;
            font-weight: 600;
            color: #262626;
            margin: 0 0 16px 0;
            padding-bottom: 8px;
            border-bottom: 1px solid #e5e5e5;
        }

        .bb-folder-card {
            background: #ffffff;
            border: 1px solid #e5e5e5;
            border-radius: 4px;
            padding: 16px;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
            cursor: pointer;
        }

        .bb-folder-card:hover {
            background-color: #fbfbfb;
            border-color: #cdcdcd;
        }

        .bb-folder-left {
            display: flex;
            align-items: center;
            gap: 12px;
            color: #262626;
            font-weight: 600;
            font-size: 15px;
        }

        .bb-folder-icon {
            width: 22px;
            height: 22px;
            fill: #707070;
        }

        .bb-sidebar-card {
            background: #ffffff;
            border: 1px solid #e5e5e5;
            border-radius: 4px;
            padding: 16px;
            margin-bottom: 16px;
        }

        .bb-faculty-row {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .bb-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: #666;
            color: #fff;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        /* --- Floating Notepad++ Desktop Window Engine --- */
        .npp-window {
            position: absolute;
            top: 75px;
            left: 120px;
            width: 860px;
            height: 560px;
            background-color: #FFFFFF;
            border: 1px solid #707070;
            box-shadow: 0 14px 35px rgba(0, 0, 0, 0.45);
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
            box-shadow: 0px 4px 8px rgba(0,0,0,0.15);
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

        /* Notepad++ Multi-Tab Bar */
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

        /* Editor Area */
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

    <!-- Native File Explorer Hook -->
    <input type="file" id="fileLoader" style="position:absolute; width:1px; height:1px; opacity:0; z-index:-1;" onchange="handleFileImport(event)">

    <!-- BACKDROP WEBPAGE: Blackboard Course Outline -->
    <div id="pageBackground">
        <header class="bb-top-header">
            <span><strong>Courses</strong></span>
            <span>|</span>
            <span>UG26FA Digital Systems (EE-4322-01)</span>
            <span style="margin-left: auto; background: #c56fd5; color: #262626; font-size: 11px; padding: 2px 8px; border-radius: 12px; font-weight: bold;">OPEN</span>
        </header>

        <nav class="bb-nav-tabs">
            <a href="#" class="bb-nav-tab active">Content</a>
            <a href="#" class="bb-nav-tab">Calendar</a>
            <a href="#" class="bb-nav-tab">Announcements (6)</a>
            <a href="#" class="bb-nav-tab">Discussions</a>
            <a href="#" class="bb-nav-tab">Gradebook</a>
            <a href="#" class="bb-nav-tab">Messages (1)</a>
            <a href="#" class="bb-nav-tab">Groups</a>
        </nav>

        <div class="bb-banner">
            <h1>UG26FA Digital Systems (EE-4322-01)</h1>
        </div>

        <div class="bb-main-layout">
            <main class="bb-content-col">
                <div class="bb-section-title">Course Content</div>

                <div class="bb-folder-card">
                    <div class="bb-folder-left">
                        <svg class="bb-folder-icon" viewBox="0 0 24 24"><path d="M10 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V8c0-1.1-.9-2-2-2h-8l-2-2z"/></svg>
                        <span>Syllabus & Course Information</span>
                    </div>
                    <span>▾</span>
                </div>

                <div class="bb-folder-card">
                    <div class="bb-folder-left">
                        <svg class="bb-folder-icon" viewBox="0 0 24 24"><path d="M10 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V8c0-1.1-.9-2-2-2h-8l-2-2z"/></svg>
                        <span>Projects, Homeworks, & Labs</span>
                    </div>
                    <span>▾</span>
                </div>

                <div class="bb-folder-card">
                    <div class="bb-folder-left">
                        <svg class="bb-folder-icon" viewBox="0 0 24 24"><path d="M10 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V8c0-1.1-.9-2-2-2h-8l-2-2z"/></svg>
                        <span>Lecture Materials</span>
                    </div>
                    <span>▾</span>
                </div>
            </main>

            <aside class="bb-sidebar-col">
                <div class="bb-sidebar-card">
                    <div class="bb-section-title">Course Faculty</div>
                    <div class="bb-faculty-row">
                        <div class="bb-avatar">TG</div>
                        <div>
                            <div style="font-weight: 600;">Timothy Gilmour</div>
                            <div style="font-size: 12px; color: #666;">Instructor</div>
                        </div>
                    </div>
                </div>

                <div class="bb-sidebar-card">
                    <div class="bb-section-title">Details & Actions</div>
                    <ul style="list-style: none; padding: 0; margin: 0; font-size: 13px; line-height: 2;">
                        <li>👥 Roster - View everyone in your course</li>
                        <li>ℹ️ Course Description</li>
                        <li>📅 Attendance - View your attendance</li>
                        <li>🔧 Books & Tools</li>
                    </ul>
                </div>
            </aside>
        </div>
    </div>

    <!-- FOREGROUND: Notepad++ Window Matrix -->
    <div class="npp-window" id="windowContainer">
        <div class="npp-titlebar" id="windowDragHeader">
            <span id="windowTitle">basic_test.py - Notepad++</span>
            <div class="npp-controls">
                <span onclick="minimizeSimulation()">━</span>
                <span onclick="toggleMaximize(event)">🗖</span>
                <span onclick="hideNotepad()">✕</span>
            </div>
        </div>
        
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

        <div class="npp-tabs-bar">
            <div class="tab-list" id="tabList"></div>
            <button class="tab-add-btn" title="New file" onclick="createNewTab()">+</button>
        </div>

        <div class="npp-editor-container">
            <div class="npp-linenumbers" id="lineNumbers">1</div>
            <div class="npp-foldmargin"></div>
            <textarea class="npp-textarea" id="editor" spellcheck="false" wrap="off"></textarea>
            <div class="resize-handle" id="resizableHandle"></div>
        </div>

        <div class="npp-statusbar">
            <span id="statusFileMeta">Normal text file  length : 0  lines : 1</span>
            <div class="npp-status-right">
                <span id="caretPos">Ln : 1  Col : 1  Sel : 0</span>
                <span>Windows (CRLF)</span>
                <span>UTF-8</span>
                <span>INS</span>
            </div>
        </div>
    </div>

    <script>
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

            // Dynamically calculate and paint lines
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

        // Window dragging & resizing logic
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
            }, 300);
        }

        function hideNotepad() {
            win.style.display = 'none';
        }

        // Initialize state
        const initial = getCurrentTab();
        editor.value = initial ? initial.content : '';
        renderTabs();
        syncEditor();
    </script>
</body>
</html>
