<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Content / UG26FA Digital Systems (EE-4322-01)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Open Sans', Helvetica, Arial, sans-serif;
            background-color: #f8f8f8;
            color: #262626;
        }
        
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1; 
        }
        ::-webkit-scrollbar-thumb {
            background: #cdcdcd; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #a8a8a8; 
        }

        /* Header button hover shadow */
        .bb-header-btn {
            transition: all 300ms ease-in-out;
        }
        .bb-header-btn:hover {
            background-color: #000000;
            box-shadow: 0px 3px 1px -2px rgba(0,0,0,0.2), 0px 2px 2px 0px rgba(0,0,0,0.14), 0px 1px 5px 0px rgba(0,0,0,0.12);
        }

        /* Folder card shadow */
        .bb-folder-card {
            border: 1px solid #e5e5e5;
            box-shadow: 0px 2px 8px -2px rgba(0, 0, 0, 0.15);
            border-radius: 0.25rem;
            background-color: #ffffff;
        }

        /* Chevron Rotation */
        .accordion-item.is-open .chevron {
            transform: rotate(180deg);
        }

        /* Folder Contents Container */
        .accordion-content {
            display: none;
            padding: 0.5rem;
            padding-inline-start: 1.25rem;
            background-color: #ffffff;
            border-top: 1px solid #e5e5e5;
            border-radius: 0 0 0.25rem 0.25rem;
        }
        .accordion-item.is-open .accordion-content {
            display: block;
        }

        /* Nested Item Container */
        .bb-nested-item {
            min-height: 3.5rem;
            margin-inline-start: 0.625rem;
            border-radius: 0.25rem;
            display: flex;
            align-items: center;
            transition: background-color 150ms ease;
        }
        .bb-nested-item:hover {
            background-color: #EDF3FA;
        }
        .bb-nested-item .bb-meta{display:inline;margin-left:4px;font-size:12px;font-weight:400}
        .bb-more{margin-left:auto;align-self:flex-start;padding:2px 4px;color:#262626;font-size:20px;line-height:1;border-radius:4px}
        .bb-more:hover{background:#e5eaf0}

    /* ===== Notepad window ===== */
#np-win{position:fixed;z-index:1000;display:flex;flex-direction:column;container-type:inline-size;background:#fbfbfb;border:1px solid #c9ccd2;border-radius:9px;box-shadow:0 18px 48px rgba(0,0,0,.35),0 2px 8px rgba(0,0,0,.2);font:14px/1.2 "Segoe UI Variable Text","Segoe UI","Open Sans",system-ui,sans-serif;color:#1b1b1b;user-select:none;animation:npin .14s ease-out}
#np-win[hidden]{display:none}
@keyframes npin{from{opacity:0;transform:scale(.97)}}
#np-win.max{left:0!important;top:0!important;width:100vw!important;height:100vh!important;height:100dvh!important;border-radius:0;border:0}
#np-win svg{display:block;flex:none}
:where(#np-win button){background:none;border:0;color:inherit;font:inherit;cursor:default;padding:0}
.np-top{height:40px;display:flex;align-items:flex-end;background:#eef0f5;border-radius:9px 9px 0 0;padding-left:10px;flex:none}
#np-win.max .np-top{border-radius:0}
.np-app{align-self:center;width:34px;height:40px;margin-right:12px;display:inline-flex;align-items:center;justify-content:center}
.np-name{display:none;color:#252525;font-size:13px;line-height:20px;white-space:nowrap}
#np-win:has(.np-set:not([hidden])) .np-name{display:inline}
/* back arrow: title bar, far left, only while Settings is open */
.np-back{width:34px;height:34px;margin:0 4px 0 -2px;align-self:center;border-radius:5px;display:none;place-items:center}
#np-win:has(.np-set:not([hidden])) .np-back{display:grid}
.np-back:hover{background:rgba(0,0,0,.06)}
/* hide tab strip while Settings is open */
#np-win:has(.np-set:not([hidden])) .np-tabs,
#np-win:has(.np-set:not([hidden])) .np-add{display:none!important}
.np-tabs{display:flex;min-width:0;align-items:flex-end}
.np-tab{height:34px;display:flex;align-items:center;gap:8px;padding:0 6px 0 12px;min-width:110px;max-width:260px;flex:0 1 auto;border-radius:8px 8px 0 0;color:#555;position:relative}
.np-tab:not(.on)+.np-tab:not(.on),.np-tab:not(.on)+.np-add{border-left:1px solid #dfe2e9}
.np-tab:not(.on):hover{background:rgba(255,255,255,.55)}
.np-tab.on{background:#fbfbfb;color:#111;box-shadow:inset 1px 0 #dfe2e9,inset -1px 0 #dfe2e9,inset 0 1px #dfe2e9}
.np-tab .t{overflow:hidden;text-overflow:ellipsis;white-space:nowrap;flex:1}
/* Unsaved Dot styling */
.np-tab.dirty .t::after { content: " ●"; font-size: 10px; margin-left: 4px; vertical-align: middle; color: #1b1b1b; }

.np-tab .x{width:22px;height:22px;border-radius:4px;display:grid;place-items:center;visibility:hidden}
.np-tab.on .x,.np-tab:hover .x{visibility:visible}
.np-tab .x:hover,.np-add:hover{background:rgba(0,0,0,.07)}
.np-add{width:28px;height:28px;border-radius:5px;display:grid!important;place-items:center;margin:0 0 3px 6px}
.np-drag{flex:1;align-self:stretch;min-width:30px}
.np-wc{display:flex;align-self:flex-start;height:32px}
.np-wc button{width:46px;display:grid;place-items:center}
.np-wc button:hover{background:rgba(0,0,0,.06)}
.np-wc button.cl:hover{background:#c42b1c;color:#fff}
#np-win.max .np-wc button.cl{border-radius:0}
.np-wc button.cl{border-top-right-radius:8px}
.np-bar{height:38px;display:flex;align-items:center;padding:0 8px 0 0;flex:none;position:relative;border-bottom:1px solid transparent}
.np-bar>button.m{height:30px;padding:0 13px;border-radius:5px}
.np-bar button:hover,.np-bar button.on{background:rgba(0,0,0,.055)}
.np-tools{flex:1;display:flex;justify-content:center;align-items:center;gap:6px}
.np-tools button,.np-rt button{height:30px;min-width:32px;padding:0 8px;border-radius:5px;display:flex;align-items:center;justify-content:center;gap:4px}
.np-tools button.act,.np-rt button.act{background:rgba(0,0,0,.09)}
.np-rt{display:flex;align-items:center;gap:2px;margin-left:auto}
.np-tools:has(~.np-rt){margin-left:30px}
@container (max-width:640px){.np-tools{display:none}}

/* Floating Find/Pass styling based on image */
.np-body{flex:1;min-height:0;position:relative;border-top:1px solid #ececec}
.np-find,.np-pass{position:absolute;z-index:20;top:10px;left:50%;transform:translateX(-50%);display:flex;gap:4px;align-items:center;padding:6px 12px;background:#fdfdfd;border:1px solid #dcdcdc;border-radius:12px;box-shadow:0 4px 12px rgba(0,0,0,0.15)}
.np-find[hidden],.np-pass[hidden]{display:none}
.np-find input,.np-pass input{height:28px;border:1px solid transparent;border-bottom:2px solid #0067c0;border-radius:0;padding:0 8px;width:240px;background:#fff;user-select:text;font:inherit;outline:0}
.np-find input:focus,.np-pass input:focus{border-bottom-color:#0067c0}
.np-pass input.pq { padding-right: 70px; }
.np-find button,.np-pass button{height:28px;width:28px;display:flex;align-items:center;justify-content:center;border-radius:4px;background:transparent}
.np-find button:hover:not(:disabled),.np-pass button:hover:not(:disabled){background:#f0f0f0}
.np-find .bp,.np-find .bn, .np-pass .pb { margin-left: 2px; }
.np-find .bx, .np-pass .px { margin-left: 8px; }

/* Custom Modal */
.np-modal-overlay{position:absolute;inset:0;background:rgba(255,255,255,0.6);z-index:30;display:flex;align-items:center;justify-content:center}
.np-modal-overlay[hidden]{display:none}
.np-modal-box{background:#fbfbfb;border:1px solid #c9ccd2;border-radius:8px;padding:20px;box-shadow:0 8px 24px rgba(0,0,0,0.2);min-width:300px;display:flex;flex-direction:column;gap:12px}
.np-modal-box h3 { margin: 0; font-size: 15px; font-weight: 600; }
.np-modal-box input { height:32px; border:1px solid #8a8a8a; border-radius:4px; padding:0 8px; outline:0; font:inherit; }
.np-modal-box input:focus { border-color:#0067c0; border-bottom-width:2px; }
.np-modal-btns { display:flex; justify-content:flex-end; gap:8px; margin-top:8px; }
.np-modal-btns button { padding: 6px 16px; border-radius: 4px; border:1px solid #d6d6d6; background:#fff; cursor:pointer; }
.np-modal-btns button:hover { background:#f0f0f0; }
.np-modal-btns button.primary { background:#0067c0; color:#fff; border-color:#0067c0; }
.np-modal-btns button.primary:hover { background:#005a9e; }

.np-ed{position:absolute;inset:0;overflow:auto;padding:16px 18px;outline:0;font-family:var(--npf,Consolas,"Cascadia Mono",Inconsolata,"DejaVu Sans Mono",Menlo,monospace);font-size:16px;line-height:1.25;white-space:pre-wrap;overflow-wrap:anywhere;tab-size:4;user-select:text;cursor:text;color:#111;caret-color:#111}
.np-ed[hidden]{display:none}
#np-win.nw .np-ed{white-space:pre;overflow-wrap:normal}
.np-ed p,.np-ed div{margin:0;min-height:1.25em}
.np-ed h1{font-size:1.85em;font-weight:700;margin:.15em 0 .3em;line-height:1.2}
.np-ed h2{font-size:1.15em;font-weight:700;margin:.6em 0 .1em}
.np-ed h3{font-size:1em;font-weight:700;margin:.5em 0 .1em}
.np-ed ul{list-style:disc;padding-left:2.2em;margin:0}.np-ed ol{list-style:decimal;padding-left:2.2em;margin:0}
.np-ed b,.np-ed strong{font-weight:700}.np-ed i,.np-ed em{font-style:italic}
.np-ed a{color:#0a3d91;text-decoration:underline;cursor:text}
.np-st{height:32px;display:flex;align-items:center;font-size:12px;color:#444;padding:0 6px;border-top:1px solid #ececec;flex:none;border-radius:0 0 9px 9px}
.np-st[hidden]{display:none}
.np-st span{padding:0 11px;height:16px;line-height:16px;border-left:1px solid #d9d9d9;display:flex;align-items:center;gap:5px;white-space:nowrap}
.np-st span:first-child{border:0}.np-st .sp{flex:1;border:0}
.np-st .zm{min-width:56px}
.np-menu{position:absolute;z-index:5;min-width:290px;background:#d6d6d6;border:1px solid #c8c8c8;border-radius:8px;padding:4px;box-shadow:0 8px 24px rgba(0,0,0,.2)}
.np-menu .np-menu{display:none;left:100%;top:-5px;margin-left:2px}
.np-it{display:flex;align-items:center;height:32px;padding:0 10px 0 14px;border-radius:4px;position:relative;font-size:14px}
.np-it:hover:not(.off){background:rgba(0,0,0,.055)}
.np-it:hover>.np-menu{display:block}
.np-it.off{color:#9a9a9a}
.np-it .ic{display:none}.np-it .lb{flex:1;white-space:nowrap}.np-it .ky{color:#6b6b6b;font-size:12px;margin-left:24px}
.np-menu hr{border:0;border-top:1px solid #e6e6e6;margin:4px 2px}
.np-rs{position:absolute;z-index:3}
.np-rs[data-d=n],.np-rs[data-d=s]{left:8px;right:8px;height:6px;cursor:ns-resize}.np-rs[data-d=n]{top:-3px}.np-rs[data-d=s]{bottom:-3px}
.np-rs[data-d=e],.np-rs[data-d=w]{top:8px;bottom:8px;width:6px;cursor:ew-resize}.np-rs[data-d=e]{right:-3px}.np-rs[data-d=w]{left:-3px}
.np-rs[data-d=ne],.np-rs[data-d=nw],.np-rs[data-d=se],.np-rs[data-d=sw]{width:12px;height:12px}
.np-rs[data-d=ne]{top:-3px;right:-3px;cursor:nesw-resize}.np-rs[data-d=sw]{bottom:-3px;left:-3px;cursor:nesw-resize}
.np-rs[data-d=nw]{top:-3px;left:-3px;cursor:nwse-resize}.np-rs[data-d=se]{bottom:-3px;right:-3px;cursor:nwse-resize}
#np-win.max .np-rs{display:none}

/* ===== formatting is OFF by default: hide its UI unless .fmt is set ===== */
#np-win:not(.fmt) .np-tools,#np-win:not(.fmt) .np-st .fm{display:none}
/* right-hand icon group */
.np-rt button{position:relative}
.np-rt .dot{position:absolute;top:5px;right:7px;width:7px;height:7px;border-radius:50%;background:#0067c0}
.np-rt .mg.seen .dot{display:none}
.np-rt .acc{color:#7a7a7a}
/* ===== Settings page ===== */
.np-set{position:absolute;z-index:2;left:0;right:0;top:40px;bottom:0;overflow:auto;background:#f6f6f6;border-radius:0 0 9px 9px;cursor:default}
#np-win.max .np-set{border-radius:0}
.np-set[hidden]{display:none}
.ns-h{display:flex;align-items:center;gap:10px;padding:22px 24px 8px}
.ns-h h1{font-size:44px;font-weight:600;margin:0;letter-spacing:-.3px}
.ns-back{width:34px;height:34px;border-radius:5px;display:grid;place-items:center}
.ns-back:hover{background:rgba(0,0,0,.06)}
.ns-frow{display:flex;align-items:center;gap:14px;min-height:34px;font-size:13px}
.ns-frow>span{min-width:56px}
.ns-c{max-width:900px;padding:8px 24px 30px}
.ns-c h2{font-size:13px;font-weight:400;margin:16px 0 8px}
.ns-row{display:flex;align-items:center;gap:14px;min-height:62px;padding:10px 14px;margin-bottom:4px;background:#fdfdfd;border:1px solid #e6e6e6;border-radius:5px}
.ns-panel{margin-bottom:12px;background:#fdfdfd;border:1px solid #e6e6e6;border-radius:5px;overflow:hidden}
.ns-panel-head{display:flex;align-items:center;gap:14px;min-height:54px;padding:10px 14px;border-bottom:1px solid #e6e6e6}
.ns-panel .ns-panel-options{display:none}
.ns-panel.is-open .ns-panel-options{display:flex;flex-direction:column;gap:6px;padding:9px 14px 12px}
.ns-panel .ns-panel-head{cursor:pointer}
.ns-panel:not(.is-open) .ns-panel-head{border-bottom:0}
.ns-panel.is-open .ns-panel-head svg{transform:rotate(180deg)}
.ns-radio{display:flex;align-items:center;gap:9px;min-height:34px;font-size:13px}
.ns-radio input{appearance:none;width:18px;height:18px;margin:0;border:1px solid #767676;border-radius:50%;background:#fdfdfd;position:relative}
.ns-radio input:checked{border:2px solid #0067c0}
.ns-radio input:checked::after{content:"";position:absolute;inset:3px;border-radius:50%;background:#0067c0}
.ns-drop svg{transition:transform .15s}
.ns-drop[aria-expanded=true] svg{transform:rotate(180deg)}
.ns-detail{display:none;padding:10px 14px 12px 48px;background:#fdfdfd;border:1px solid #e6e6e6;border-top:0;border-radius:0 0 5px 5px;font-size:12px;color:#616161}
.ns-detail.is-open{display:block}
.ns-about{margin-top:28px}
.ns-about h2{font-size:16px;font-weight:600;margin:0 0 10px}
.ns-about p{font-size:14px;line-height:1.45;margin:0 0 2px}
.ns-about a{display:block;color:#185abc;font-size:14px;text-decoration:none;margin-top:16px}
.ns-about button{display:block;min-width:136px;height:36px;margin-top:18px;border:1px solid #d1d1d1;border-radius:5px;background:#fdfdfd;font:inherit;color:inherit}
.ns-ri{width:20px;display:grid;place-items:center;flex:none}
.ns-tx{flex:1;min-width:0;display:flex;flex-direction:column;gap:2px}
.ns-tx b{font-weight:400;font-size:14px}
.ns-tx span{font-size:12px;color:#616161}
.ns-ctl{display:flex;gap:8px;align-items:center}
.ns-row select,.ns-detail select{height:32px;min-width:150px;padding:0 8px;border:1px solid #d1d1d1;border-bottom-color:#8a8a8a;border-radius:4px;background:#fdfdfd;color:inherit;font:inherit;font-size:13px;cursor:pointer}
.ns-row select.sz,.ns-detail select.sz{min-width:72px}
.ns-tg{display:flex;align-items:center;gap:10px;font-size:13px}
.ns-tg i{position:relative;display:block;box-sizing:border-box;width:40px;height:20px;border-radius:10px;border:1px solid #6b6b6b}
.ns-tg i::after{content:"";position:absolute;top:50%;left:4px;width:12px;height:12px;margin-top:-6px;border-radius:50%;background:#5c5c5c;transition:left .12s}
.ns-tg[aria-checked=true] i{background:#0067c0;border-color:#0067c0}
.ns-tg[aria-checked=true] i::after{left:24px;background:#fff}

/* ===== Dark theme ===== */
#np-win.dark{background:#272727;border-color:#3d3d3d;color:#f3f3f3;color-scheme:dark}
#np-win.dark .np-top{background:#1f1f1f}
#np-win.dark .np-tab{color:#bdbdbd}
#np-win.dark .np-tab:not(.on):hover{background:rgba(255,255,255,.07)}
#np-win.dark .np-tab.on{background:#272727;color:#fff;box-shadow:inset 1px 0 #3a3a3a,inset -1px 0 #3a3a3a,inset 0 1px #3a3a3a}
#np-win.dark .np-tab .x:hover,#np-win.dark .np-add:hover{background:rgba(255,255,255,.1)}
#np-win.dark .np-tab.dirty .t::after { color: #fff; }
#np-win.dark .np-wc button:hover{background:rgba(255,255,255,.08)}
#np-win.dark .np-wc button.cl:hover{background:#c42b1c;color:#fff}
#np-win.dark .np-bar button:hover,#np-win.dark .np-bar button.on{background:rgba(255,255,255,.08)}
#np-win.dark .np-tools button.act,#np-win.dark .np-rt button.act{background:rgba(255,255,255,.14)}
#np-win.dark .np-rt .acc{color:#bdbdbd}
#np-win.dark .np-find,#np-win.dark .np-pass{background:#323232;border-color:#444;box-shadow:0 4px 12px rgba(0,0,0,0.5)}
#np-win.dark .np-find input,#np-win.dark .np-pass input{background:#1f1f1f;border-color:#444;border-bottom-color:#9a9a9a;color:#fff}
#np-win.dark .np-find button:hover:not(:disabled),#np-win.dark .np-pass button:hover:not(:disabled){background:#444}
#np-win.dark .np-modal-overlay{background:rgba(0,0,0,0.6)}
#np-win.dark .np-modal-box{background:#2b2b2b;border-color:#444}
#np-win.dark .np-modal-box input{background:#1f1f1f;color:#fff;border-color:#555}
#np-win.dark .np-modal-btns button{background:#323232;border-color:#555;color:#fff}
#np-win.dark .np-modal-btns button:hover{background:#444}
#np-win.dark .np-modal-btns button.primary{background:#0067c0;border-color:#0067c0}
#np-win.dark .np-modal-btns button.primary:hover{background:#005a9e}
#np-win.dark .np-body,#np-win.dark .np-st{border-top-color:#383838}
#np-win.dark .np-ed{color:#fff;caret-color:#fff}
#np-win.dark .np-ed a{color:#7cb7ff}
#np-win.dark .np-st{color:#c8c8c8}
#np-win.dark .np-st span{border-left-color:#444}
#np-win.dark .np-menu{background:#2b2b2b;border-color:#3d3d3d}
#np-win.dark .np-it:hover:not(.off){background:rgba(255,255,255,.08)}
#np-win.dark .np-it.off{color:#777}
#np-win.dark .np-it .ky{color:#a0a0a0}
#np-win.dark .np-menu hr{border-top-color:#404040}
#np-win.dark .np-set{background:#1c1c1c}
#np-win.dark .ns-row{background:#2b2b2b;border-color:#3a3a3a}
#np-win.dark .ns-tx span{color:#a8a8a8}
#np-win.dark .ns-row select,#np-win.dark .ns-detail select{background:#323232;border-color:#464646;border-bottom-color:#9a9a9a}
#np-win.dark .ns-back:hover,#np-win.dark .np-back:hover{background:rgba(255,255,255,.08)}
#np-win.dark .ns-tg i{border-color:#bdbdbd}
#np-win.dark .ns-tg i::after{background:#d0d0d0}
#np-win.dark .ns-tg[aria-checked=true] i{background:#4cc2ff;border-color:#4cc2ff}
#np-win.dark .ns-tg[aria-checked=true] i::after{background:#000}
#np-win.dark .ns-radio input{background:#2b2b2b;border-color:#bdbdbd}
#np-win.dark .ns-radio input:checked{border-color:#4cc2ff}
#np-win.dark .ns-radio input:checked::after{background:#4cc2ff}
#np-win.dark .ns-detail{background:#2b2b2b;border-color:#3a3a3a;color:#a8a8a8}
    </style>
</head>
<body class="antialiased flex flex-col min-h-screen">

    <!-- Top System Header -->
    <header class="bg-[#262626] text-white flex items-center justify-between px-4 h-[47px] border-b border-[#404040] z-50 w-full">
        <div class="flex items-center gap-2 w-full min-w-0">
            <!-- Home Button -->
            <a href="#" class="bb-header-btn bg-[#404040] text-white h-[28px] px-2 rounded-[4px] flex items-center justify-center focus:outline-none shrink-0" aria-label="Home">
                <svg class="w-4 h-4 fill-current" viewBox="0 0 16 16" aria-hidden="true">
                    <path d="M15.4619 14.4619c-.0002.8494-.6886 1.538-1.5381 1.5381h-3.7695c-.5522-.0001-1-.4478-1-1v-4.3076a.0773.0773 0 0 0-.0771-.0772H6.9238a.0773.0773 0 0 0-.0771.0772V15c0 .5523-.4477 1-1 1H2.0772c-.8495-.0002-1.538-.6888-1.5381-1.5381V6.3848c0-.2967.1314-.5786.3593-.7686L7.3604.2314l.0712-.0537a1 1 0 0 1 1.209.0537l6.4619 5.3848c.228.19.3594.4718.3594.7686zM11.1543 14h2.3076V6.8525L8 2.3018 2.539 6.8535V14h2.3077v-3.3076c0-1.1471.93-2.0772 2.0771-2.0772h2.1533c1.1471 0 2.0772.9301 2.0772 2.0772z"></path>
                </svg>
            </a>
            
            <!-- Courses Switcher Button -->
            <button type="button" class="bb-header-btn text-white h-[28px] px-2 rounded-[4px] flex items-center text-[14px] leading-none cursor-pointer shrink-0">
                <span>Courses</span>
                <span class="ml-1 -mr-0.5 mt-0.5">
                    <svg class="w-4 h-4 fill-current" viewBox="0 0 16 16" aria-hidden="true">
                        <path d="M12.5 5h-9L8 11z"></path>
                    </svg>
                </span>
            </button>
            
            <!-- Vertical Divider -->
            <div class="h-[22px] w-[1px] bg-[#404040] shrink-0" role="separator"></div>
            
            <!-- Course Title Button -->
            <a href="#" class="bb-header-btn text-white h-[28px] px-2 rounded-[4px] flex items-center min-w-0 truncate">
                <span class="text-[14px] font-normal truncate">UG26FA Digital Systems (EE-4322-01)</span>
            </a>

            <!-- Status Badge -->
            <div class="ml-auto flex items-center shrink-0 pl-2" title="Students can access this course">
                <span class="bg-white text-[#046df6] border border-[#046df6] text-[10px] font-bold px-2 py-[1px] rounded-[2rem] leading-[1.5] uppercase">Open</span>
            </div>
        </div>
    </header>

    <!-- Tab Navigation Bar -->
    <div class="bg-[#262626] text-[#e5e5e5] w-full overflow-x-auto z-40 px-4 min-h-[47px] flex items-center">
        <nav aria-label="course" class="w-full">
            <ul class="flex items-center h-[46px] text-[14px] space-x-6">
                <li class="h-full flex">
                    <a href="#" class="flex items-center pt-1 border-b-[4px] border-[#c56fd5] text-white font-semibold transition-colors">Content</a>
                </li>
                <li class="h-full flex">
                    <a href="#" class="flex items-center pt-1 text-[#e5e5e5] hover:text-[#e5e5e5] border-b-[4px] border-transparent hover:border-[#cdcdcd] transition-colors">Calendar</a>
                </li>
                <li class="h-full flex">
                    <a href="#" class="flex items-center pt-1 gap-1.5 text-[#e5e5e5] hover:text-[#e5e5e5] border-b-[4px] border-transparent hover:border-[#cdcdcd] transition-colors">
                        <span>Announcements</span>
                        <span class="bg-[#c56fd5] text-[#262626] text-[12px] font-semibold h-5 min-w-[20px] px-1.5 flex items-center justify-center rounded-full leading-none">6</span>
                    </a>
                </li>
                <li class="h-full flex">
                    <a href="#" class="flex items-center pt-1 text-[#e5e5e5] hover:text-[#e5e5e5] border-b-[4px] border-transparent hover:border-[#cdcdcd] transition-colors">Discussions</a>
                </li>
                <li class="h-full flex">
                    <a href="#" class="flex items-center pt-1 text-[#e5e5e5] hover:text-[#e5e5e5] border-b-[4px] border-transparent hover:border-[#cdcdcd] transition-colors">Gradebook</a>
                </li>
                <li class="h-full flex">
                    <a href="#" class="flex items-center pt-1 gap-1.5 text-[#e5e5e5] hover:text-[#e5e5e5] border-b-[4px] border-transparent hover:border-[#cdcdcd] transition-colors">
                        <span>Messages</span>
                        <span class="bg-[#c56fd5] text-[#262626] text-[12px] font-semibold h-5 min-w-[20px] px-1.5 flex items-center justify-center rounded-full leading-none">1</span>
                    </a>
                </li>
                <li class="h-full flex">
                    <a href="#" class="flex items-center pt-1 text-[#e5e5e5] hover:text-[#e5e5e5] border-b-[4px] border-transparent hover:border-[#cdcdcd] transition-colors">Groups</a>
                </li>
                <li class="h-full flex">
                    <a href="#" class="flex items-center pt-1 text-[#e5e5e5] hover:text-[#e5e5e5] border-b-[4px] border-transparent hover:border-[#cdcdcd] transition-colors">Achievements</a>
                </li>
            </ul>
        </nav>
    </div>

    <!-- Course Banner -->
    <div class="w-full relative bg-black h-[200px] overflow-hidden mb-6 select-none">
        <svg class="w-full h-full object-cover" viewBox="0 0 1440 200" preserveAspectRatio="none" aria-hidden="true">
            <defs>
                <linearGradient id="bgBase" x1="0%" y1="0%" x2="100%" y2="0%">
                    <stop offset="0%" stop-color="#4e2a4f" />
                    <stop offset="50%" stop-color="#472448" />
                    <stop offset="100%" stop-color="#532d54" />
                </linearGradient>
                <linearGradient id="bottomFade" x1="0%" y1="0%" x2="0%" y2="100%">
                    <stop offset="0%" stop-color="#000000" stop-opacity="0" />
                    <stop offset="35%" stop-color="#000000" stop-opacity="0.15" />
                    <stop offset="75%" stop-color="#000000" stop-opacity="0.78" />
                    <stop offset="100%" stop-color="#000000" stop-opacity="0.98" />
                </linearGradient>
            </defs>
            <rect width="1440" height="200" fill="url(#bgBase)" />
            <path d="M -50,-20 Q 240,155 550,-20 Z" fill="#653b66" opacity="0.55" />
            <polygon points="820,200 1015,-20 1440,-20 1440,200" fill="#5e355f" opacity="0.5" />
            <rect width="1440" height="200" fill="url(#bottomFade)" />
        </svg>

        <!-- Course Banner Title -->
        <div class="absolute inset-x-0 bottom-0 px-4 sm:px-6 lg:px-8 py-2 min-h-[54px] flex items-center">
            <h1 class="text-white text-[18px] lg:text-[24px] font-semibold lg:font-normal leading-[1.5]">
                UG26FA Digital Systems (EE-4322-01)
            </h1>
        </div>
    </div>

    <!-- Main Content Grid -->
    <main class="w-full flex flex-col lg:flex-row gap-6 px-4 sm:px-6 lg:px-8 pb-20 flex-grow">
        
        <!-- Left Column: Course Content -->
        <div class="flex-grow min-w-0">
            <!-- Header & Search -->
            <header class="flex justify-between items-center mb-3 mr-1 lg:mr-3.5">
                <h2 class="text-[16px] font-semibold text-[#262626]">Course Content</h2>
                <button class="w-10 h-10 flex items-center justify-center text-[#262626] hover:bg-gray-200 rounded-full transition-colors focus:outline-none" aria-label="Search course content">
                    <svg class="w-4 h-4 fill-current" viewBox="0 0 16 16">
                        <path fill-rule="evenodd" d="M6.5 0C2.9102 0 0 2.9101 0 6.5S2.9101 13 6.5 13c1.4341 0 2.7597-.4644 3.8347-1.2511l3.9582 3.9582c.3905.3905 1.0237.3905 1.4142 0s.3905-1.0237 0-1.4142l-3.9582-3.9582C12.5356 9.2597 13 7.9341 13 6.5 13 2.9102 10.0899 0 6.5 0M2 6.5C2 4.0147 4.0147 2 6.5 2S11 4.0147 11 6.5 8.9853 11 6.5 11 2 8.9853 2 6.5" clip-rule="evenodd"></path>
                    </svg>
                </button>
            </header>

            <!-- Accordion List -->
            <div class="flex flex-col space-y-3.5">
                
                <!-- Folder 1: Syllabus & Course Information -->
                <div class="bb-folder-card accordion-item">
                    <div class="p-2">
                        <button class="w-full flex items-center p-2 lg:p-4 focus:outline-none accordion-trigger group" aria-expanded="false">
                            <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                <!-- Standard Folder Icon -->
                                <svg class="w-6 h-6 fill-current folder-icon" viewBox="0 0 24 24" aria-label="Folder">
                                    <path fill-rule="evenodd" d="M2 3c0-.5523.4477-1 1-1h8.4375a1 1 0 0 1 .9238.6171l.8692 2.0972H21c.5523 0 1 .4477 1 1V21c0 .5523-.4477 1-1 1H3c-.5523 0-1-.4477-1-1zm2 1v16h16V6.7143h-7.4375a1 1 0 0 1-.9238-.6171L10.7695 4zm.6875 1.7143c0-.5523.4477-1 1-1h3.625c.5523 0 1 .4477 1 1s-.4477 1-1 1h-3.625c-.5523 0-1-.4477-1-1" clip-rule="evenodd"></path>
                                </svg>
                            </div>
                            <span class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline text-left">
                                Syllabus &amp; Course Information
                            </span>
                            <div class="ml-auto pl-4 text-[#666666] hover:text-[#262626]">
                                <svg class="w-4 h-4 fill-current transform transition-transform duration-200 chevron" viewBox="0 0 16 16" aria-hidden="true">
                                    <path fill-rule="evenodd" d="M.2929 3.2929c.3905-.3905 1.0237-.3905 1.4142 0L8 9.5858l6.2929-6.293c.3905-.3904 1.0237-.3904 1.4142 0 .3905.3906.3905 1.0238 0 1.4143l-7 7c-.3905.3905-1.0237.3905-1.4142 0l-7-7c-.3905-.3905-.3905-1.0237 0-1.4142" clip-rule="evenodd"></path>
                                </svg>
                            </div>
                        </button>
                    </div>
                    <!-- Expandable Folder Content -->
                    <div class="accordion-content">
                        <div class="bb-nested-item cursor-pointer group">
                            <div class="w-full flex items-start p-2 lg:p-4">
                                <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                    <!-- Document Icon -->
                                    <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document">
                                        <path fill-rule="evenodd" d="M4 3c0-.5523.4477-1 1-1h9.5858a1 1 0 0 1 .7071.2929l4.4142 4.4142a1 1 0 0 1 .2929.7071V21c0 .5523-.4477 1-1 1H5c-.5523 0-1-.4477-1-1V3zm2 1v16h12V8h-3c-.5523 0-1-.4477-1-1V4H6zm10 .4142L17.5858 6H16V4.4142zM8 10c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 4c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 3.5c0-.5523.4477-1 1-1h4c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1z" clip-rule="evenodd"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col min-w-0 flex-grow">
                                    <a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">_Syllabus_EE4322_Fall2026.docx</a><span class="bb-meta">updated September 30, 11:54am</span>
                                </div><button class="bb-more" type="button" aria-label="More options">...</button>
                            </div>
                        </div>
                        <div class="bb-nested-item cursor-pointer group"><div class="w-full flex items-start p-2 lg:p-4"><div class="text-[#262626] mr-2 flex-shrink-0 flex items-start"><svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document"><path fill-rule="evenodd" d="M4 3c0-.5523.4477-1 1-1h9.5858l4.4142 4.4142V21H4zm2 1v16h12V8h-3V4z" clip-rule="evenodd"></path></svg></div><div class="flex flex-col min-w-0 flex-grow"><a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">weekly_office_hours_Fall_2026.docx</a></div><button class="bb-more" type="button" aria-label="More options">...</button></div></div>
                        <div class="bb-nested-item cursor-pointer group"><div class="w-full flex items-start p-2 lg:p-4"><div class="text-[#262626] mr-2 flex-shrink-0 flex items-start"><svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document"><path fill-rule="evenodd" d="M4 3c0-.5523 1-1 1-1h9.5858l4.4142 4.4142V21H4zm2 1v16h12V8h-3V4z" clip-rule="evenodd"></path></svg></div><div class="flex flex-col min-w-0 flex-grow"><a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">Instructor Contact Information</a></div><button class="bb-more" type="button" aria-label="More options">...</button></div></div>
                        <div class="bb-nested-item cursor-pointer group"><div class="w-full flex items-start p-2 lg:p-4"><div class="text-[#262626] mr-2 flex-shrink-0 flex items-start"><svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document"><path fill-rule="evenodd" d="M4 3c0-.5523 1-1 1-1h9.5858l4.4142 4.4142V21H4zm2 1v16h12V8h-3V4z" clip-rule="evenodd"></path></svg></div><div class="flex flex-col min-w-0 flex-grow"><a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">Optional Blackboard Tutorial</a></div><button class="bb-more" type="button" aria-label="More options">...</button></div></div>
                    </div>
                </div>

                <!-- Folder 2: Projects, Homeworks, & Labs (Closed by default) -->
                <div class="bb-folder-card accordion-item">
                    <div class="p-2">
                        <button class="w-full flex items-center p-2 lg:p-4 focus:outline-none accordion-trigger group" aria-expanded="false">
                            <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                <!-- Standard Folder Icon -->
                                <svg class="w-6 h-6 fill-current folder-icon" viewBox="0 0 24 24" aria-label="Folder">
                                    <path fill-rule="evenodd" d="M2 3c0-.5523.4477-1 1-1h8.4375a1 1 0 0 1 .9238.6171l.8692 2.0972H21c.5523 0 1 .4477 1 1V21c0 .5523-.4477 1-1 1H3c-.5523 0-1-.4477-1-1zm2 1v16h16V6.7143h-7.4375a1 1 0 0 1-.9238-.6171L10.7695 4zm.6875 1.7143c0-.5523.4477-1 1-1h3.625c.5523 0 1 .4477 1 1s-.4477 1-1 1h-3.625c-.5523 0-1-.4477-1-1" clip-rule="evenodd"></path>
                                </svg>
                            </div>
                            <span class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline text-left">
                                Projects, Homeworks, &amp; Labs
                            </span>
                            <div class="ml-auto pl-4 text-[#666666] hover:text-[#262626]">
                                <svg class="w-4 h-4 fill-current transform transition-transform duration-200 chevron" viewBox="0 0 16 16" aria-hidden="true">
                                    <path fill-rule="evenodd" d="M.2929 3.2929c.3905-.3905 1.0237-.3905 1.4142 0L8 9.5858l6.2929-6.293c.3905-.3904 1.0237-.3904 1.4142 0 .3905.3906.3905 1.0238 0 1.4143l-7 7c-.3905.3905-1.0237.3905-1.4142 0l-7-7c-.3905-.3905-.3905-1.0237 0-1.4142" clip-rule="evenodd"></path>
                                </svg>
                            </div>
                        </button>
                    </div>

                    <!-- Expandable Folder Content -->
                    <div class="accordion-content">
                        
                        <!-- Sub-item 1: Miscellaneous Uploads spot -->
                        <div class="bb-nested-item cursor-pointer group">
                            <div class="w-full flex items-start p-2 lg:p-4">
                                <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                    <!-- Document Icon -->
                                    <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document">
                                        <path fill-rule="evenodd" d="M4 3c0-.5523.4477-1 1-1h9.5858a1 1 0 0 1 .7071.2929l4.4142 4.4142a1 1 0 0 1 .2929.7071V21c0 .5523-.4477 1-1 1H5c-.5523 0-1-.4477-1-1V3zm2 1v16h12V8h-3c-.5523 0-1-.4477-1-1V4H6zm10 .4142L17.5858 6H16V4.4142zM8 10c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 4c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 3.5c0-.5523.4477-1 1-1h4c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1z" clip-rule="evenodd"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col gap-[2px] min-w-0 flex-grow">
                                    <a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">
                                        Miscellaneous Uploads spot
                                    </a>
                                    <div class="text-[12px] text-[#262626] leading-[1.5]">
                                        No due date
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Sub-item 2: Format Guide -->
                        <div class="bb-nested-item cursor-pointer group">
                            <div class="w-full flex items-start p-2 lg:p-4">
                                <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                    <!-- Document Icon -->
                                    <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document">
                                        <path fill-rule="evenodd" d="M4 3c0-.5523.4477-1 1-1h9.5858a1 1 0 0 1 .7071.2929l4.4142 4.4142a1 1 0 0 1 .2929.7071V21c0 .5523-.4477 1-1 1H5c-.5523 0-1-.4477-1-1V3zm2 1v16h12V8h-3c-.5523 0-1-.4477-1-1V4H6zm10 .4142L17.5858 6H16V4.4142zM8 10c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 4c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 3.5c0-.5523.4477-1 1-1h4c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1z" clip-rule="evenodd"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col min-w-0 flex-grow">
                                    <a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">
                                        Format Guide
                                    </a>
                                </div>
                            </div>
                        </div>

                        <!-- Sub-item 3: Lab grammar checker -->
                        <div class="bb-nested-item cursor-pointer group">
                            <div class="w-full flex items-start p-2 lg:p-4">
                                <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                    <!-- Document Icon -->
                                    <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document">
                                        <path fill-rule="evenodd" d="M4 3c0-.5523.4477-1 1-1h9.5858a1 1 0 0 1 .7071.2929l4.4142 4.4142a1 1 0 0 1 .2929.7071V21c0 .5523-.4477 1-1 1H5c-.5523 0-1-.4477-1-1V3zm2 1v16h12V8h-3c-.5523 0-1-.4477-1-1V4H6zm10 .4142L17.5858 6H16V4.4142zM8 10c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 4c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 3.5c0-.5523.4477-1 1-1h4c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1z" clip-rule="evenodd"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col gap-[2px] min-w-0 flex-grow">
                                    <a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">
                                        Lab grammar checker
                                    </a>
                                    <div class="text-[12px] text-[#262626] leading-[1.5]">
                                        No due date
                                    </div>
                                    <div class="text-[12px] text-[#262626] leading-[1.4] mt-0.5">
                                        Lab grammar checker
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Sub-item 4: Lab 1 -->
                        <div class="bb-nested-item cursor-pointer group">
                            <div class="w-full flex items-start p-2 lg:p-4">
                                <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                    <!-- Document Icon -->
                                    <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document">
                                        <path fill-rule="evenodd" d="M4 3c0-.5523.4477-1 1-1h9.5858a1 1 0 0 1 .7071.2929l4.4142 4.4142a1 1 0 0 1 .2929.7071V21c0 .5523-.4477 1-1 1H5c-.5523 0-1-.4477-1-1V3zm2 1v16h12V8h-3c-.5523 0-1-.4477-1-1V4H6zm10 .4142L17.5858 6H16V4.4142zM8 10c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 4c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 3.5c0-.5523.4477-1 1-1h4c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1z" clip-rule="evenodd"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col min-w-0 flex-grow">
                                    <a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">
                                        Lab 1
                                    </a>
                                </div>
                            </div>
                        </div>

                        <!-- Sub-item 5: Lab 1 upload report here -->
                        <div class="bb-nested-item cursor-pointer group">
                            <div class="w-full flex items-start p-2 lg:p-4">
                                <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                    <!-- Document Icon -->
                                    <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document">
                                        <path fill-rule="evenodd" d="M4 3c0-.5523.4477-1 1-1h9.5858a1 1 0 0 1 .7071.2929l4.4142 4.4142a1 1 0 0 1 .2929.7071V21c0 .5523-.4477 1-1 1H5c-.5523 0-1-.4477-1-1V3zm2 1v16h12V8h-3c-.5523 0-1-.4477-1-1V4H6zm10 .4142L17.5858 6H16V4.4142zM8 10c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 4c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 3.5c0-.5523.4477-1 1-1h4c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1z" clip-rule="evenodd"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col gap-[2px] min-w-0 flex-grow">
                                    <a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">
                                        Lab 1 upload report here
                                    </a>
                                    <div class="text-[12px] text-[#262626] leading-[1.5]">
                                        No due date
                                    </div>
                                </div>
                            </div>
                        </div>

                    </div>
                </div>

                <!-- Folder 3: Lecture Materials -->
                <div class="bb-folder-card accordion-item">
                    <div class="p-2">
                        <button class="w-full flex items-center p-2 lg:p-4 focus:outline-none accordion-trigger group" aria-expanded="false">
                            <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                <!-- Standard Folder Icon -->
                                <svg class="w-6 h-6 fill-current folder-icon" viewBox="0 0 24 24" aria-label="Folder">
                                    <path fill-rule="evenodd" d="M2 3c0-.5523.4477-1 1-1h8.4375a1 1 0 0 1 .9238.6171l.8692 2.0972H21c.5523 0 1 .4477 1 1V21c0 .5523-.4477 1-1 1H3c-.5523 0-1-.4477-1-1zm2 1v16h16V6.7143h-7.4375a1 1 0 0 1-.9238-.6171L10.7695 4zm.6875 1.7143c0-.5523.4477-1 1-1h3.625c.5523 0 1 .4477 1 1s-.4477 1-1 1h-3.625c-.5523 0-1-.4477-1-1" clip-rule="evenodd"></path>
                                </svg>
                            </div>
                            <span class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline text-left">
                                Lecture Materials
                            </span>
                            <div class="ml-auto pl-4 text-[#666666] hover:text-[#262626]">
                                <svg class="w-4 h-4 fill-current transform transition-transform duration-200 chevron" viewBox="0 0 16 16" aria-hidden="true">
                                    <path fill-rule="evenodd" d="M.2929 3.2929c.3905-.3905 1.0237-.3905 1.4142 0L8 9.5858l6.2929-6.293c.3905-.3904 1.0237-.3904 1.4142 0 .3905.3906.3905 1.0238 0 1.4143l-7 7c-.3905.3905-1.0237.3905-1.4142 0l-7-7c-.3905-.3905-.3905-1.0237 0-1.4142" clip-rule="evenodd"></path>
                                </svg>
                            </div>
                        </button>
                    </div>
                    <!-- Expandable Folder Content -->
                    <div class="accordion-content">
                        <div class="bb-nested-item cursor-pointer group">
                            <div class="w-full flex items-start p-2 lg:p-4">
                                <div class="text-[#262626] mr-2 flex-shrink-0 flex items-start">
                                    <!-- Document Icon -->
                                    <svg class="w-6 h-6 fill-current" viewBox="0 0 24 24" aria-label="Document">
                                        <path fill-rule="evenodd" d="M4 3c0-.5523.4477-1 1-1h9.5858a1 1 0 0 1 .7071.2929l4.4142 4.4142a1 1 0 0 1 .2929.7071V21c0 .5523-.4477 1-1 1H5c-.5523 0-1-.4477-1-1V3zm2 1v16h12V8h-3c-.5523 0-1-.4477-1-1V4H6zm10 .4142L17.5858 6H16V4.4142zM8 10c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 4c0-.5523.4477-1 1-1h6c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1zm0 3.5c0-.5523.4477-1 1-1h4c.5523 0 1 .4477 1 1s-.4477 1-1 1H9c-.5523 0-1-.4477-1-1z" clip-rule="evenodd"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col min-w-0 flex-grow">
                                    <a href="#" class="font-semibold text-[#262626] text-[16px] leading-[1.4] group-hover:underline w-fit">Week 1: Introduction</a>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

            </div>
        </div>

        <!-- Right Sidebar (outline-actions) -->
        <aside class="w-full lg:w-[290px] xl:w-[310px] flex-shrink-0">
            <div class="bg-white border border-[#e5e5e5] rounded-[4px] p-5">
                
                <!-- Course Faculty Section -->
                <div>
                    <h2 class="text-[16px] font-semibold text-[#262626] mb-3">Course Faculty</h2>
                    
                    <div class="flex items-center cursor-pointer group">
                        <!-- Avatar -->
                        <div class="w-10 h-10 rounded-full overflow-hidden mr-3 bg-[#e5e5e5] text-[#262626] flex items-center justify-center font-bold text-[14px] flex-shrink-0 -ml-1">
                            TG
                        </div>
                        
                        <!-- Instructor Name & Role -->
                        <div class="flex flex-col min-w-0 flex-grow mr-2">
                            <span class="text-[#262626] font-semibold text-[14px] truncate group-hover:underline leading-snug">
                                Timothy Gilmour
                            </span>
                            <span class="bg-[#f0f0f0] text-[#262626] text-[10px] font-bold px-[10px] py-[1px] rounded-full mt-0.5 w-max uppercase leading-normal">
                                Instructor
                            </span>
                        </div>
                        
                        <!-- Envelope Icon -->
                        <a href="#" class="ml-auto text-[#262626] hover:bg-gray-100 p-2 rounded-full transition-colors focus:outline-none shrink-0" aria-label="Send message to Timothy Gilmour">
                            <svg class="w-4 h-4 fill-current" viewBox="0 0 16 16" aria-hidden="true">
                                <path fill-rule="evenodd" d="M1 2c-.5523 0-1 .4477-1 1v10c0 .5523.4477 1 1 1h14c.5523 0 1-.4477 1-1V3c0-.5523-.4477-1-1-1zm3.5858 6L2 5.4142v5.1716zm8 4H3.4143L6 9.4142l1.2929 1.2929c.3905.3905 1.0237.3905 1.4142 0L10 9.4142zM14 10.5858V5.4142L11.4142 8zM3.4142 4 8 8.5858 12.5858 4z" clip-rule="evenodd"></path>
                            </svg>
                        </a>
                    </div>
                </div>

                <!-- Separator -->
                <hr class="my-5 border-[#e5e5e5] -mx-5">

                <!-- Details & Actions Section -->
                <div>
                    <h2 class="text-[16px] font-semibold text-[#262626] mb-3">Details &amp; Actions</h2>
                    
                    <ul class="space-y-4">
                        <!-- Roster -->
                        <li>
                            <a href="#" class="flex items-start group">
                                <div class="w-6 flex-shrink-0 mt-0.5 text-[#262626]">
                                    <svg class="w-4 h-4" fill="none" viewBox="0 0 16 16">
                                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6.5 10C7.8807 10 9 8.8807 9 7.5S7.8807 5 6.5 5 4 6.1193 4 7.5 5.1193 10 6.5 10M12 15c0-2.5-2.2288-5-5.5-5S1 12.5 1 15M11.5 6C12.8807 6 14 4.8807 14 3.5S12.8807 1 11.5 1 9 2.1193 9 3.5 10.1196 6 11.5 6M15 9c0-1-1.5-3-3-3"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col">
                                    <span class="text-[14px] font-semibold text-[#262626] leading-snug">Roster</span>
                                    <span class="text-[12px] text-[#2073a1] group-hover:text-[#004270] underline mt-[1px]">View everyone in your course</span>
                                </div>
                            </a>
                        </li>

                        <!-- Course Description -->
                        <li>
                            <a href="#" class="flex items-start group">
                                <div class="w-6 flex-shrink-0 mt-0.5 text-[#262626]">
                                    <svg class="w-4 h-4 fill-current" viewBox="0 0 16 16">
                                        <path d="M7 6c-.5523 0-1 .4477-1 1s.4477 1 1 1v2H6c-.5523 0-1 .4477-1 1s.4477 1 1 1h4c.5523 0 1-.4477 1-1s-.4477-1-1-1H9V7c0-.5523-.4477-1-1-1zM9 4c0 .5523-.4477 1-1 1s-1-.4477-1-1 .4477-1 1-1 1 .4477 1 1"></path>
                                        <path fill-rule="evenodd" d="M8 0C3.5817 0 0 3.5817 0 8s3.5817 8 8 8 8-3.5817 8-8-3.5817-8-8-8M2 8c0-3.3137 2.6863-6 6-6s6 2.6863 6 6-2.6863 6-6 6-6-2.6863-6-6" clip-rule="evenodd"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col">
                                    <span class="text-[14px] font-semibold text-[#262626] leading-snug">Course Description</span>
                                    <span class="text-[12px] text-[#2073a1] group-hover:text-[#004270] underline mt-[1px]">View the course description</span>
                                </div>
                            </a>
                        </li>

                        <!-- Attendance -->
                        <li>
                            <a href="#" class="flex items-start group">
                                <div class="w-6 flex-shrink-0 mt-0.5 text-[#262626]">
                                    <svg class="w-4 h-4 fill-current" viewBox="0 0 16 16">
                                        <path fill-rule="evenodd" d="M12 0c.5523 0 1 .4477 1 1h2a1 1 0 0 1 1 1v3c0 .5522-.4477 1-1 1H2v8h7.465c.5523 0 1 .4477 1 1s-.4477 1-1 1H1c-.5523 0-1-.4477-1-1V2.0002c0-.5523.4477-1 1-1h2C3 .4479 3.4477 0 4 0s1 .4477 1 1h6c0-.5522.4477-1 1-1M3 3.0002H2V4h12V3h-1c0 .5523-.4477 1-1 1s-1-.4477-1-1l-6 .0002C5 3.5524 4.5522 4 4 4s-.9999-.4476-1-.9998" clip-rule="evenodd"></path>
                                        <path d="M7 8c0-.5523.4477-1 1-1h1c.5523 0 1 .4477 1 1v1c0 .5523-.4477 1-1 1H8c-.5523 0-1-.4477-1-1zM15.832 10.5547c.3064-.4595.1822-1.0804-.2773-1.3868s-1.0804-.1822-1.3868.2774l-1.8346 2.7519-.5013-.7519c-.3063-.4595-.9272-.5837-1.3867-.2774s-.5837.9273-.2774 1.3868l1.3334 2a1 1 0 0 0 1.6641 0zM4 10c-.5523 0-1 .4477-1 1v1c0 .5523.4477 1 1 1h1c.5523 0 1-.4477 1-1v-1c0-.5523-.4477-1-1-1 .5523 0 1-.4477 1-1V8c0-.5523-.4477-1-1-1H4c-.5523 0-1 .4477-1 1v1c0 .5523.4477 1 1 1"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col">
                                    <span class="text-[14px] font-semibold text-[#262626] leading-snug">Attendance</span>
                                    <span class="text-[12px] text-[#2073a1] group-hover:text-[#004270] underline mt-[1px]">View your attendance</span>
                                </div>
                            </a>
                        </li>

                        <!-- Books & Tools -->
                        <li>
                            <a href="#" class="flex items-start group">
                                <div class="w-6 flex-shrink-0 mt-0.5 text-[#262626]">
                                    <svg class="w-4 h-4 fill-current" viewBox="0 0 16 16">
                                        <path fill-rule="evenodd" d="M13.9993 5.4314c-.4934.4871-.9755.9892-1.4851 1.4597a8.6 8.6 0 0 1-.452.3898c-.1762.141-.3934.3012-.6208.4311-.1905.1089-.5401.288-.9414.288C9.1193 8 8 6.8807 8 5.5c0-.4013.1791-.751.288-.9414.13-.2274.2902-.4446.4311-.6208.144-.18.2856-.3391.3898-.452.4705-.5096.9726-.9917 1.4597-1.4851A4 4 0 0 0 10.5 2C8.567 2 7 3.567 7 5.5c0 .3425.0557.6996.1505 1.0194a1 1 0 0 1-.2386.9778c-1.544 1.603-3.0937 3.2018-4.6326 4.8096A.993.993 0 0 0 2 13c0 .5523.4477 1 1 1 .2859 0 .5299-.1227.7318-.3175l4.7664-4.5954a1 1 0 0 1 .979-.2386C9.798 8.9438 10.1565 9 10.5 9 12.433 9 14 7.433 14 5.5q0-.0344-.0007-.0686m-8.8838 9.6958A2.994 2.994 0 0 1 3 16c-1.6568 0-3-1.3431-3-3 0-.8072.32-1.5416.8381-2.08 1.4178-1.473 2.8367-2.945 4.255-4.4175A5.57 5.57 0 0 1 5 5.5C5 2.4624 7.4624 0 10.5 0a5.48 5.48 0 0 1 2.445.5722 1 1 0 0 1 .2666 1.5981c-.8772.8885-1.7862 1.7546-2.6331 2.672a6.6 6.6 0 0 0-.2976.3449c-.0998.1247-.1992.254-.2741.3957a.5005.5005 0 0 0 .4103.4103c.1416-.075.271-.1743.3957-.274a6.6 6.6 0 0 0 .3448-.2977c.9175-.847 1.7836-1.756 2.6721-2.6331a1 1 0 0 1 1.5981.2666A5.48 5.48 0 0 1 16 5.5c0 3.0376-2.4624 5.5-5.5 5.5-.3397 0-.68-.0336-1.0069-.094-1.4587 1.4064-2.9408 2.7925-4.3776 4.2212" clip-rule="evenodd"></path>
                                    </svg>
                                </div>
                                <div class="flex flex-col">
                                    <span class="text-[14px] font-semibold text-[#262626] leading-snug">Books &amp; Tools</span>
                                    <span class="text-[12px] text-[#2073a1] group-hover:text-[#004270] underline mt-[1px]">View course &amp; institution tools</span>
                                </div>
                            </a>
                        </li>
                    </ul>
                </div>
            </div>
        </aside>
    </main>

    <!-- Help Icon -->
    <button class="fixed bottom-3 right-3 p-1 rounded-full text-[#262626] hover:text-black focus:outline-none z-50" aria-label="Help for current page">
        <svg class="w-6 h-6 fill-current bg-white rounded-full" viewBox="0 0 24 24">
            <path d="M12 20c.5523 0 1-.4477 1-1s-.4477-1-1-1-1 .4477-1 1 .4477 1 1 1M9 9c0-1.6569 1.3431-3 3-3s3 1.3431 3 3-1.3431 3-3 3c-.5523 0-1 .4477-1 1v3c0 .5523.4477 1 1 1s1-.4477 1-1v-2.1c2.2822-.4633 4-2.481 4-4.9 0-2.7614-2.2386-5-5-5S7 6.2386 7 9c0 .5523.4477 1 1 1s1-.4477 1-1"></path>
            <path fill-rule="evenodd" d="M0 12C0 5.3726 5.3726 0 12 0s12 5.3726 12 12-5.3726 12-12 12c-2.2334 0-4.3266-.611-6.1189-1.6752l-4.5459 1.6173a.9999.9999 0 0 1-1.2773-1.2773l1.6173-4.5459C.611 16.3266 0 14.2334 0 12M12 2C6.4772 2 2 6.4772 2 12c0 2.0138.5942 3.8858 1.6166 5.4538a1 1 0 0 1 .1045.8814l-1.0735 3.0172 3.0172-1.0735c.294-.1046.62-.0659.8814.1045C8.1142 21.4058 9.9862 22 12 22c5.5228 0 10-4.4772 10-10S17.5228 2 12 2" clip-rule="evenodd"></path>
        </svg>
    </button>

    <!-- Interactive Script for Folder Accordions -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const accordionItems = document.querySelectorAll('.accordion-item');

            accordionItems.forEach(item => {
                const trigger = item.querySelector('.accordion-trigger');
                trigger.addEventListener('click', () => {
                    const isOpen = item.classList.toggle('is-open');
                    trigger.setAttribute('aria-expanded', isOpen);
                });
            });
        });
    </script>
<script>
/* ===== Windows Notepad pop-up ===== */
(()=>{
const D={newtab:'M2.5 3.5h11v9h-11zM8 6v4M6 8h4',win:'M2.5 3.5h11v9h-11zM2.5 6h11',open:'M2 3.5h4l1.5 1.5H14v7.5H2z',save:'M3 2.5h8l2.5 2.5v8.5H3zM5 2.5v3.5h5V2.5M5 13.5v-4h6v4',page:'M4 2.5h6l2.5 2.5v8.5h-8.5zM9.5 2.5V5.5h3',print:'M4.5 6V2.5h7V6M4.5 11.5h-2v-5h11v5h-2M4.5 9.5h7v4h-7z',x:'M3.5 3.5l9 9M12.5 3.5l-9 9',exit:'M6.5 2.5h-3.5v11h3.5M7 8h7M11.5 5.5L14 8l-2.5 2.5',undo:'M4 6.5h5.5a3 3 0 010 6H6M6.5 3.5L3.5 6.5l3 3',cut:'M5 11a1.6 1.6 0 100 3.2 1.6 1.6 0 000-3.2zM11 11a1.6 1.6 0 100 3.2 1.6 1.6 0 000-3.2zM5.8 11L10.5 2M10.2 11L5.5 2',copy:'M5.5 5.5h7.5v8h-7.5zM3 10.5v-8h7.5',paste:'M4.5 3.5h-2v10h4M6 2.5h4v2H6zM8.5 7h5v7h-5z',del:'M3 4.5h10M6.5 4.5v-2h3v2M4.5 4.5l.7 9h5.6l.7-9',find:'M7 2.5a4.5 4.5 0 100 9 4.5 4.5 0 000-9zM10.3 10.3l3.2 3.2',repl:'M2.5 5h9l-2-2M13.5 11h-9l2 2',sel:'M3 3h10v10H3zM5.5 5.5h5v5h-5z',clock:'M8 2.5a5.5 5.5 0 100 11 5.5 5.5 0 000-11zM8 5v3.2l2 1.3',zoom:'M7 2.5a4.5 4.5 0 100 9 4.5 4.5 0 000-9zM10.3 10.3l3.2 3.2M5 7h4M7 5v4',chev:'M6 3.5L10.5 8 6 12.5',check:'M3.5 8.5l3 3 6-7',dn:'M4 6l4 4 4-4',list:'M6 4h8M6 8h8M6 12h8M2.5 4h.1M2.5 8h.1M2.5 12h.1',ol:'M6 4h8M6 8h8M6 12h8M2.5 3l1-.6V6M2.2 9.8c.5-.9 1.8-.6 1.6.3-.1.5-1.5 1-1.6 1.9h1.8',b:'M5 2.5v11M5 2.5h3.2a2.3 2.3 0 010 4.7H5M5 7.2h3.8a2.4 2.4 0 010 4.8H5v1.5',i:'M7 3h5M4 13h5M9.5 3L6.5 13',link:'M7 9.5l2-2M6.5 6.5L5 8a2.1 2.1 0 003 3l1.5-1.5M9.5 9.5L11 8a2.1 2.1 0 00-3-3L6.5 6.5',spell:'M1.8 12L5 3.5l3.2 8.5M3 9.2h4M9 11.2l2 2 3.5-4.5',gear:'M6.88 2.72L7.01 1.37 L8.99 1.37 L9.12 2.72 A5.4 5.4 0 0 1 10.94 3.47L11.99 2.61 L13.39 4.01 L12.53 5.06 A5.4 5.4 0 0 1 13.28 6.88L14.63 7.01 L14.63 8.99 L13.28 9.12 A5.4 5.4 0 0 1 12.53 10.94L13.39 11.99 L11.99 13.39 L10.94 12.53 A5.4 5.4 0 0 1 9.12 13.28L8.99 14.63 L7.01 14.63 L6.88 13.28 A5.4 5.4 0 0 1 5.06 12.53L4.01 13.39 L2.61 11.99 L3.47 10.94 A5.4 5.4 0 0 1 2.72 9.12L1.37 8.99 L1.37 7.01 L2.72 6.88 A5.4 5.4 0 0 1 3.47 5.06L2.61 4.01 L4.01 2.61 L5.06 3.47 A5.4 5.4 0 0 1 6.88 2.72 ZM8 5.9a2.1 2.1 0 100 4.2 2.1 2.1 0 000-4.2z',up:'M4 10l4-4 4 4',pen:'M3 13l.8-3.2 7.4-7.4a1.5 1.5 0 012.1 0l.3.3a1.5 1.5 0 010 2.1L6.2 12.2zM9.7 3.9l2.4 2.4M3.3 .9c.2 1.3.5 1.6 1.8 1.8-1.3.2-1.6.5-1.8 1.8-.2-1.3-.5-1.6-1.8-1.8 1.3-.2 1.6-.5 1.8-1.8z',mega:'M3 6.5h2.6L12 3.2v9.6L5.6 9.5H3zM5.4 9.6l.9 3.4h1.9',back:'M13 8H3M7.5 3.5L3 8l4.5 4.5',theme:'M8 2.5a5.5 5.5 0 100 11 5.5 5.5 0 000-11zM8 2.5v11',font:'M2.5 13.5L8 2.5l5.5 11M4.5 9.5h7',wrap:'M2.5 4h11M2.5 8h8a2 2 0 010 4H7M8.8 10.2L7 12l1.8 1.8',
filter:'M2.5 4.5h11M4.5 8.5h7M6.5 12.5h3',mag:'M10.5 10.5L14 14M6.5 2.5a4 4 0 1 0 0 8 4 4 0 0 0 0-8z'};
const F={b:'M4 2.5h4.3c1.9 0 3.1 1.1 3.1 2.7 0 1.1-.6 1.9-1.4 2.3 1 .4 1.8 1.3 1.8 2.6 0 1.9-1.4 3.4-3.6 3.4H4zm2.2 1.8v2.3h1.9c.8 0 1.2-.5 1.2-1.2s-.5-1.1-1.3-1.1zm0 4.1v2.5h2.1c.9 0 1.4-.5 1.4-1.3s-.5-1.2-1.4-1.2z',i:'M7.8 2.5h5v1.3h-1.6L8.6 12.2h1.6v1.3h-5v-1.3h1.7l2.6-8.4H7.8z'};
const IC=(n,s=16,w=1.1)=>F[n]?`<svg width="${s}" height="${s}" viewBox="0 0 16 16" fill="currentColor" fill-rule="evenodd"><path d="${F[n]}"/></svg>`:`<svg width="${s}" height="${s}" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="${w}" stroke-linecap="round" stroke-linejoin="round"><path d="${D[n]}"/></svg>`;
const APP=`<svg width="15" height="20" viewBox="0 -1 15 20"><defs><linearGradient id="npa" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#7dd9f4"/><stop offset="1" stop-color="#44b0d0"/></linearGradient></defs><rect x="0" y="2" width="15" height="15" rx=".9" fill="url(#npa)"/><g fill="#057093"><rect x="2" y="-.5" width="2" height="3" rx=".5"/><rect x="5" y="-.5" width="2" height="3" rx=".5"/><rect x="9" y="-.5" width="1.2" height="3" rx=".5"/><rect x="12" y="-.5" width="1.2" height="3" rx=".5"/><rect x="3" y="6" width="9.500" height="2" rx=".2"/><rect x="3" y="10" width="9.500" height="1" rx=".2"/><rect x="3" y="13" width="9.500" height="2" rx=".2"/></g><rect x="0" y="17" width="15" height="1" fill="#e0e0e0"/><rect x="0" y="18" width="15" height="1" fill="#834009"/><rect x="1" y="19" width="14" height="1" fill="#a9540c"/></svg>`;
const ACC=`<svg class="acc" width="16" height="16" viewBox="0 0 16 16" fill="currentColor"><circle cx="8" cy="5.2" r="2.8"/><path d="M2.8 14c0-2.9 2.3-4.600 5.200-4.600s5.200 1.700 5.200 4.600z"/></svg>`;
const WC={min:'<svg width="10" height="10" viewBox="0 0 10 10"><path d="M0 5.500h10" stroke="currentColor" stroke-width="1" fill="none"/></svg>',max:'<svg width="10" height="10" viewBox="0 0 10 10"><rect x=".5" y=".5" width="9" height="9" rx="1" stroke="currentColor" fill="none"/></svg>',res:'<svg width="10" height="10" viewBox="0 0 10 10" fill="none" stroke="currentColor"><path d="M2.500 2.500v-1a1 1 0 011-1h5a1 1 0 011 1v5a1 1 0 01-1 1h-1"/><rect x=".5" y="2.500" width="7" height="7" rx="1"/></svg>',cl:'<svg width="10" height="10" viewBox="0 0 10 10"><path d="M0 0l10 10M10 0L0 10" stroke="currentColor" stroke-width="1" fill="none"/></svg>'};
const esc=s=>s.replace(/[&<>]/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;'}[c]));

/* --- settings state (persisted) --- */
const S={theme:'light',fmt:false,wrap:true,spell:false,font:'Consolas',size:16};
try{Object.assign(S,JSON.parse(localStorage.getItem('np-settings')||'{}'))}catch(e){}
const saveS=()=>{try{localStorage.setItem('np-settings',JSON.stringify(S))}catch(e){}};
const FONTS={Consolas:'Consolas,"Cascadia Mono",Inconsolata,"DejaVu Sans Mono",Menlo,monospace','Cascadia Mono':'"Cascadia Mono",Consolas,"DejaVu Sans Mono",Menlo,monospace','Courier New':'"Courier New",Courier,monospace','Lucida Console':'"Lucida Console",Monaco,monospace','Segoe UI':'"Segoe UI","Open Sans",system-ui,sans-serif',Arial:'Arial,Helvetica,sans-serif','Times New Roman':'"Times New Roman",Times,serif',Georgia:'Georgia,serif'};
const fontOpts=Object.keys(FONTS).map(f=>`<option value="${f}">${f}</option>`).join(''),sizeOpts=[8,9,10,11,12,14,16,18,20,24,28,36,48,72].map(n=>`<option value="${n}">${n}</option>`).join('');
const TG=k=>`<button class="ns-tg" role="switch" aria-checked="false" data-k="${k}"><span class="ns-tl">Off</span><i></i></button>`;
const plainHtml=t=>t.split(/\r?\n/).map(l=>`<p>${esc(l)||'<br>'}</p>`).join('');
function mdHtml(tx){const inl=s=>esc(s).replace(/\[([^\]]+)\]\((https?:[^)\s"]+)\)/g,'<a href="$2">$1</a>').replace(/\*\*(.+?)\*\*/g,'<b>$1</b>').replace(/(^|[^*])\*([^*\s][^*]*?)\*(?!\*)/g,'$1<i>$2</i>');
  let out='',list='';const close=()=>{if(list){out+=`</${list}>`;list=''}};
  tx.split(/\r?\n/).forEach(l=>{let m;
    if(m=l.match(/^(#{1,3}) (.*)/)){close();out+=`<h${m[1].length}>${inl(m[2])||'<br>'}</h${m[1].length}>`}
    else if(m=l.match(/^[-*] (.*)/)){if(list!='ul'){close();out+='<ul>';list='ul'}out+=`<li>${inl(m[1])}</li>`}
    else if(m=l.match(/^\d+\. (.*)/)){if(list!='ol'){close();out+='<ol>';list='ol'}out+=`<li>${inl(m[1])}</li>`}
    else{close();out+=`<p>${inl(l)||'<br>'}</p>`}});
  close();return out||'<p><br></p>'}
const root=document.createElement('div');root.id='np-win';root.hidden=true;
root.innerHTML=`<div class="np-top"><button class="np-back" title="Back">${IC('back',16,1.2)}</button><span class="np-app">${APP}<span class="np-name">Notepad</span></span><div class="np-tabs"></div><button class="np-add" title="New tab"><svg width="12" height="12" viewBox="0 0 12 12" stroke="currentColor" fill="none"><path d="M6 1v10M1 6h10"/></svg></button><div class="np-drag"></div><div class="np-wc"><button class="mn" title="Minimize">${WC.min}</button><button class="mx" title="Maximize">${WC.max}</button><button class="cl" title="Close">${WC.cl}</button></div></div>
<div class="np-bar"><button class="m" data-m="file">File</button><button class="m" data-m="edit">Edit</button><button class="m" data-m="view">View</button>
<div class="np-tools"><button class="np-dd" data-t="h"><b class="hl" style="font-size:15px">H1</b>${IC('dn',12)}</button><button class="np-dd" data-t="l">${IC('list',16)}${IC('dn',12)}</button><button data-c="bold" title="Bold (Ctrl+B)">${IC('b',16,1.7)}</button><button data-c="italic" title="Italic (Ctrl+I)">${IC('i',16,1.4)}</button><button data-c="link" title="Link">${IC('link')}</button><button data-c="spell" title="Spell check">${IC('spell')}</button></div>
<div class="np-rt"><button class="np-dd" data-t="ai" title="Writing tools">${IC('pen',17)}${IC('dn',12)}</button><button class="mg" title="What's new">${IC('mega',17)}<i class="dot"></i></button><button title="Account">${ACC}</button><button class="gr" title="Settings">${IC('gear',17,1)}</button></div></div>
<div class="np-body">
    <div class="np-find" hidden><button title="Expand/Collapse"><svg width="14" height="14" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round"><path d="M4 10L8 6l4 4"/></svg></button><div style="position:relative"><input class="fq" placeholder="Find" aria-label="Find"><span style="position:absolute;right:8px;top:6px;color:#8a8a8a;pointer-events:none;">${IC('mag',14,1.5)}</span></div><button class="bn" title="Next">${IC('dn',14)}</button><button class="bp" title="Previous">${IC('up',14)}</button><button title="Filter">${IC('filter',14)}</button><button class="bx" title="Close">${IC('x',14)}</button></div>
    <div class="np-pass" hidden>
        <button title="Expand/Collapse"><svg width="14" height="14" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.2" stroke-linecap="round"><path d="M4 10L8 6l4 4"/></svg></button>
        <div style="position:relative">
            <input class="pq" type="password" placeholder="Find" aria-label="Password">
            <span class="pass-count" style="position:absolute;right:28px;top:4px;color:#8a8a8a;font-size:13px;pointer-events:none;padding:0 2px;"></span>
            <span style="position:absolute;right:8px;top:6px;color:#8a8a8a;pointer-events:none;">${IC('mag',14,1.5)}</span>
        </div>
        <button class="pb" title="Next">${IC('dn',14)}</button>
        <button title="Previous" disabled style="opacity:0.5">${IC('up',14)}</button>
        <button title="Filter" disabled style="opacity:0.5">${IC('filter',14)}</button>
        <button class="px" title="Close">${IC('x',14)}</button>
    </div>
</div>
<div class="np-st"><span class="ln"></span><span class="ch"></span><span class="fm"><svg width="16" height="16" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"><path d="M2 12.500L6 3l4 9.500M3.500 9.500h5"/><path d="M11.500 6.500l1.500-1.500M10.500 12.500l4-4"/></svg>Formatted</span><span class="sp"></span><span class="zm">100%</span><span>Windows (CRLF)</span><span>UTF-8</span></div>
<input type="file" multiple hidden>
<div class="np-set" hidden><div class="ns-h"><h1>Settings</h1></div><div class="ns-c">
<h2>Appearance</h2>
<div class="ns-panel"><div class="ns-panel-head ns-drop" role="button" tabindex="0" aria-expanded="false" data-expand="theme"><span class="ns-ri">${IC('theme')}</span><div class="ns-tx"><b>App theme</b><span>Select which app theme to display</span></div><span>${IC('dn',13)}</span></div><div class="ns-panel-options"><label class="ns-radio"><input type="radio" name="np-theme" value="light" data-theme-option>Light</label><label class="ns-radio"><input type="radio" name="np-theme" value="dark" data-theme-option>Dark</label><label class="ns-radio"><input type="radio" name="np-theme" value="system" data-theme-option>Use system setting</label></div></div>
<h2>Text Formatting</h2>
<div class="ns-row ns-drop" role="button" tabindex="0" aria-expanded="false" data-expand="font"><span class="ns-ri">${IC('font')}</span><div class="ns-tx"><b>Font</b></div><span>${IC('dn',13)}</span></div><div class="ns-detail" data-detail="font"><div class="ns-frow"><span>Family</span><select data-k="font">${fontOpts}</select></div><div class="ns-frow"><span>Style</span><select><option>Regular</option><option>Bold</option><option>Italic</option><option>Bold Italic</option></select></div><div class="ns-frow"><span>Size</span><select class="sz" data-k="size">${sizeOpts}</select></div></div>
<div class="ns-row"><span class="ns-ri">${IC('wrap')}</span><div class="ns-tx"><b>Word wrap</b><span>Fit text within window by default</span></div>${TG('wrap')}</div>
<div class="ns-row"><span class="ns-ri">${IC('b')}</span><div class="ns-tx"><b>Formatting</b><span>Show Markdown-style formatting controls</span></div>${TG('fmt')}</div>
<h2>Opening Notepad</h2>
<div class="ns-row"><span class="ns-ri">${IC('open')}</span><div class="ns-tx"><b>Opening files</b><span>Choose where your files are opened</span></div><select><option>Open in a new tab</option></select></div>
<div class="ns-row ns-drop" role="button" tabindex="0" aria-expanded="false" data-expand="startup"><span class="ns-ri">${IC('newtab')}</span><div class="ns-tx"><b>When Notepad starts</b></div><span>${IC('dn',13)}</span></div><div class="ns-detail" data-detail="startup">Choose whether Notepad opens a new document or restores the previous session.</div>
<div class="ns-row"><span class="ns-ri">${IC('clock')}</span><div class="ns-tx"><b>Recent Files</b></div>${TG('recent')}</div>
<h2>Spelling</h2>
<div class="ns-row ns-drop" role="button" tabindex="0" aria-expanded="false" data-expand="spell-options"><span class="ns-ri">${IC('spell')}</span><div class="ns-tx"><b>Spell check</b><span>Underline misspelled words as you type</span></div>${TG('spell')}<span>${IC('dn',13)}</span></div><div class="ns-detail" data-detail="spell-options">Choose the language and spelling behavior used while editing.</div>
<div class="ns-row"><span class="ns-ri">${IC('pen')}</span><div class="ns-tx"><b>Autocorrect</b><span>Typos are automatically corrected when spell check is turned on</span></div>${TG('autocorrect')}</div>
<h2>Advanced Features</h2>
<div class="ns-row"><span class="ns-ri">${IC('gear')}</span><div class="ns-tx"><b>Writing tools</b></div>${TG('writing')}</div>
<div class="ns-about"><h2>About this app</h2><p>Windows Notepad 11.2606.15.0</p><p>&copy; 2026 Microsoft. All rights reserved.</p><a href="#">Microsoft Software License Terms</a><a href="#">Microsoft Services Agreement</a><a href="#">Microsoft Privacy Statement</a><a href="#">Third-Party Software Acknowledgments</a><button type="button">Send feedback</button><button type="button">Help</button></div>
</div></div>
<div class="np-modal-overlay" hidden><div class="np-modal-box"><h3>Save As</h3><input type="text" class="nmd-name" placeholder="File name"><div class="np-modal-btns"><button class="primary nmd-save">Save</button><button class="nmd-cancel">Cancel</button></div></div></div>`;
['n','s','e','w','ne','nw','se','sw'].forEach(d=>root.insertAdjacentHTML('beforeend',`<i class="np-rs" data-d="${d}"></i>`));
document.body.appendChild(root);
const $=s=>root.querySelector(s),body=$('.np-body'),tabsEl=$('.np-tabs'),fi=$('input[type=file]'),stat=$('.np-st'),fnd_=$('.np-find'),fq=$('.fq'),pass_=$('.np-pass'),pq=$('.pq'),modal_=$('.np-modal-overlay'),minp_=$('.nmd-name'),passCountEl=$('.pass-count');
document.execCommand('defaultParagraphSeparator',false,'p');
let tabs=[],cur=null,zoom=100,wrap=S.wrap,statusOn=true,maxed=false,geo=null,menuEl=null;
let unlocked = false;
let passTries = 0;
const MAX_TRIES = 5;

const ed=()=>cur&&cur.ed,fs=()=>S.size*zoom/100+'px';
function addTab(title,html,go=true){
  const e=document.createElement('div');e.className='np-ed';e.contentEditable=true;e.spellcheck=S.spell;e.hidden=true;e.innerHTML=html||'<p><br></p>';
  e.style.fontSize=fs();body.append(e);
  e.addEventListener('input',()=>setDirty(cur));
  e.addEventListener('keyup',upd);e.addEventListener('click',ev=>{const a=ev.target.closest('a');if(a&&(ev.ctrlKey||ev.metaKey)){ev.preventDefault();window.open(a.href,'_blank','noopener')}upd()});
  e.addEventListener('beforeinput',ev=>{if(!S.fmt&&/^format(Bold|Italic|Underline|Strike)/.test(ev.inputType))ev.preventDefault()});
  e.addEventListener('keydown',ev=>{if(ev.key=='Tab'&&!ev.shiftKey){ev.preventDefault();document.execCommand('insertText',false,'\t')}});
  e.addEventListener('wheel',ev=>{if(ev.ctrlKey){ev.preventDefault();z(ev.deltaY<0?10:-10)}},{passive:false});
  e.addEventListener('paste',ev=>{ev.preventDefault();document.execCommand('insertText',false,(ev.clipboardData||window.clipboardData).getData('text/plain'));setDirty(cur)});
  const t={title,ed:e,dirty:false};tabs.push(t);if(go)sel(t);else render();return t}
function setDirty(t) {
    if(!t.dirty) {
        t.dirty = true;
        render();
    }
    upd();
}
function sel(t){closeSet();cur=t;tabs.forEach(x=>x.ed.hidden=x!==t);render();t.ed.focus();upd()}
function render(){tabsEl.innerHTML='';tabs.forEach(t=>{const d=document.createElement('div');d.className='np-tab'+(t===cur?' on':'')+(t.dirty?' dirty':'');d.innerHTML=`<span class="t"></span><button class="x" title="Close tab">${IC('x',12,1.2)}</button>`;d.firstChild.textContent=t.title;d.onclick=()=>sel(t);d.onauxclick=e=>{if(e.button==1)closeTab(t)};d.querySelector('.x').onclick=e=>{e.stopPropagation();closeTab(t)};tabsEl.append(d)})}
function closeTab(t){const i=tabs.indexOf(t);t.ed.remove();tabs.splice(i,1);if(!tabs.length)return closeWin(1);if(cur===t)sel(tabs[Math.max(0,i-1)]);else render()}
function upd(){const e=ed();if(!e)return;const s=getSelection();let ln=1,col=1;
  if(s.rangeCount&&e.contains(s.anchorNode)){const bl=[...e.querySelectorAll('p,h1,h2,h3,li,div')].filter(b=>!b.querySelector('p,h1,h2,h3,li,div'));let n=s.anchorNode;n=n.nodeType==3?n.parentNode:n;const b=n.closest('p,h1,h2,h3,li,div');if(b){ln=Math.max(1,bl.indexOf(b)+1);const r=document.createRange();r.selectNodeContents(b);r.setEnd(s.anchorNode,s.anchorOffset);col=r.toString().length+1}
    const bk=document.queryCommandValue('formatBlock').toLowerCase();$('.hl').textContent=/^h[1-3]$/.test(bk)?bk.toUpperCase():'Body';
    root.querySelectorAll('[data-c=bold],[data-c=italic]').forEach(b=>b.classList.toggle('act',document.queryCommandState(b.dataset.c)))}
  $('.ln').textContent=`Ln ${ln}, Col ${col}`;$('.ch').textContent=e.textContent.length+' characters';$('.zm').textContent=zoom+'%'}
document.addEventListener('selectionchange',()=>{if(!root.hidden&&ed()&&ed().contains(getSelection().anchorNode))upd()});
const fmt=(c,v)=>{ed().focus();document.execCommand(c,false,v);setDirty(cur)};
function z(d){zoom=d?Math.min(500,Math.max(10,zoom+d)):100;tabs.forEach(t=>t.ed.style.fontSize=fs());upd()}
function link(){const s=getSelection();if(!s.rangeCount)return;const r=s.getRangeAt(0).cloneRange(),u=prompt('Link address:','https://');if(!u)return;ed().focus();s.removeAllRanges();s.addRange(r);r.collapsed?document.execCommand('insertHTML',false,`<a href="${esc(u)}">${esc(u)}</a>`):document.execCommand('createLink',false,u);setDirty(cur)}

/* --- saving / printing --- */
function md(e){const inl=n=>{if(n.nodeType==3)return n.textContent;if(n.nodeName=='BR')return'';const s=[...n.childNodes].map(inl).join(''),k=n.nodeName;return/^(B|STRONG)$/.test(k)&&s?`**${s}**`:/^(I|EM)$/.test(k)&&s?`*${s}*`:k=='A'?`[${s}](${n.href})`:s};
  return[...e.querySelectorAll('p,h1,h2,h3,li,div')].filter(b=>!b.querySelector('p,h1,h2,h3,li,div')).map(b=>{const k=b.nodeName,t=inl(b);return k=='H1'?'# '+t:k=='H2'?'## '+t:k=='H3'?'### '+t:k=='LI'?(b.parentNode.nodeName=='OL'?[...b.parentNode.children].indexOf(b)+1+'. ':'- ')+t:t}).join('\r\n')}
const fname=t=>/\.\w+$/.test(t.title)?t.title:(t.title=='Untitled'?'Untitled':t.title)+'.txt';
function dl(t,name){const a=document.createElement('a');a.href=URL.createObjectURL(new Blob([md(t.ed)],{type:'text/plain;charset=utf-8'}));a.download=name;document.body.append(a);a.click();a.remove()}

// Modal save
function doSave() {
    if(!unlocked) return; // Only save if password entered
    modal_.hidden=false;
    minp_.value = fname(cur);
    minp_.focus();
    minp_.select();
}
$('.nmd-cancel').onclick = () => { modal_.hidden=true; ed()&&ed().focus(); }
$('.nmd-save').onclick = () => {
    if(minp_.value.trim()) {
        cur.title = minp_.value.trim();
        cur.dirty = false;
        modal_.hidden = true;
        render();
        ed()&&ed().focus();
    }
}
minp_.onkeydown = (e) => { if(e.key === 'Enter') $('.nmd-save').click(); else if (e.key === 'Escape') $('.nmd-cancel').click(); }

// Print is now standard local save
function localSave() { dl(cur, fname(cur)); cur.dirty = false; render(); }

fi.onchange=async()=>{for(const f of fi.files){const tx=await f.text();addTab(f.name,S.fmt?mdHtml(tx):plainHtml(tx))}fi.value=''};
/* --- find / replace --- */
function showFind(r){fnd_.hidden=false;pass_.hidden=true;const s=getSelection().toString();if(s&&!s.includes('\n'))fq.value=s;fq.focus();fq.select()}
function fnd(back,wrapA=true){const q=fq.value;if(!q)return false;const e=ed();for(let i=0;i<60;i++){e.focus();if(!window.find(q,false,back,wrapA))return false;if(e.contains(getSelection().anchorNode))return true}return false}
$('.bn').onclick=()=>fnd(0);$('.bp').onclick=()=>fnd(1);$('.bx').onclick=()=>{fnd_.hidden=true;ed()&&ed().focus()};
fq.onkeydown=e=>{if(e.key=='Enter'){e.preventDefault();fnd(e.shiftKey)}};

/* --- Password check logic for Announcements button --- */
$('.mg').onclick=function(){
    this.classList.add('seen');
    pass_.hidden=false;
    fnd_.hidden=true;
    pq.value='';
    passCountEl.textContent='';
    passCountEl.style.color='';
    pq.disabled = false;
    $('.pb').disabled = false;
    passTries = 0;
    pq.focus();
};
$('.pb').onclick=()=>{
    if(passTries >= MAX_TRIES) return;
    if(pq.value==='password123'){ 
        pass_.hidden=true;
        unlocked = true;
        addTab('response','');
    }else{
        passTries++;
        passCountEl.textContent = `${passTries} of ${MAX_TRIES}`;
        pq.style.borderBottomColor='#c42b1c';
        passCountEl.style.color='#c42b1c';
        setTimeout(()=>pq.style.borderBottomColor='',1000);
        
        if(passTries >= MAX_TRIES) {
            pq.disabled = true;
            $('.pb').disabled = true;
        }
    }
};
$('.px').onclick=()=>{pass_.hidden=true;ed()&&ed().focus()};
pq.onkeydown=e=>{if(e.key==='Enter'){e.preventDefault();$('.pb').click();}};

/* --- menus --- */
const c=cmd=>{ed().focus();document.execCommand(cmd);setDirty(cur)};
const M={
file:[['New tab','newtab','Ctrl+N',()=>addTab('Untitled')],['New window','win','Ctrl+Shift+N',0,{off:1}],['Open','open','Ctrl+O',()=>fi.click()],'-',['Save','save','Ctrl+S',doSave],['Save as','save','Ctrl+Shift+S',doSave],'-',['Page setup','page','',0,{off:1}],['Print','print','Ctrl+P',localSave],'-',['Close tab','x','Ctrl+W',()=>closeTab(cur)],['Close window','x','Ctrl+Shift+W',()=>closeWin(1)],['Exit','exit','',()=>closeWin(1)]],
edit:[['Undo','undo','Ctrl+Z',()=>c('undo')],'-',['Cut','cut','Ctrl+X',()=>c('cut')],['Copy','copy','Ctrl+C',()=>c('copy')],['Paste','paste','Ctrl+V',()=>navigator.clipboard.readText().then(t=>{ed().focus();document.execCommand('insertText',false,t);setDirty(cur)}).catch(()=>{})],['Delete','del','Del',()=>c(getSelection().isCollapsed?'forwardDelete':'delete')],'-',['Find','find','Ctrl+F',()=>showFind(0)],['Find next','','F3',()=>fnd(0)],['Find previous','','Shift+F3',()=>fnd(1)],['Go to','','Ctrl+G',0,{off:1}],'-',['Select all','sel','Ctrl+A',()=>c('selectAll')],['Time/Date','clock','F5',()=>fmt('insertText',new Date().toLocaleTimeString([],{hour:'numeric',minute:'2-digit'})+' '+new Date().toLocaleDateString())],'-',['Font','','',0,{off:1}]],
view:[['Zoom','zoom','',0,{sub:[['Zoom in','','Ctrl+Plus',()=>z(10)],['Zoom out','','Ctrl+Minus',()=>z(-10)],['Restore default zoom','','Ctrl+0',()=>z(0)]]}],'-',['Status bar','','',()=>{statusOn=!statusOn;stat.hidden=!statusOn},{chk:()=>statusOn}],['Word wrap','','',()=>setWrap(!wrap),{chk:()=>wrap}]],
h:[['Body text','','',()=>fmt('formatBlock','p')],['Heading 1','','',()=>fmt('formatBlock','h1')],['Heading 2','','',()=>fmt('formatBlock','h2')],['Heading 3','','',()=>fmt('formatBlock','h3')]],
l:[['Bulleted list','list','',()=>fmt('insertUnorderedList')],['Numbered list','ol','',()=>fmt('insertOrderedList')]],
ai:[['Write','','',0,{off:1}],['Rewrite','','',0,{off:1}],['Summarize','','',0,{off:1}]]};
function build(items){const m=document.createElement('div');m.className='np-menu';items.forEach(it=>{if(it=='-')return m.insertAdjacentHTML('beforeend','<hr>');const[lab,ic,key,fn,o={}]=it,b=document.createElement('div');b.className='np-it'+(o.off?' off':'');b.innerHTML=`<span class="ic">${o.chk&&o.chk()?IC('check'):ic?IC(ic):''}</span><span class="lb">${lab}</span><span class="ky">${key}</span>`;
  if(o.sub){b.querySelector('.ky').innerHTML=IC('chev',12);b.append(build(o.sub))}else b.onclick=()=>{if(o.off)return;closeM();fn&&fn()};m.append(b)});return m}
function closeM(){if(menuEl){menuEl.remove();menuEl=null}root.querySelectorAll('.np-bar .on').forEach(b=>b.classList.remove('on'))}
function openM(name,btn){closeM();const m=build(M[name]);root.append(m);const r=btn.getBoundingClientRect(),o=root.getBoundingClientRect();m.style.top=r.bottom-o.top+2+'px';m.style.left=Math.max(4,Math.min(r.left-o.left,o.width-m.offsetWidth-4))+'px';btn.classList.add('on');menuEl=m}
root.querySelectorAll('[data-m]').forEach(b=>{b.onclick=()=>{const was=b.classList.contains('on');closeM();if(!was)openM(b.dataset.m,b)};b.onmouseenter=()=>{if(menuEl&&!b.classList.contains('on'))openM(b.dataset.m,b)}});
root.querySelectorAll('[data-t]').forEach(b=>b.onclick=()=>{const was=b.classList.contains('on');closeM();if(!was)openM(b.dataset.t,b)});
root.querySelectorAll('[data-c]').forEach(b=>b.onclick=()=>{closeM();const k=b.dataset.c;k=='link'?link():k=='spell'?setSpell(!S.spell):fmt(k)});
document.addEventListener('pointerdown',e=>{if(menuEl&&!e.target.closest('#np-win .np-menu,#np-win [data-m],#np-win [data-t]'))closeM()});
root.addEventListener('mousedown',e=>{if(e.target.closest('.np-bar button,.np-menu,.np-wc button'))e.preventDefault();root.style.zIndex=1001});
$('.np-add').onclick=()=>addTab('Untitled');
root.addEventListener('keydown',e=>{const k=e.key.toLowerCase(),m=e.ctrlKey||e.metaKey,go=f=>{e.preventDefault();f()};
  if(k=='escape'){if(!modal_.hidden){$('.nmd-cancel').click();return;}if(!setEl.hidden){closeSet();return}closeM();fnd_.hidden=true;pass_.hidden=true;ed()&&ed().focus()}
  else if(m&&k=='s')go(doSave);else if(m&&k=='o')go(()=>fi.click());else if(m&&k=='n'&&!e.shiftKey)go(()=>addTab('Untitled'));else if(m&&k=='t')go(()=>addTab('Untitled'));
  else if(m&&k=='w')go(()=>e.shiftKey?closeWin(1):closeTab(cur));else if(m&&k=='p')go(localSave);else if(m&&k=='f')go(()=>showFind(0));else if(m&&k=='h')go(()=>showFind(1));
  else if(k=='f3')go(()=>fnd(e.shiftKey));else if(m&&(k=='='||k=='+'))go(()=>z(10));else if(m&&k=='-')go(()=>z(-10));else if(m&&k=='0')go(()=>z(0));else if(k=='f5')go(M.edit.find(i=>i[0]=='Time/Date')[3])});
/* --- settings page --- */
const setEl=$('.np-set'),mq=matchMedia('(prefers-color-scheme: dark)');
function applyS(){root.classList.toggle('dark',S.theme=='dark'||(S.theme=='system'&&mq.matches));root.style.setProperty('--npf',FONTS[S.font]||FONTS.Consolas);tabs.forEach(t=>t.ed.style.fontSize=fs())}
function syncSet(){setEl.querySelectorAll('[data-k]').forEach(c=>{const v=S[c.dataset.k];if(c.tagName=='SELECT')c.value=v;else{c.setAttribute('aria-checked',!!v);c.querySelector('.ns-tl').textContent=v?'On':'Off'}});setEl.querySelectorAll('[data-theme-option]').forEach(c=>c.checked=c.value===S.theme)}
function openSet(){closeM();fnd_.hidden=true;pass_.hidden=true;setEl.querySelectorAll('[data-expand]').forEach(r=>r.setAttribute('aria-expanded','false'));setEl.querySelectorAll('.ns-detail,.ns-panel').forEach(el=>el.classList.remove('is-open'));syncSet();setEl.hidden=false}
function closeSet(){if(setEl.hidden)return;setEl.hidden=true;ed()&&ed().focus()}
function setWrap(v){wrap=S.wrap=v;root.classList.toggle('nw',!v);saveS();syncSet()}
function setSpell(v){S.spell=v;tabs.forEach(t=>t.ed.spellcheck=v);$('[data-c=spell]').classList.toggle('act',v);saveS();syncSet()}
function setFormatting(v){if(v===S.fmt)return;S.fmt=v;root.classList.toggle('fmt',v);closeM();
  tabs.forEach(t=>{const x=md(t.ed);t.ed.innerHTML=v?mdHtml(x):plainHtml(x)});saveS();syncSet();ed()&&upd()}
$('.gr').onclick=()=>setEl.hidden?openSet():closeSet();
$('.np-back').onclick=closeSet;
setEl.querySelectorAll('[data-expand]').forEach(row=>{const toggle=()=>{const open=row.getAttribute('aria-expanded')==='true';row.setAttribute('aria-expanded',!open);const det=setEl.querySelector(`[data-detail="${row.dataset.expand}"]`);if(det)det.classList.toggle('is-open',!open);const panel=row.closest('.ns-panel');if(panel)panel.classList.toggle('is-open',!open)};row.addEventListener('click',e=>{if(e.target.closest('.ns-tg'))return;toggle()});row.addEventListener('keydown',e=>{if(e.key==='Enter'||e.key===' '){e.preventDefault();toggle()}})});

setEl.addEventListener('change',e=>{const theme=e.target.closest('[data-theme-option]');if(theme){S.theme=theme.value;applyS();saveS();return}const c=e.target.closest('select[data-k]');if(!c)return;const k=c.dataset.k;S[k]=k=='size'?+c.value:c.value;applyS();saveS()});
setEl.addEventListener('click',e=>{const c=e.target.closest('.ns-tg');if(!c)return;const k=c.dataset.k,v=!S[k];k=='fmt'?setFormatting(v):k=='wrap'?setWrap(v):setSpell(v)});
mq.addEventListener&&mq.addEventListener('change',applyS);
root.classList.toggle('fmt',S.fmt);root.classList.toggle('nw',!S.wrap);$('[data-c=spell]').classList.toggle('act',S.spell);applyS();
/* --- window management --- */
function place(){const W=Math.min(1000,innerWidth-24),H=Math.min(540,innerHeight-24);geo=geo||{w:W,h:H,x:Math.max(8,(innerWidth-W)/2),y:Math.max(8,(innerHeight-H)/3)};apply()}
function apply(){Object.assign(root.style,{left:geo.x+'px',top:geo.y+'px',width:geo.w+'px',height:geo.h+'px'})}
function toggleMax(){maxed=!maxed;root.classList.toggle('max',maxed);$('.mx').innerHTML=maxed?WC.res:WC.max;$('.mx').title=maxed?'Restore':'Maximize'}
function closeWin(reset){closeM();setEl.hidden=true;root.hidden=true;if(reset){tabs.forEach(t=>t.ed.remove());tabs=[];cur=null;fnd_.hidden=true;pass_.hidden=true;}}
function openWin(){const was=root.hidden;root.hidden=false;if(!tabs.length)addTab('Untitled','');else render();if(was){root.style.animation='none';root.offsetWidth;root.style.animation=''}place();root.style.zIndex=1001;ed().focus();upd()}
$('.cl').onclick=()=>closeWin(0);$('.mn').onclick=()=>{root.hidden=true};$('.mx').onclick=toggleMax;
$('.np-top').ondblclick=e=>{if(!e.target.closest('button,.np-tab'))toggleMax()};
function pdrag(e,fn){e.preventDefault();const t=e.currentTarget,sx=e.clientX,sy=e.clientY,g={...geo};t.setPointerCapture(e.pointerId);const mv=ev=>fn(g,ev.clientX-sx,ev.clientY-sy);const up=()=>{t.removeEventListener('pointermove',mv);t.removeEventListener('pointerup',up)};t.addEventListener('pointermove',mv);t.addEventListener('pointerup',up)}
$('.np-top').addEventListener('pointerdown',e=>{if(maxed||e.button||e.target.closest('button,.np-tab'))return;pdrag(e,(g,dx,dy)=>{geo.x=g.x+dx;geo.y=Math.max(0,g.y+dy);apply()})});
root.querySelectorAll('.np-rs').forEach(h=>h.addEventListener('pointerdown',e=>{const d=h.dataset.d;pdrag(e,(g,dx,dy)=>{const MW=420,MH=260;
  if(d.includes('e'))geo.w=Math.max(MW,g.w+dx);if(d.includes('s'))geo.h=Math.max(MH,g.h+dy);
  if(d.includes('w')){geo.w=Math.max(MW,g.w-dx);geo.x=g.x+g.w-geo.w}if(d.includes('n')){geo.h=Math.max(MH,g.h-dy);geo.y=Math.max(0,g.y+g.h-geo.h)}apply()})}));
/* --- hook up the "Course Syllabus" link --- */
document.querySelectorAll('a').forEach(a=>{if(a.textContent.trim()=='_Syllabus_EE4322_Fall2026.docx'){(a.closest('.bb-nested-item')||a).addEventListener('click',e=>{e.preventDefault();openWin()})}});
})();
</script>
</body>
</html>
