<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Notepad++ - Standard Web Interface</title>
    <style>
        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            background-color: #55769A;
            margin: 0;
            padding: 0;
            height: 100vh;
            overflow: hidden;
        }

        .npp-window {
            position: absolute;
            top: 40px;
            left: 40px;
            width: 850px;
            height: 550px;
            background-color: #FFFFFF;
            border: 1px solid #707070;
            box-shadow: 0 8px 24px rgba(0,0,0,0.3);
            display: flex;
            flex-direction: column;
            border-radius: 3px;
            overflow: hidden;
            min-width: 450px;
            min-height: 300px;
            box-sizing: border-box;
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
            padding: 2px 4px;
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
            min-width: 140px;
            box-shadow: 0px 4px 8px rgba(0,0,0,0.15);
            border: 1px solid #CCCCCC;
            z-index: 100;
        }

        .dropdown-content div {
            padding: 6px 12px;
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
            background-color: #Edf2f7;
            border: 1px solid #cbd5e0;
        }

        .t-btn svg {
            width: 14px;
            height: 14px;
            display: block;
        }

        .npp-tabs {
            background-color: #F0F0F0;
            display: flex;
            padding-top: 3px;
            border-bottom: 1px solid #CCCCCC;
        }

        .npp-tab {
            background-color: #FFFFFF;
            color: #000000;
            padding: 4px 14px;
            font-size: 11.5px;
            border-top: 3px solid #FF3B30;
            border-left: 1px solid #CCCCCC;
            border-right: 1px solid #CCCCCC;
            border-radius: 2px 2px 0 0;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .npp-tab svg {
            width: 11px;
            height: 11px;
        }

        .npp-editor-container {
            display: flex;
            flex: 1;
            overflow: hidden;
            position: relative;
        }

        .npp-linenumbers {
            background-color: #ECE9D8;
            color: #555555;
            font-family: 'Consolas', 'Courier New', monospace;
            font-size: 13px;
            padding: 6px 5px;
            text-align: right;
            min-width: 32px;
            user-select: none;
            border-right: 1px solid #A0A0A0;
            line-height: 1.5;
            white-space: pre;
        }

        .npp-foldmargin {
            background-color: #F0F0F0;
            width: 14px;
            border-right: 1px solid #D0D0D0;
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
            overflow-y: auto;
            white-space: pre;
            word-wrap: normal;
        }

        .py-keyword { color: #0000FF; font-weight: bold; }
        .py-string { color: #804000; }
        .py-number { color: #FF0000; }
        .py-builtin { color: #000080; }
        .py-comment { color: #008000; font-style: italic; }

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
            padding: 0 12px;
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

    <div class="npp-window" id="windowContainer">
        
        <div class="npp-titlebar" id="windowDragHeader">
            <span id="windowTitle">*C:\Users\Documents\basic_test.py - Notepad++</span>
            <div class="npp-controls">
                <span onclick="alert('Minimize window')">━</span>
                <span onclick="toggleMaximize(event)">🗖</span>
                <span onclick="alert('Close window')">✕</span>
            </div>
        </div>
        
        <div class="npp-menubar">
            <div class="menu-item">File
                <div class="dropdown-content">
                    <div onclick="clearWorkspace()">New</div>
                    <div onclick="triggerFileInput(event)">Open...</div>
                    <div onclick="exportTextAsFile()">Save</div>
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
                <div class="t-btn" title="New file" onclick="clearWorkspace()">
                    <svg viewBox="0 0 16 16" fill="none"><path d="M3 1h7l3 3v11H3V1z" stroke="#4A5568" stroke-width="1.5"/><path d="M10 1v3h3" stroke="#4A5568" stroke-width="1.5"/></svg>
                </div>
                <div class="t-btn" title="Open file" onclick="triggerFileInput(event)">
                    <svg viewBox="0 0 16 16" fill="none"><path d="M1.5 3.5h4l1.5 1.5h7.5v8.5h-13V3.5z" stroke="#D69E2E" stroke-width="1.5" fill="#FEFCBF"/><path d="M1.5 6.5h13" stroke="#D69E2E" stroke-width="1.5"/></svg>
                </div>
                <div class="t-btn" title="Save file (Ctrl+S)" onclick="exportTextAsFile()">
                    <svg viewBox="0 0 16 16" fill="none"><path d="M2 2h10l2 2v10H2V2z" fill="#3182CE" stroke="#2B6CB0"/><rect x="5" y="2" width="6" height="4" fill="#FFF"/><rect x="5" y="9" width="6" height="5" fill="#E2E8F0"/></svg>
                </div>
                <div class="t-btn" title="Close document" onclick="clearWorkspace()">
                    <svg viewBox="0 0 16 16" fill="none"><path d="M3 3l10 10M13 3L3 13" stroke="#E53E3E" stroke-width="2"/></svg>
                </div>
            </div>
            <div class="icon-group">
                <div class="t-btn" title="Cut" onclick="document.execCommand('cut')">
                    <svg viewBox="0 0 16 16" fill="none"><circle cx="4.5" cy="5.5" r="2" stroke="#4A5568" stroke-width="1.5"/><circle cx="4.5" cy="10.5" r="2" stroke="#4A5568" stroke-width="1.5"/><path d="M6.5 6.5l7 5.5M6.5 9.5l7-5.5" stroke="#4A5568" stroke-width="1.5"/></svg>
                </div>
                <div class="t-btn" title="Copy" onclick="document.execCommand('copy')">
                    <svg viewBox="0 0 16 16" fill="none"><rect x="4" y="4" width="9" height="10" stroke="#4A5568" stroke-width="1.5" fill="#FFF"/><path d="M3 11H2V2h9v1" stroke="#4A5568" stroke-width="1.5"/></svg>
                </div>
                <div class="t-btn" title="Paste" onclick="navigator.clipboard.readText().then(t => document.execCommand('insertText', false, t))">
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

        <div class="npp-tabs">
            <div class="npp-tab">
                <svg viewBox="0 0 16 16" fill="#FF3B30"><circle cx="8" cy="8" r="7"/></svg>
                <span id="tabHeadingName">basic_test.py</span>
            </div>
        </div>

        <div class="npp-editor-container">
            <div class="npp-linenumbers" id="lineNumbers">1</div>
            <div class="npp-foldmargin"></div>
            <div class="npp-textarea" id="editor" contenteditable="true" spellcheck="false">import numpy as np
# Initialize counter
apple_count = 4
if apple_count >= 5:
    print("You have enough")
else:
    print("Need more apples")
print("Program end")</div>
            <div class="resize-handle" id="resizableHandle"></div>
        </div>

        <div class="npp-statusbar">
            <span id="statusFileMeta">Python  length : 0  lines : 1</span>
            <div class="npp-status-right">
                <span id="caretPos">Ln : 1  Col : 1</span>
                <span>Windows (CRLF)</span>
                <span>UTF-8</span>
                <span>INS</span>
            </div>
        </div>
    </div>

    <script>
        let targetFileName = "basic_test.py";
        let fontZoomPx = 13;

        function exportTextAsFile() {
            const currentCode = document.getElementById('editor').innerText;
            const blob = new Blob([currentCode], { type: "text/plain;charset=utf-8" });
            const a = document.createElement("a");
            a.download = targetFileName;
            a.href = URL.createObjectURL(blob);
            a.style.display = "none";
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            URL.revokeObjectURL(a.href);
        }

        document.addEventListener('keydown', (e) => {
            if ((e.ctrlKey || e.metaKey) && e.key === 's') {
                e.preventDefault();
                exportTextAsFile();
            }
        });

        function triggerFileInput(e) {
            if (e) e.stopPropagation();
            document.getElementById('fileLoader').click();
        }

        function clearWorkspace() {
            document.getElementById('editor').innerText = "";
            targetFileName = "new_1.txt";
            document.getElementById('tabHeadingName').innerText = targetFileName;
            document.getElementById('windowTitle').innerText = `${targetFileName} - Notepad++`;
            processHighlighting();
        }

        function handleFileImport(event) {
            const file = event.target.files[0];
            if (!file) return;
            targetFileName = file.name;
            document.getElementById('tabHeadingName').innerText = targetFileName;
            document.getElementById('windowTitle').innerText = `${targetFileName} - Notepad++`;
            const reader = new FileReader();
            reader.onload = function(e) {
                document.getElementById('editor').innerText = e.target.result;
                processHighlighting();
            };
            reader.readAsText(file);
            event.target.value = '';
        }

        function adjustZoom(direction) {
            fontZoomPx = Math.max(10, Math.min(30, fontZoomPx + direction));
            document.getElementById('editor').style.fontSize = fontZoomPx + "px";
            document.getElementById('lineNumbers').style.fontSize = fontZoomPx + "px";
        }

        function escapeHtml(text) {
            return text
                .replace(/&/g, "&amp;")
                .replace(/</g, "&lt;")
                .replace(/>/g, "&gt;");
        }

        function processHighlighting() {
            const editor = document.getElementById('editor');
            const rawText = editor.innerText.replace(/\r\n/g, '\n');

            const linesCount = rawText.split('\n').length;
            document.getElementById('lineNumbers').textContent = Array.from({length: linesCount}, (_, i) => i + 1).join('\n');
            document.getElementById('statusFileMeta').innerText = `Python  length : ${rawText.length}  lines : ${linesCount}`;
        }

        const win = document.getElementById('windowContainer');
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
                let nextX = startLeft + (e.clientX - startX);
                let nextY = startTop + (e.clientY - startY);
                win.style.left = Math.max(0, Math.min(window.innerWidth - 100, nextX)) + 'px';
                win.style.top = Math.max(0, Math.min(window.innerHeight - 50, nextY)) + 'px';
            } else if (isResizing) {
                win.style.width = Math.max(450, startW + (e.clientX - startX)) + 'px';
                win.style.height = Math.max(300, startH + (e.clientY - startY)) + 'px';
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

        document.getElementById('editor').addEventListener('input', processHighlighting);

        window.addEventListener('DOMContentLoaded', processHighlighting);
    </script>
</body>
</html>
