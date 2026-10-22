<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Notepad++ Web Framework</title>
    <style>
        /* Classic Windows Desktop Accent Canvas Background */
        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            background-color: #55769A; 
            margin: 0;
            padding: 0;
            height: 100vh;
            overflow: hidden;
        }

        /* Resizable Windows Sub-Frame */
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
            border-radius: 4px;
            overflow: hidden;
            min-width: 450px;
            min-height: 300px;
        }

        /* Fullscreen Maximize State Modifier */
        .npp-window.maximized {
            top: 0 !important;
            left: 0 !important;
            width: 100vw !important;
            height: 100vh !important;
            border: none;
            border-radius: 0;
        }

        /* App Title Drag bar tracking track */
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
        }
        .npp-controls { display: flex; gap: 14px; font-size: 11px; padding-right: 4px; }
        .npp-controls span { cursor: pointer; }

        /* Classic Menu Options Links Row */
        .npp-menubar {
            background-color: #F0F0F0;
            padding: 2px 6px;
            display: flex;
            gap: 12px;
            font-size: 11.5px;
            color: #000000;
            user-select: none;
        }
        .menu-item { position: relative; cursor: pointer; padding: 1px 4px; }
        .menu-item:hover { background-color: #E5E5E5; }
        
        /* Menu Action Dropdowns */
        .dropdown-content {
            display: none;
            position: absolute;
            top: 100%; left: 0;
            background-color: #F9F9F9;
            min-width: 140px;
            box-shadow: 0px 4px 8px rgba(0,0,0,0.15);
            border: 1px solid #CCCCCC;
            z-index: 10;
        }
        .dropdown-content div { padding: 6px 12px; font-size: 11.5px; color: #000000; text-align: left; }
        .dropdown-content div:hover { background-color: #007ACC; color: white; }
        .menu-item:hover .dropdown-content { display: block; }

        /* Toolbar Icon Strip Elements */
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
        .icon-group { display: flex; border-right: 1px solid #D0D0D0; padding-right: 6px; margin-right: 4px; gap: 5px; }
        
        .t-btn {
            font-size: 13px; cursor: pointer; padding: 3px; border-radius: 2px;
            display: flex; align-items: center; justify-content: center; width: 16px; height: 16px;
        }
        .t-btn:hover { background-color: #DCDCDC; border: 1px solid #ABABAB; padding: 2px; }

        /* Active Workspace File Header Tabs */
        .npp-tabs { background-color: #F0F0F0; display: flex; padding-top: 3px; border-bottom: 1px solid #CCCCCC; }
        .npp-tab {
            background-color: #FFFFFF; color: #000000; padding: 4px 14px; font-size: 11.5px;
            border-top: 3px solid #FF3B30; border-left: 1px solid #CCCCCC; border-right: 1px solid #CCCCCC;
            border-radius: 2px 2px 0 0; display: flex; align-items: center; gap: 8px;
        }

        /* Main Editor View Panels Layout grid */
        .npp-editor-container { display: flex; flex: 1; overflow: hidden; position: relative; }

        .npp-linenumbers {
            background-color: #ECE9D8; color: #555555; font-family: 'Consolas', monospace;
            font-size: 13px; padding: 6px 5px; text-align: right; min-width: 32px; user-select: none;
            border-right: 1px solid #A0A0A0; line-height: 1.5;
        }
        .npp-foldmargin { background-color: #F0F0F0; width: 14px; border-right: 1px solid #D0D0D0; }

        .npp-textarea {
            flex: 1; background-color: #FFFFFF; color: #000000; font-family: 'Consolas', monospace;
            font-size: 13px; padding: 6px 8px; line-height: 1.5; outline: none;
            overflow-y: auto; white-space: pre; word-wrap: normal;
        }

        /* Syntax Highlighter Colors Token Registry */
        .py-keyword { color: #0000FF; font-weight: bold; }
        .py-string { color: #804000; }
        .py-number { color: #FF0000; }
        .py-builtin { color: #000080; }

        /* Bottom Application Status Info Ribbon */
        .npp-statusbar {
            background-color: #F0F0F0; color: #000000; padding: 3px 10px; font-size: 11.5px;
            display: flex; justify-content: space-between; border-top: 1px solid #CCCCCC; user-select: none;
        }
        .npp-status-right span { border-left: 1px solid #CCCCCC; padding: 0 12px; }

        /* Window Corner Scale Active Handle Point Layout */
        .resize-handle {
            position: absolute; width: 12px; height: 12px; right: 0; bottom: 0;
            cursor: se-resize; z-index: 20; background: linear-gradient(135deg, transparent 4px, #999 4px);
        }
    </style>
</head>
<body>

    <!-- Hidden Native OS File Selection Anchor Pipe -->
    <input type="file" id="fileLoader" style="display: none;" onchange="handleFileImport(event)">

    <!-- Main Workspace Container Interface Layout -->
    <div class="npp-window" id="windowContainer">
        
        <!-- Application Title Bar Layout Line Header -->
        <div class="npp-titlebar" id="windowDragHeader">
            <span id="windowTitle">*C:\Users\colemann\Documents\basic_test.py - Notepad++</span>
            <div class="npp-controls">
                <span>━</span><span onclick="toggleMaximize()">🗖</span><span onclick="alert('Close event simulation.')">✕</span>
            </div>
        </div>
        
        <!-- Nested Dropdown Navigation Options Matrix -->
        <div class="npp-menubar">
            <div class="menu-item">File
                <div class="dropdown-content">
                    <div onclick="clearWorkspace()">New</div>
                    <div onclick="triggerFileInput()">Open...</div>
                    <div onclick="exportTextAsFile()">Save</div>
                </div>
            </div>
            <div class="menu-item">Edit</div><div class="menu-item">Search</div><div class="menu-item">View</div>
            <div class="menu-item">Encoding</div><div class="menu-item">Language</div><div class="menu-item">Settings</div>
            <div class="menu-item">Tools</div><div class="menu-item">Macro</div><div class="menu-item">Run</div>
        </div>

        <!-- Custom Application Toolbar Button Strip Row -->
        <div class="npp-toolbar">
            <div class="icon-group">
                <div class="t-btn" title="New file" onclick="clearWorkspace()">📄</div>
                <div class="t-btn" title="Open file (Upload)" onclick="triggerFileInput()">📂</div>
                <div class="t-btn" title="Save file (Download - Ctrl+S)" onclick="exportTextAsFile()">💾</div>
                <div class="t-btn" title="Close document">❌</div>
            </div>
            <div class="icon-group">
                <div class="t-btn" title="Cut">✂️</div><div class="t-btn" title="Copy">📋</div><div class="t-btn" title="Undo">🔄</div><div class="t-btn" title="Search">🔍</div>
            </div>
            <div class="icon-group">
                <div class="t-btn" title="Zoom In" onclick="adjustZoom(1)">➕</div>
                <div class="t-btn" title="Zoom Out" onclick="adjustZoom(-1)">➖</div>
            </div>
        </div>

        <!-- Active Folder/Tab Heading Status Row -->
        <div class="npp-tabs">
            <div class="npp-tab">💾 <span id="tabHeadingName">basic_test.py</span></div>
        </div>

        <!-- Primary Text Workspace Panels Grid -->
        <div class="npp-editor-container">
            <div class="npp-linenumbers" id="lineNumbers">1<br>2<br>3<br>4<br>5<br>6<br>7<br>8</div>
            <div class="npp-foldmargin"></div>
            <div class="npp-textarea" id="editor" contenteditable="true" spellcheck="false" oninput="processHighlighting()">import numpy as np

apple_count = 4

if apple_count >= 5:
    print("You have enough")

print("Program end")</div>
        </div>

        <!-- Lower Panel Tracking Metadata Strip -->
        <div class="npp-statusbar">
            <span id="statusFileMeta">Python  length : 115  lines : 8</span>
            <div class="npp-status-right">
                <span>Ln : 8  Col : 21</span><span>Windows (CRLF)</span><span>UTF-8</span><span>INS</span>
            </div>
        </div>

        <!-- Resizing Trigger Corner Element Handle Layout -->
        <div class="resize-handle" id="resizableHandle"></div>
    </div>

    <script>
        let targetFileName = "basic_test.py";
        let fontZoomPx = 13;

        // --- Stream File Out To Client Machine ---
        function exportTextAsFile() {
            const currentCode = document.getElementById('editor').innerText;
            const blob = new Blob([currentCode], { type: "text/plain;charset=utf-8" });
            const a = document.createElement("a");
            
            a.download = targetFileName;
            a.href = URL.createObjectURL(blob);
Use code with caution.
a.style.display = "none";
document.body.appendChild(a);
a.click();
document.body.removeChild(a);
}
// Global Shortcut Command Binder
document.addEventListener('keydown', (e) => {
if ((e.ctrlKey || e.metaKey) && e.key === 's') {
e.preventDefault();
exportTextAsFile();
}
});
function triggerFileInput() { document.getElementById('fileLoader').click(); }
function clearWorkspace() {
document.getElementById('editor').innerText = "";
targetFileName = "new_1.txt";
document.getElementById('tabHeadingName').innerText = targetFileName;
document.getElementById('windowTitle').innerText = ${targetFileName} - Notepad++;
processHighlighting();
}
// --- Stream In Local Script File Data Async ---
function handleFileImport(event) {
const file = event.target.files[0];
if (!file) return;
targetFileName = file.name;
document.getElementById('tabHeadingName').innerText = targetFileName;
document.getElementById('windowTitle').innerText = ${targetFileName} - Notepad++;
const reader = new FileReader();
reader.onload = function(e) {
document.getElementById('editor').innerText = e.target.result;
processHighlighting();
};
reader.readAsText(file);
}
function adjustZoom(direction) {
fontZoomPx = Math.max(10, Math.min(30, fontZoomPx + direction));
document.getElementById('editor').style.fontSize = fontZoomPx + "px";
document.getElementById('lineNumbers').style.fontSize = fontZoomPx + "px";
}
// --- Realtime Client Python Syntax Token Parser Regex Engine ---
function processHighlighting() {
const editor = document.getElementById('editor');
let text = editor.innerText;
let highlighted = text
.replace(/&/g, "&").replace(/</g, "<").replace(/>/g, ">")
.replace(/\b(import|as|if|elif|else|for|while|def|return|class)\b/g, '$1')
.replace(/\b(print|len|range|str|int|float|list|dict)\b/g, '$1')
.replace(/("[^"]")|('[^']')/g, '$1')
.replace(/\b(\d+)\b/g, '$1');
editor.innerHTML = highlighted;
const linesCount = text.split('\n').length;
document.getElementById('lineNumbers').innerHTML = Array.from({length: linesCount}, (_, i) => i + 1).join('
');
document.getElementById('statusFileMeta').innerText = Python  length : ${text.length}  lines : ${linesCount};
}
// --- Absolute Coordinate Window Drag & Resize Tracking Engine ---
const win = document.getElementById('windowContainer');
const header = document.getElementById('windowDragHeader');
const rHandle = document.getElementById('resizableHandle');
let isDragging = false, isResizing = false;
let startX, startY, startW, startH, startLeft, startTop;
header.addEventListener('mousedown', (e) => {
if(win.classList.contains('maximized') || e.target.tagName === 'SPAN') return;
isDragging = true;
startX = e.clientX; startY = e.clientY;
startLeft = win.offsetLeft; startTop = win.offsetTop;
document.body.style.userSelect = 'none';
});
rHandle.addEventListener('mousedown', (e) => {
isResizing = true;
startX = e.clientX; startY = e.clientY;
startW = win.clientWidth; startH = win.clientHeight;
document.body.style.userSelect = 'none';
e.stopPropagation();
});
document.addEventListener('mousemove', (e) => {
if (isDragging) {
win.style.left = (startLeft + (e.clientX - startX)) + 'px';
win.style.top = (startTop + (e.clientY - startY)) + 'px';
} else if (isResizing) {
win.style.width = (startW + (e.clientX - startX)) + 'px';
win.style.height = (startH + (e.clientY - startY)) + 'px';
}
});
document.addEventListener('mouseup', () => {
isDragging = false; isResizing = false;
document.body.style.userSelect = 'auto';
});
function toggleMaximize() { win.classList.toggle('maximized'); }
window.addEventListener('DOMContentLoaded', processHighlighting);
