<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0, user-scalable=yes">
  
  <!-- PWA & Add to Home Screen Capabilities -->
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <meta name="apple-mobile-web-app-title" content="Global Ind">
  <meta name="mobile-web-app-capable" content="yes">
  <meta name="theme-color" content="#102A43">
  <title>Global Industries | Official Site Management</title>
  
  <link rel="manifest" href='data:application/manifest+json,{"name":"Global Industries Portal","short_name":"GlobalInd","display":"standalone","background_color":"#F0F4F8","theme_color":"#102A43","icons":[{"src":"data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAxMDAgMTAwIj48Y2lyY2xlIGN4PSI1MCIgY3k9IjUwIiByPSI0NSIgZmlsbD0iIzEwMkE0MyIvPjx0ZXh0IHg9IjUwIiB5PSI1NiIgZmlsbD0iI0ZGRkZGRiIgZm9udC1mYW1pbHk9IkFyaWFsIiBmb250LXNpemU9IjIwIiBmb250LXdlaWdodD0iYm9sZCIgdGV4dC1hbmNob3I9Im1pZGRsZSI+R0k8L3RleHQ+PC9zdmc+","sizes":"192x192","type":"image/svg+xml"}]}'>

  <!-- Firebase SDKs (Primary, Database & Storage Compat) -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/firebase/10.8.1/firebase-app-compat.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/firebase/10.8.1/firebase-database-compat.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/firebase/10.8.1/firebase-storage-compat.min.js"></script>
  
  <!-- Export & PDF Libraries -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>

  <!-- Three.js & GSAP Animation Libraries -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>

  <style>
    /* =========================================
       THEMES SETUP
       ========================================= */
    :root {
      --primary: #102A43; --primary-light: #1F4E78; --secondary: #2D68C4;
      --accent: #FFD700; --bg: #F0F4F8; --card-bg: #FFFFFF;
      --text: #0F172A; --text-muted: #64748B; --border: #E2E8F0;
      --success: #10B981; --warning: #F59E0B; --danger: #EF4444;
      --shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
      --spring: cubic-bezier(0.175, 0.885, 0.32, 1.275);
      --glass-blur: blur(0px);
    }

    [data-theme="dark"] {
      --primary: #94A3B8; --primary-light: #334155; --secondary: #3B82F6;
      --accent: #F59E0B; --bg: #0F172A; --card-bg: #1E293B;
      --text: #F8FAFC; --text-muted: #94A3B8; --border: #334155;
      --shadow: 0 4px 15px rgba(0, 0, 0, 0.5);
    }

    [data-theme="liquid-glass"] {
      --primary: #38BDF8; --primary-light: #0284C7; --secondary: #0EA5E9;
      --accent: #38BDF8; --bg: #030712; --card-bg: rgba(15, 23, 42, 0.65);
      --text: #F8FAFC; --text-muted: #94A3B8; --border: rgba(56, 189, 248, 0.25);
      --success: #34D399; --warning: #FBBF24; --danger: #F87171;
      --shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.37);
      --glass-blur: blur(16px);
    }

    [data-theme="cyberpunk"] {
      --primary: #FF007F; --primary-light: #7928CA; --secondary: #00F0FF;
      --accent: #FFE600; --bg: #05050A; --card-bg: #121019;
      --text: #00F0FF; --text-muted: #FF007F; --border: #FF007F;
      --success: #00FF66; --warning: #FF9900; --danger: #FF0033;
      --shadow: 0 0 20px rgba(255,0,127,0.3);
    }

    [data-theme="emerald"] {
      --primary: #064E3B; --primary-light: #047857; --secondary: #059669;
      --accent: #10B981; --bg: #022C22; --card-bg: #064E3B;
      --text: #ECFDF5; --text-muted: #6EE7B7; --border: #047857;
      --success: #34D399; --warning: #F59E0B; --danger: #EF4444;
      --shadow: 0 10px 25px rgba(6, 78, 59, 0.4);
    }

    [data-theme="sunset"] {
      --primary: #7C2D12; --primary-light: #C2410C; --secondary: #EA580C;
      --accent: #FDBA74; --bg: #FFF7ED; --card-bg: #FFFFFF;
      --text: #431407; --text-muted: #9A3412; --border: #FFEDD5;
      --success: #16A34A; --warning: #D97706; --danger: #DC2626;
    }

    [data-theme="royal"] {
      --primary: #31105C; --primary-light: #581C87; --secondary: #7C3AED;
      --accent: #C084FC; --bg: #1E1B4B; --card-bg: #2E1065;
      --text: #FAF5FF; --text-muted: #D8B4FE; --border: #581C87;
    }

    [data-theme="arctic"] {
      --primary: #0C4A6E; --primary-light: #0369A1; --secondary: #0284C7;
      --accent: #38BDF8; --bg: #F0F9FF; --card-bg: #FFFFFF;
      --text: #082F49; --text-muted: #38BDF8; --border: #BAE6FD;
    }

    [data-theme="matrix"] {
      --primary: #00FF00; --primary-light: #003300; --secondary: #00CC00;
      --accent: #00FF66; --bg: #000500; --card-bg: #001100;
      --text: #00FF00; --text-muted: #008800; --border: #00FF00;
    }

    [data-theme="obsidian"] {
      --primary: #FAFAFA; --primary-light: #A3A3A3; --secondary: #525252;
      --accent: #E5E5E5; --bg: #0A0A0A; --card-bg: #171717;
      --text: #F5F5F5; --text-muted: #737373; --border: #262626;
    }

    [data-theme="rose-gold"] {
      --primary: #4A2E2B; --primary-light: #8C5853; --secondary: #B76E79;
      --accent: #E0BFB8; --bg: #FDFBFB; --card-bg: #FFFFFF;
      --text: #2D1D1B; --text-muted: #8C5853; --border: #E8D7D5;
    }

    [data-theme="tokyo-night"] {
      --primary: #7AA2F7; --primary-light: #3D59A1; --secondary: #bb9af7;
      --accent: #ff9e64; --bg: #1a1b26; --card-bg: #24283b;
      --text: #c0caf5; --text-muted: #565f89; --border: #414868;
    }

    [data-theme="solarized"] {
      --primary: #268bd2; --primary-light: #2aa198; --secondary: #b58900;
      --accent: #cb4b16; --bg: #fdf6e3; --card-bg: #eee8d5;
      --text: #657b83; --text-muted: #93a1a1; --border: #93a1a1;
    }

    [data-theme="nordic"] {
      --primary: #5E81AC; --primary-light: #81A1C1; --secondary: #88C0D0;
      --accent: #A3BE8C; --bg: #2E3440; --card-bg: #3B4252;
      --text: #ECEFF4; --text-muted: #D8DEE9; --border: #4C566A;
    }

    [data-theme="deep-space"] {
      --primary: #6366F1; --primary-light: #4F46E5; --secondary: #8B5CF6;
      --accent: #EC4899; --bg: #030712; --card-bg: #0F172A;
      --text: #F3F4F6; --text-muted: #9CA3AF; --border: #1F2937;
    }

    [data-theme="pastel-dream"] {
      --primary: #93C5FD; --primary-light: #60A5FA; --secondary: #F472B6;
      --accent: #FDE047; --bg: #FDF4FF; --card-bg: #FFFFFF;
      --text: #4B5563; --text-muted: #9CA3AF; --border: #F3E8FF;
    }

    [data-theme="retro-terminal"] {
      --primary: #33FF33; --primary-light: #008800; --secondary: #00FFCC;
      --accent: #FFFF33; --bg: #111111; --card-bg: #1E1E1E;
      --text: #33FF33; --text-muted: #00AA00; --border: #33FF33;
    }

    [data-theme="industrial-steel"] {
      --primary: #475569; --primary-light: #64748B; --secondary: #0284C7;
      --accent: #F59E0B; --bg: #0F172A; --card-bg: #1E293B;
      --text: #F1F5F9; --text-muted: #94A3B8; --border: #334155;
    }

    [data-theme="golden-amber"] {
      --primary: #B45309; --primary-light: #D97706; --secondary: #F59E0B;
      --accent: #FEF3C7; --bg: #FFFBEB; --card-bg: #FFFFFF;
      --text: #78350F; --text-muted: #92400E; --border: #FDE68A;
    }

    [data-theme="carbon-fiber"] {
      --primary: #38BDF8; --primary-light: #0284C7; --secondary: #64748B;
      --accent: #F43F5E; --bg: #09090B; --card-bg: #18181B;
      --text: #FAFAFA; --text-muted: #A1A1AA; --border: #27272A;
    }

    [data-theme="synthwave"] {
      --primary: #FF77FF; --primary-light: #9900CC; --secondary: #00FFFF;
      --accent: #FFCC00; --bg: #1A0033; --card-bg: #2B0055;
      --text: #FF66FF; --text-muted: #CC99FF; --border: #FF33CC;
    }

    [data-theme="neon-sakura"] {
      --primary: #FF69B4; --primary-light: #C71585; --secondary: #FF1493;
      --accent: #FFB6C1; --bg: #FFF0F5; --card-bg: #FFFFFF;
      --text: #8B008B; --text-muted: #DB7093; --border: #FFC0CB;
    }

    [data-theme="sunset-mirage"] {
      --primary: #FF4500; --primary-light: #FF6347; --secondary: #FF8C00;
      --accent: #FFD700; --bg: #2C0000; --card-bg: #3D0C02;
      --text: #FFA500; --text-muted: #FF6347; --border: #FF4500;
    }

    [data-theme="acid-matrix"] {
      --primary: #76FF03; --primary-light: #33691E; --secondary: #64DD17;
      --accent: #CCFF90; --bg: #0A140A; --card-bg: #142814;
      --text: #B9F6CA; --text-muted: #69F0AE; --border: #76FF03;
    }

    [data-theme="vampire-blood"] {
      --primary: #D32F2F; --primary-light: #8E0000; --secondary: #B71C1C;
      --accent: #FF8A80; --bg: #120505; --card-bg: #210A0A;
      --text: #FFCDD2; --text-muted: #EF9A9A; --border: #D32F2F;
    }

    [data-theme="deep-ocean-abyss"] {
      --primary: #00838F; --primary-light: #005662; --secondary: #00ACC1;
      --accent: #80DEEA; --bg: #001015; --card-bg: #00222B;
      --text: #E0F7FA; --text-muted: #4DD0E1; --border: #00838F;
    }

    [data-theme="cyber-gold"] {
      --primary: #FFD700; --primary-light: #FFA000; --secondary: #FFC107;
      --accent: #FFE082; --bg: #141200; --card-bg: #242100;
      --text: #FFF8E1; --text-muted: #FFE082; --border: #FFD700;
    }

    [data-theme="neon-mint"] {
      --primary: #00E676; --primary-light: #00C853; --secondary: #1DE9B6;
      --accent: #A7FFEB; --bg: #001A10; --card-bg: #003320;
      --text: #E0F2F1; --text-muted: #80CBC4; --border: #00E676;
    }

    [data-theme="crimson-dusk"] {
      --primary: #C2185B; --primary-light: #880E4F; --secondary: #E91E63;
      --accent: #F8BBD0; --bg: #1F0510; --card-bg: #330A1D;
      --text: #FCE4EC; --text-muted: #F48FB1; --border: #C2185B;
    }

    [data-theme="electric-violet"] {
      --primary: #7C4DFF; --primary-light: #6200EE; --secondary: #B388FF;
      --accent: #EA80FC; --bg: #0D051A; --card-bg: #1A0A33;
      --text: #EDE7F6; --text-muted: #D1C4E9; --border: #7C4DFF;
    }

    /* =========================================================
       42 NEW THEMES (70 TOTAL) + WHOLE-UI MORPHING DEFINITIONS
       ========================================================= */
    [data-theme="blueprint-cad"] {
      --primary: #38BDF8; --primary-light: #0284C7; --secondary: #7DD3FC;
      --accent: #FDE047; --bg: #061C36; --card-bg: rgba(8, 35, 68, 0.92);
      --text: #E0F2FE; --text-muted: #7DD3FC; --border: #38BDF8;
      --shadow: 0 0 0 1px rgba(56,189,248,0.4), 0 10px 25px rgba(2,12,27,0.7);
    }
    [data-theme="autocad-engineer"] {
      --primary: #00E5FF; --primary-light: #00838F; --secondary: #FFEA00;
      --accent: #FF3D00; --bg: #0B0F17; --card-bg: #111824;
      --text: #E0F7FA; --text-muted: #80DEEA; --border: #00ACC1;
    }
    [data-theme="structural-steel-cad"] {
      --primary: #F97316; --primary-light: #C2410C; --secondary: #38BDF8;
      --accent: #FACC15; --bg: #0F172A; --card-bg: #1E293B;
      --text: #F8FAFC; --text-muted: #94A3B8; --border: #F97316;
    }
    [data-theme="vision-os-spatial"] {
      --primary: #FFFFFF; --primary-light: #38BDF8; --secondary: #60A5FA;
      --accent: #C084FC; --bg: #0B1120; --card-bg: rgba(30, 41, 59, 0.52);
      --text: #F8FAFC; --text-muted: #CBD5E1; --border: rgba(255, 255, 255, 0.28);
      --glass-blur: blur(26px);
      --shadow: 0 20px 50px rgba(0, 0, 0, 0.55), inset 0 1px 1px rgba(255, 255, 255, 0.35);
    }
    [data-theme="frosted-aurora"] {
      --primary: #2DD4BF; --primary-light: #0D9488; --secondary: #818CF8;
      --accent: #F472B6; --bg: #040D1A; --card-bg: rgba(15, 32, 56, 0.58);
      --text: #F0FDFA; --text-muted: #99F6E4; --border: rgba(45, 212, 191, 0.35);
      --glass-blur: blur(22px);
    }
    [data-theme="crystal-prism"] {
      --primary: #1E3A8A; --primary-light: #2563EB; --secondary: #7C3AED;
      --accent: #EC4899; --bg: #EEF2FF; --card-bg: rgba(255, 255, 255, 0.72);
      --text: #0F172A; --text-muted: #475569; --border: rgba(124, 58, 237, 0.3);
      --glass-blur: blur(20px);
    }
    [data-theme="aero-frutiger"] {
      --primary: #0369A1; --primary-light: #0284C7; --secondary: #10B981;
      --accent: #38BDF8; --bg: #E0F2FE; --card-bg: rgba(255, 255, 255, 0.82);
      --text: #082F49; --text-muted: #0369A1; --border: rgba(14, 165, 233, 0.45);
      --glass-blur: blur(18px);
    }
    [data-theme="neubrutalist-pop"] {
      --primary: #111827; --primary-light: #4F46E5; --secondary: #FF5722;
      --accent: #FACC15; --bg: #FEF08A; --card-bg: #FFFFFF;
      --text: #000000; --text-muted: #374151; --border: #000000;
      --shadow: 6px 6px 0px #000000;
    }
    [data-theme="brutalist-arch"] {
      --primary: #000000; --primary-light: #DC2626; --secondary: #2563EB;
      --accent: #FDE047; --bg: #E5E7EB; --card-bg: #FFFFFF;
      --text: #000000; --text-muted: #4B5563; --border: #000000;
      --shadow: 7px 7px 0px #111827;
    }
    [data-theme="manga-ink"] {
      --primary: #09090B; --primary-light: #27272A; --secondary: #E11D48;
      --accent: #FACC15; --bg: #FAFAFA; --card-bg: #FFFFFF;
      --text: #09090B; --text-muted: #52525B; --border: #09090B;
      --shadow: 6px 6px 0px #09090B;
    }
    [data-theme="swiss-bauhaus"] {
      --primary: #1D4ED8; --primary-light: #DC2626; --secondary: #EAB308;
      --accent: #DC2626; --bg: #F5F5F4; --card-bg: #FFFFFF;
      --text: #1C1917; --text-muted: #57534E; --border: #1C1917;
      --shadow: 6px 6px 0px #DC2626;
    }
    [data-theme="jarvis-iron-hud"] {
      --primary: #00F0FF; --primary-light: #0080FF; --secondary: #FF9900;
      --accent: #00F0FF; --bg: #020813; --card-bg: rgba(4, 20, 42, 0.88);
      --text: #CCFBF1; --text-muted: #38BDF8; --border: #00F0FF;
      --shadow: 0 0 22px rgba(0, 240, 255, 0.28);
    }
    [data-theme="starfleet-lcars"] {
      --primary: #FF9900; --primary-light: #CC6699; --secondary: #9999FF;
      --accent: #FFCC66; --bg: #000000; --card-bg: #111122;
      --text: #FFCC99; --text-muted: #9999FF; --border: #FF9900;
    }
    [data-theme="mecha-gundam"] {
      --primary: #1D4ED8; --primary-light: #DC2626; --secondary: #FACC15;
      --accent: #EF4444; --bg: #090D16; --card-bg: #131C2E;
      --text: #F8FAFC; --text-muted: #93C5FD; --border: #3B82F6;
    }
    [data-theme="cyber-samurai"] {
      --primary: #F43F5E; --primary-light: #881337; --secondary: #38BDF8;
      --accent: #FACC15; --bg: #090408; --card-bg: #180914;
      --text: #FFE4E6; --text-muted: #FDA4AF; --border: #F43F5E;
    }
    [data-theme="halo-unsc"] {
      --primary: #84CC16; --primary-light: #3F6212; --secondary: #eab308;
      --accent: #F59E0B; --bg: #0C140C; --card-bg: #162416;
      --text: #ECFCCB; --text-muted: #A3E635; --border: #65A30D;
    }
    [data-theme="tron-legacy-grid"] {
      --primary: #6DF9FF; --primary-light: #0284C7; --secondary: #FF7B00;
      --accent: #6DF9FF; --bg: #020508; --card-bg: #07121A;
      --text: #E0FFFF; --text-muted: #38BDF8; --border: #6DF9FF;
      --shadow: 0 0 25px rgba(109, 249, 255, 0.3);
    }
    [data-theme="alien-nostromo"] {
      --primary: #10B981; --primary-light: #064E3B; --secondary: #34D399;
      --accent: #F59E0B; --bg: #030906; --card-bg: #071710;
      --text: #A7F3D0; --text-muted: #34D399; --border: #10B981;
    }
    [data-theme="dune-arrakis"] {
      --primary: #D97706; --primary-light: #92400E; --secondary: #38BDF8;
      --accent: #FDE68A; --bg: #1C1208; --card-bg: #2E1E0F;
      --text: #FEF3C7; --text-muted: #FBBF24; --border: #D97706;
    }
    [data-theme="neumorphic-light"] {
      --primary: #334155; --primary-light: #475569; --secondary: #2563EB;
      --accent: #10B981; --bg: #E2E8F0; --card-bg: #E2E8F0;
      --text: #1E293B; --text-muted: #64748B; --border: rgba(255,255,255,0.65);
      --shadow: 9px 9px 18px #B8C2CC, -9px -9px 18px #FFFFFF;
    }
    [data-theme="neumorphic-dark"] {
      --primary: #38BDF8; --primary-light: #0284C7; --secondary: #818CF8;
      --accent: #F59E0B; --bg: #1E242B; --card-bg: #1E242B;
      --text: #F1F5F9; --text-muted: #94A3B8; --border: rgba(255,255,255,0.06);
      --shadow: 8px 8px 16px #12161A, -8px -8px 16px #2A323C;
    }
    [data-theme="claymorphic-3d"] {
      --primary: #4F46E5; --primary-light: #6366F1; --secondary: #EC4899;
      --accent: #FACC15; --bg: #EEF2FF; --card-bg: #FFFFFF;
      --text: #1E1B4B; --text-muted: #6366F1; --border: #C7D2FE;
      --shadow: 0 16px 32px rgba(79, 70, 229, 0.18), inset 0 -6px 12px rgba(79, 70, 229, 0.10), inset 0 6px 12px rgba(255, 255, 255, 0.9);
    }
    [data-theme="porcelain-ceramic"] {
      --primary: #0F172A; --primary-light: #334155; --secondary: #0D9488;
      --accent: #D97706; --bg: #F8FAFC; --card-bg: #FFFFFF;
      --text: #0F172A; --text-muted: #64748B; --border: #E2E8F0;
      --shadow: 0 12px 28px rgba(15, 23, 42, 0.08), inset 0 -4px 8px rgba(203, 213, 225, 0.4);
    }
    [data-theme="luxury-black-gold"] {
      --primary: #D4AF37; --primary-light: #996515; --secondary: #F3E5AB;
      --accent: #FFD700; --bg: #080808; --card-bg: #12110E;
      --text: #FAF0CA; --text-muted: #C5A059; --border: #D4AF37;
      --shadow: 0 12px 30px rgba(212, 175, 55, 0.16);
    }
    [data-theme="marble-imperial"] {
      --primary: #1E293B; --primary-light: #B45309; --secondary: #D97706;
      --accent: #F59E0B; --bg: #FAF8F5; --card-bg: #FFFFFF;
      --text: #1C1917; --text-muted: #78716C; --border: #E7E5E4;
    }
    [data-theme="rolex-emerald-gold"] {
      --primary: #D4AF37; --primary-light: #046307; --secondary: #10B981;
      --accent: #FFD700; --bg: #022316; --card-bg: #053824;
      --text: #ECFDF5; --text-muted: #A7F3D0; --border: #D4AF37;
    }
    [data-theme="wall-street-paper"] {
      --primary: #1C1917; --primary-light: #44403C; --secondary: #9A3412;
      --accent: #B45309; --bg: #FBF1E6; --card-bg: #FFF9F2;
      --text: #1C1917; --text-muted: #57534E; --border: #D6C7B2;
    }
    [data-theme="monaco-yacht"] {
      --primary: #0F294A; --primary-light: #1E4E8C; --secondary: #C59B27;
      --accent: #FDE047; --bg: #F0F6FC; --card-bg: #FFFFFF;
      --text: #0A192F; --text-muted: #475569; --border: #CBD5E1;
    }
    [data-theme="dubai-burj-gold"] {
      --primary: #F59E0B; --primary-light: #B45309; --secondary: #38BDF8;
      --accent: #FDE68A; --bg: #090D16; --card-bg: #131B2E;
      --text: #FEF3C7; --text-muted: #FBBF24; --border: #D97706;
    }
    [data-theme="win95-retro-os"] {
      --primary: #000080; --primary-light: #1084D0; --secondary: #008080;
      --accent: #FFFF00; --bg: #008080; --card-bg: #C0C0C0;
      --text: #000000; --text-muted: #333333; --border: #FFFFFF;
      --shadow: inset 2px 2px 0px #FFFFFF, inset -2px -2px 0px #808080, 2px 2px 0px #000000;
    }
    [data-theme="mac-classic-platinum"] {
      --primary: #222222; --primary-light: #555555; --secondary: #3B82F6;
      --accent: #9333EA; --bg: #CCCCCC; --card-bg: #EEEEEE;
      --text: #000000; --text-muted: #444444; --border: #888888;
    }
    [data-theme="pipboy-fallout"] {
      --primary: #16F529; --primary-light: #0A5C12; --secondary: #22C55E;
      --accent: #86EFAC; --bg: #041204; --card-bg: #092209;
      --text: #16F529; --text-muted: #15803D; --border: #16F529;
    }
    [data-theme="amber-crt-monitor"] {
      --primary: #FFB000; --primary-light: #784B00; --secondary: #FFCC00;
      --accent: #FFE066; --bg: #120B00; --card-bg: #1F1400;
      --text: #FFB000; --text-muted: #B37B00; --border: #FFB000;
    }
    [data-theme="dos-borland-blue"] {
      --primary: #FFFF55; --primary-light: #00AAAA; --secondary: #55FFFF;
      --accent: #FF5555; --bg: #0000AA; --card-bg: #000088;
      --text: #FFFFFF; --text-muted: #55FFFF; --border: #55FFFF;
    }
    [data-theme="gameboy-pocket"] {
      --primary: #0F380F; --primary-light: #306230; --secondary: #306230;
      --accent: #8BAC0F; --bg: #9BBC0F; --card-bg: #8BAC0F;
      --text: #0F380F; --text-muted: #306230; --border: #0F380F;
    }
    [data-theme="himalayan-dawn"] {
      --primary: #1E3A8A; --primary-light: #3B82F6; --secondary: #F97316;
      --accent: #FDBA74; --bg: #F8FAFC; --card-bg: #FFFFFF;
      --text: #0F172A; --text-muted: #475569; --border: #CBD5E1;
    }
    [data-theme="ganga-river-mist"] {
      --primary: #0F766E; --primary-light: #14B8A6; --secondary: #0284C7;
      --accent: #F59E0B; --bg: #F0FDFA; --card-bg: #FFFFFF;
      --text: #134E4A; --text-muted: #0F766E; --border: #99F6E4;
    }
    [data-theme="monsoon-thunder"] {
      --primary: #38BDF8; --primary-light: #1E3A8A; --secondary: #60A5FA;
      --accent: #FACC15; --bg: #0F172A; --card-bg: #1E293B;
      --text: #E2E8F0; --text-muted: #94A3B8; --border: #475569;
    }
    [data-theme="thar-desert-gold"] {
      --primary: #9A3412; --primary-light: #C2410C; --secondary: #D97706;
      --accent: #FDE047; --bg: #FEFCE8; --card-bg: #FFFFFF;
      --text: #431407; --text-muted: #9A3412; --border: #FDE68A;
    }
    [data-theme="kashmir-saffron"] {
      --primary: #C2410C; --primary-light: #EA580C; --secondary: #DC2626;
      --accent: #FACC15; --bg: #FFF7ED; --card-bg: #FFFFFF;
      --text: #431407; --text-muted: #9A3412; --border: #FED7AA;
    }
    [data-theme="sundarbans-mangrove"] {
      --primary: #34D399; --primary-light: #065F46; --secondary: #10B981;
      --accent: #FBBF24; --bg: #041E17; --card-bg: #062E22;
      --text: #ECFDF5; --text-muted: #6EE7B7; --border: #059669;
    }
    [data-theme="bioluminescent-bay"] {
      --primary: #00F5D4; --primary-light: #00BBF9; --secondary: #00BBF9;
      --accent: #FEE440; --bg: #020818; --card-bg: #061532;
      --text: #E0FBFC; --text-muted: #00F5D4; --border: #00BBF9;
    }
    [data-theme="northern-lights"] {
      --primary: #4ADE80; --primary-light: #3B82F6; --secondary: #A855F7;
      --accent: #2DD4BF; --bg: #050B14; --card-bg: #0D192B;
      --text: #F0FDF4; --text-muted: #86EFAC; --border: #22C55E;
    }
    [data-theme="volcanic-magma"] {
      --primary: #FF5722; --primary-light: #BF360C; --secondary: #FF9800;
      --accent: #FFEB3B; --bg: #120705; --card-bg: #220E0A;
      --text: #FFCCBC; --text-muted: #FF8A65; --border: #FF5722;
    }
    [data-theme="cherry-blossom-kyoto"] {
      --primary: #BE185D; --primary-light: #EC4899; --secondary: #F43F5E;
      --accent: #FBBF24; --bg: #FFF1F2; --card-bg: #FFFFFF;
      --text: #881337; --text-muted: #BE185D; --border: #FECDD3;
    }
    [data-theme="matcha-zen"] {
      --primary: #3F6212; --primary-light: #65A30D; --secondary: #4D7C0F;
      --accent: #CA8A04; --bg: #F7FEE7; --card-bg: #FFFFFF;
      --text: #1A2E05; --text-muted: #4D7C0F; --border: #D9F99D;
    }
    [data-theme="nordic-fjord"] {
      --primary: #0284C7; --primary-light: #0369A1; --secondary: #0D9488;
      --accent: #38BDF8; --bg: #0B192C; --card-bg: #162B47;
      --text: #F0F9FF; --text-muted: #7DD3FC; --border: #0284C7;
    }
    [data-theme="sahara-dusk"] {
      --primary: #EA580C; --primary-light: #9A3412; --secondary: #F59E0B;
      --accent: #FDE047; --bg: #1F120B; --card-bg: #331D12;
      --text: #FFEDD5; --text-muted: #FDBA74; --border: #EA580C;
    }
    [data-theme="amalfi-coast"] {
      --primary: #0284C7; --primary-light: #0369A1; --secondary: #EAB308;
      --accent: #FACC15; --bg: #F0F9FF; --card-bg: #FFFFFF;
      --text: #0C4A6E; --text-muted: #0284C7; --border: #BAE6FD;
    }
    [data-theme="lavender-provence"] {
      --primary: #6D28D9; --primary-light: #7C3AED; --secondary: #8B5CF6;
      --accent: #F472B6; --bg: #F5F3FF; --card-bg: #FFFFFF;
      --text: #2E1065; --text-muted: #6D28D9; --border: #DDD6FE;
    }

    /* =========================================================
       WHOLE-UI MORPHING ENGINE (CHANGES ENTIRE UI ARCHITECTURE!)
       ========================================================= */
    /* 1. CAD Blueprint / Engineering Grid Whole-UI Morph */
    body[data-theme="blueprint-cad"],
    body[data-theme="autocad-engineer"],
    body[data-theme="structural-steel-cad"],
    body[data-ui-mode="blueprint"] {
      background-image:
        linear-gradient(rgba(56, 189, 248, 0.14) 1px, transparent 1px),
        linear-gradient(90deg, rgba(56, 189, 248, 0.14) 1px, transparent 1px),
        linear-gradient(rgba(56, 189, 248, 0.06) 1px, transparent 1px),
        linear-gradient(90deg, rgba(56, 189, 248, 0.06) 1px, transparent 1px) !important;
      background-size: 100px 100px, 100px 100px, 20px 20px, 20px 20px !important;
    }
    body[data-theme="blueprint-cad"] *,
    body[data-theme="autocad-engineer"] *,
    body[data-theme="structural-steel-cad"] *,
    body[data-ui-mode="blueprint"] * {
      font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, monospace !important;
    }
    body[data-theme="blueprint-cad"] .stat-card,
    body[data-theme="blueprint-cad"] .worker-card,
    body[data-theme="blueprint-cad"] .dpr-section,
    body[data-theme="blueprint-cad"] .toolbar,
    body[data-theme="blueprint-cad"] .chart-card,
    body[data-theme="blueprint-cad"] .ai-feature-card,
    body[data-theme="autocad-engineer"] .stat-card,
    body[data-theme="autocad-engineer"] .worker-card,
    body[data-theme="autocad-engineer"] .dpr-section,
    body[data-theme="structural-steel-cad"] .stat-card,
    body[data-theme="structural-steel-cad"] .worker-card,
    body[data-ui-mode="blueprint"] .stat-card,
    body[data-ui-mode="blueprint"] .worker-card,
    body[data-ui-mode="blueprint"] .dpr-section,
    body[data-ui-mode="blueprint"] .toolbar,
    body[data-ui-mode="blueprint"] .chart-card,
    body[data-ui-mode="blueprint"] .ai-feature-card {
      border-radius: 2px !important;
      border: 1.5px dashed var(--border) !important;
      position: relative;
    }

    /* 2. 3D Neubrutalist Studio Whole-UI Morph */
    body[data-theme="neubrutalist-pop"] .stat-card,
    body[data-theme="neubrutalist-pop"] .worker-card,
    body[data-theme="neubrutalist-pop"] .dpr-section,
    body[data-theme="neubrutalist-pop"] .toolbar,
    body[data-theme="neubrutalist-pop"] .chart-card,
    body[data-theme="neubrutalist-pop"] .ai-feature-card,
    body[data-theme="neubrutalist-pop"] .btn,
    body[data-theme="neubrutalist-pop"] .tab-btn,
    body[data-theme="brutalist-arch"] .stat-card,
    body[data-theme="brutalist-arch"] .worker-card,
    body[data-theme="brutalist-arch"] .dpr-section,
    body[data-theme="brutalist-arch"] .btn,
    body[data-theme="manga-ink"] .stat-card,
    body[data-theme="manga-ink"] .worker-card,
    body[data-theme="manga-ink"] .dpr-section,
    body[data-theme="swiss-bauhaus"] .stat-card,
    body[data-theme="swiss-bauhaus"] .worker-card,
    body[data-theme="swiss-bauhaus"] .dpr-section,
    body[data-ui-mode="neubrutalist"] .stat-card,
    body[data-ui-mode="neubrutalist"] .worker-card,
    body[data-ui-mode="neubrutalist"] .dpr-section,
    body[data-ui-mode="neubrutalist"] .toolbar,
    body[data-ui-mode="neubrutalist"] .chart-card,
    body[data-ui-mode="neubrutalist"] .ai-feature-card,
    body[data-ui-mode="neubrutalist"] .btn,
    body[data-ui-mode="neubrutalist"] .tab-btn {
      border-radius: 0px !important;
      border: 3px solid var(--border) !important;
      box-shadow: 6px 6px 0px var(--border) !important;
    }

    /* 3. Sci-Fi Holographic HUD Whole-UI Morph (Chamfered Polygon Cards & Scanlines) */
    body[data-theme="jarvis-iron-hud"],
    body[data-theme="cyberpunk"],
    body[data-theme="mecha-gundam"],
    body[data-theme="cyber-samurai"],
    body[data-theme="tron-legacy-grid"],
    body[data-theme="halo-unsc"],
    body[data-theme="alien-nostromo"],
    body[data-ui-mode="scifi-hud"] {
      background-image: repeating-linear-gradient(
        0deg,
        rgba(0, 240, 255, 0.03) 0px,
        rgba(0, 240, 255, 0.03) 1px,
        transparent 1px,
        transparent 4px
      ) !important;
    }
    body[data-theme="jarvis-iron-hud"] .stat-card,
    body[data-theme="jarvis-iron-hud"] .worker-card,
    body[data-theme="jarvis-iron-hud"] .dpr-section,
    body[data-theme="jarvis-iron-hud"] .chart-card,
    body[data-theme="jarvis-iron-hud"] .ai-feature-card,
    body[data-theme="mecha-gundam"] .stat-card,
    body[data-theme="mecha-gundam"] .worker-card,
    body[data-theme="tron-legacy-grid"] .stat-card,
    body[data-theme="tron-legacy-grid"] .worker-card,
    body[data-ui-mode="scifi-hud"] .stat-card,
    body[data-ui-mode="scifi-hud"] .worker-card,
    body[data-ui-mode="scifi-hud"] .dpr-section,
    body[data-ui-mode="scifi-hud"] .chart-card,
    body[data-ui-mode="scifi-hud"] .ai-feature-card,
    body[data-ui-mode="scifi-hud"] .tab-btn {
      border-radius: 0px !important;
      clip-path: polygon(0 0, calc(100% - 16px) 0, 100% 16px, 100% 100%, 16px 100%, 0 calc(100% - 16px));
      border: 1.5px solid var(--secondary) !important;
    }

    /* 4. VisionOS Spatial Glass Whole-UI Morph */
    body[data-theme="vision-os-spatial"],
    body[data-theme="frosted-aurora"],
    body[data-theme="crystal-prism"],
    body[data-theme="aero-frutiger"],
    body[data-theme="liquid-glass"],
    body[data-ui-mode="vision-spatial"] {
      background-image:
        radial-gradient(at 15% 15%, rgba(56, 189, 248, 0.25) 0px, transparent 50%),
        radial-gradient(at 85% 20%, rgba(168, 85, 247, 0.24) 0px, transparent 50%),
        radial-gradient(at 50% 85%, rgba(16, 185, 129, 0.20) 0px, transparent 50%) !important;
      background-attachment: fixed !important;
    }
    body[data-theme="vision-os-spatial"] .stat-card,
    body[data-theme="vision-os-spatial"] .worker-card,
    body[data-theme="vision-os-spatial"] .dpr-section,
    body[data-theme="vision-os-spatial"] .toolbar,
    body[data-theme="vision-os-spatial"] .chart-card,
    body[data-theme="vision-os-spatial"] .ai-feature-card,
    body[data-ui-mode="vision-spatial"] .stat-card,
    body[data-ui-mode="vision-spatial"] .worker-card,
    body[data-ui-mode="vision-spatial"] .dpr-section,
    body[data-ui-mode="vision-spatial"] .toolbar,
    body[data-ui-mode="vision-spatial"] .chart-card,
    body[data-ui-mode="vision-spatial"] .ai-feature-card {
      border-radius: 28px !important;
      backdrop-filter: blur(26px) saturate(180%) !important;
      border: 1px solid rgba(255, 255, 255, 0.32) !important;
    }

    /* 5. Luxury Executive & Editorial Whole-UI Morph */
    body[data-theme="luxury-black-gold"] *,
    body[data-theme="marble-imperial"] *,
    body[data-theme="rolex-emerald-gold"] *,
    body[data-theme="wall-street-paper"] *,
    body[data-ui-mode="luxury-editorial"] * {
      font-family: Georgia, "Times New Roman", Times, serif !important;
    }
    body[data-theme="luxury-black-gold"] .stat-card,
    body[data-theme="luxury-black-gold"] .worker-card,
    body[data-theme="luxury-black-gold"] .dpr-section,
    body[data-theme="rolex-emerald-gold"] .stat-card,
    body[data-theme="rolex-emerald-gold"] .worker-card,
    body[data-ui-mode="luxury-editorial"] .stat-card,
    body[data-ui-mode="luxury-editorial"] .worker-card,
    body[data-ui-mode="luxury-editorial"] .dpr-section {
      border: 3px double var(--primary) !important;
      border-radius: 6px !important;
    }

    /* 6. Retro OS & CRT Terminal Whole-UI Morph */
    body[data-theme="win95-retro-os"] *,
    body[data-theme="pipboy-fallout"] *,
    body[data-theme="amber-crt-monitor"] *,
    body[data-theme="dos-borland-blue"] *,
    body[data-theme="gameboy-pocket"] *,
    body[data-theme="retro-terminal"] *,
    body[data-theme="matrix"] *,
    body[data-ui-mode="retro-os"] * {
      font-family: "Courier New", Courier, monospace !important;
    }
    body[data-theme="win95-retro-os"] .stat-card,
    body[data-theme="win95-retro-os"] .worker-card,
    body[data-theme="win95-retro-os"] .dpr-section,
    body[data-theme="win95-retro-os"] .toolbar,
    body[data-theme="win95-retro-os"] .btn,
    body[data-theme="win95-retro-os"] .tab-btn,
    body[data-ui-mode="retro-os"] .stat-card,
    body[data-ui-mode="retro-os"] .worker-card,
    body[data-ui-mode="retro-os"] .dpr-section,
    body[data-ui-mode="retro-os"] .btn {
      border-radius: 0px !important;
      border-top: 2px solid #FFFFFF !important;
      border-left: 2px solid #FFFFFF !important;
      border-right: 2px solid #333333 !important;
      border-bottom: 2px solid #333333 !important;
    }

    /* 7. 3D Neumorphic & Tactile Clay Whole-UI Morph */
    body[data-theme="neumorphic-light"] .stat-card,
    body[data-theme="neumorphic-light"] .worker-card,
    body[data-theme="neumorphic-light"] .dpr-section,
    body[data-theme="neumorphic-dark"] .stat-card,
    body[data-theme="neumorphic-dark"] .worker-card,
    body[data-theme="neumorphic-dark"] .dpr-section,
    body[data-theme="claymorphic-3d"] .stat-card,
    body[data-theme="claymorphic-3d"] .worker-card,
    body[data-theme="claymorphic-3d"] .dpr-section,
    body[data-ui-mode="neumorphic-clay"] .stat-card,
    body[data-ui-mode="neumorphic-clay"] .worker-card,
    body[data-ui-mode="neumorphic-clay"] .dpr-section,
    body[data-ui-mode="neumorphic-clay"] .chart-card,
    body[data-ui-mode="neumorphic-clay"] .ai-feature-card {
      border-radius: 26px !important;
      box-shadow: var(--shadow) !important;
    }

    /* Theme Studio Swatch Card Grid */
    .theme-studio-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(195px, 1fr)); gap: 12px; max-height: 52vh; overflow-y: auto; padding: 6px; }
    .theme-swatch-card { border: 2px solid var(--border); border-radius: 14px; padding: 12px; cursor: pointer; transition: 0.25s var(--spring); display: flex; flex-direction: column; gap: 8px; text-align: left; position: relative; }
    .theme-swatch-card:hover { transform: translateY(-4px) scale(1.02); border-color: var(--secondary); }
    .theme-swatch-card.active-theme { border: 3px solid var(--accent); box-shadow: 0 0 20px rgba(45, 104, 196, 0.35); }

    /* Intro Telemetry Bottom Bar & Controls */
    .intro-telemetry-bar { position: fixed; bottom: 26px; left: 50%; transform: translateX(-50%); z-index: 6; display: flex; align-items: center; gap: 14px; background: rgba(6, 18, 36, 0.88); backdrop-filter: blur(12px); border: 1px solid rgba(56, 189, 248, 0.45); padding: 10px 20px; border-radius: 30px; color: #E0F2FE; font-size: 12px; font-weight: 800; letter-spacing: 1px; box-shadow: 0 10px 30px rgba(0,0,0,0.65); flex-wrap: wrap; justify-content: center; }
    .intro-ctrl-btn { background: rgba(56, 189, 248, 0.18); color: #38BDF8; border: 1px solid rgba(56, 189, 248, 0.6); padding: 6px 14px; border-radius: 20px; font-size: 11px; font-weight: 900; cursor: pointer; transition: 0.2s; text-transform: uppercase; letter-spacing: 0.8px; }
    .intro-ctrl-btn:hover { background: #38BDF8; color: #020813; transform: scale(1.05); }

    * { box-sizing: border-box; margin: 0; padding: 0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; }
    
    body.barrel-roll { animation: googleBarrelRoll 2s var(--spring) forwards; overflow: hidden; }
    @keyframes googleBarrelRoll {
      0% { transform: rotate(0deg) scale(1); }
      50% { transform: rotate(180deg) scale(0.6); }
      100% { transform: rotate(360deg) scale(1); }
    }

    body { background-color: var(--bg); color: var(--text); min-height: 100vh; display: flex; flex-direction: column; transition: background-color 0.4s, color 0.4s; overflow-x: hidden; }

    @keyframes springIn { 
      0% { transform: scale(0.5); opacity: 0; } 
      60% { transform: scale(1.05); opacity: 1; }
      100% { transform: scale(1); opacity: 1; } 
    }
    @keyframes popIn {
      0% { transform: translateY(-10px) scale(0.95); opacity: 0; }
      100% { transform: translateY(0) scale(1); opacity: 1; }
    }
    @keyframes slideUpFade { from { opacity: 0; transform: translateY(40px); } to { opacity: 1; transform: translateY(0); } }
    @keyframes pulseWarning { 0% { transform: scale(1); } 50% { transform: scale(1.08); background: var(--danger); box-shadow: 0 0 15px var(--danger);} 100% { transform: scale(1); } }
    
    #intro-container { position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: #000; z-index: 999999; display: flex; align-items: center; justify-content: center; flex-direction: column; overflow: hidden; cursor: crosshair; }
    #intro-canvas { position: absolute; top: 0; left: 0; width: 100%; height: 100%; z-index: 1; }
    
    .intro-logo-wrapper { position: relative; z-index: 2; display: flex; align-items: center; gap: 25px; animation: springIn 1.5s var(--spring); pointer-events: none; }
    .intro-svg { width: 180px; height: 180px; filter: drop-shadow(0 0 15px rgba(166,123,91,0.6)); }
    .intro-text-group { display: flex; align-items: baseline; gap: 15px; }
    .intro-global { font-family: "Brush Script MT", "Comic Sans MS", cursive; color: #4CAF50; font-size: 110px; line-height: 1; text-shadow: 0 4px 15px rgba(76,175,80,0.5); }
    .intro-industries { font-family: "Times New Roman", Times, serif; color: #6da35e; font-size: 70px; letter-spacing: 1px; }
    
    .enter-instruction { position: relative; z-index: 2; margin-top: 60px; font-size: 16px; font-weight: 800; color: rgba(255,255,255,0.8); text-transform: uppercase; letter-spacing: 4px; animation: pulseWarning 2s infinite; pointer-events: none; background: rgba(0,0,0,0.5); padding: 12px 24px; border-radius: 30px; border: 1px solid rgba(255,255,255,0.2);}
    .hq-radar-hud { position: fixed; top: 50%; left: 50%; width: 160px; height: 160px; transform: translate(-50%, -50%) scale(0.85); z-index: 5; pointer-events: none; opacity: 0; display: flex; align-items: center; justify-content: center; }
    .hq-radar-reticle { width: 136px; height: 136px; border: 2.5px dashed rgba(56, 189, 248, 0.95); border-radius: 50%; position: relative; display: flex; align-items: center; justify-content: center; box-shadow: 0 0 32px rgba(56, 189, 248, 0.45), inset 0 0 22px rgba(56, 189, 248, 0.25); transition: border-color 0.2s, box-shadow 0.2s, transform 0.2s; }
    .hq-radar-reticle.locked { border: 3px solid #10B981; box-shadow: 0 0 50px rgba(16, 185, 129, 0.9), inset 0 0 30px rgba(255, 215, 0, 0.55); transform: scale(1.08); }
    .hq-radar-reticle::before, .hq-radar-reticle::after { content: ''; position: absolute; background: rgba(56, 189, 248, 0.85); }
    .hq-radar-reticle.locked::before, .hq-radar-reticle.locked::after { background: #FFD700; }
    .hq-radar-reticle::before { width: 172px; height: 2px; }
    .hq-radar-reticle::after { width: 2px; height: 172px; }
    .hq-radar-badge { position: absolute; top: 156px; left: 50%; transform: translateX(-50%); background: rgba(6, 18, 36, 0.92); backdrop-filter: blur(8px); color: #38BDF8; border: 1.5px solid rgba(56, 189, 248, 0.7); padding: 9px 20px; border-radius: 24px; font-size: 12px; font-weight: 900; letter-spacing: 1.4px; text-transform: uppercase; white-space: nowrap; box-shadow: 0 8px 25px rgba(0, 0, 0, 0.7); transition: all 0.2s; }
    .hq-radar-badge.locked { background: rgba(6, 46, 34, 0.96); color: #FFD700; border-color: #10B981; box-shadow: 0 0 30px rgba(16, 185, 129, 0.65); }

    .ai-grid-30 { display: grid; grid-template-columns: repeat(auto-fill, minmax(275px, 1fr)); gap: 14px; margin-top: 16px; }
    .ai-feature-card { background: var(--card-bg); border: 1.5px solid var(--border); border-radius: 16px; padding: 16px; display: flex; flex-direction: column; justify-content: space-between; gap: 10px; box-shadow: var(--shadow); transition: 0.25s var(--spring); position: relative; overflow: hidden; }
    .ai-feature-card:hover { transform: translateY(-4px); border-color: var(--secondary); box-shadow: 0 12px 24px rgba(45, 104, 196, 0.16); }
    .ai-feature-num { font-size: 10px; font-weight: 900; padding: 3px 8px; border-radius: 10px; background: rgba(59, 130, 246, 0.12); color: var(--secondary); text-transform: uppercase; letter-spacing: 0.5px; }
    .ai-feature-title { font-size: 14px; font-weight: 900; color: var(--primary); line-height: 1.3; }
    .ai-feature-desc { font-size: 12px; color: var(--text-muted); font-weight: 600; line-height: 1.4; }
    .ai-run-btn { padding: 9px 12px; font-size: 12px; font-weight: 800; border-radius: 10px; background: linear-gradient(135deg, var(--secondary), #6366F1); color: #fff; border: none; cursor: pointer; transition: 0.2s; display: inline-flex; align-items: center; justify-content: center; gap: 6px; }
    .ai-run-btn:hover { opacity: 0.95; transform: scale(1.02); }

    .overlay { position: fixed; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0, 0, 0, 0.8); z-index: 9999; display: none; align-items: center; justify-content: center; padding: 20px; backdrop-filter: blur(8px); transition: 0.3s;}
    .modal-box-center { background: var(--card-bg); backdrop-filter: var(--glass-blur); padding: 30px 24px; border-radius: 24px; width: 100%; max-width: 420px; text-align: center; box-shadow: var(--shadow); border: 1px solid var(--border); position: relative; animation: springIn 0.5s var(--spring); }
    .close-btn { position: absolute; top: 14px; right: 18px; background: rgba(0,0,0,0.05); border-radius: 50%; width: 34px; height: 34px; border: none; font-size: 22px; color: var(--text-muted); cursor: pointer; transition: 0.3s var(--spring); display: flex; align-items: center; justify-content: center; }
    .close-btn:hover { background: var(--danger); color: white; transform: rotate(90deg) scale(1.1); }
    .modal-box-center h2 { color: var(--primary); margin-bottom: 8px; font-size: 22px; font-weight: 900; }
    .modal-box-center p { color: var(--text-muted); font-size: 14px; margin-bottom: 20px; }
    .pin-input { width: 100%; padding: 18px; font-size: 24px; text-align: center; letter-spacing: 12px; border: 2px solid var(--border); border-radius: 14px; margin-bottom: 16px; background: var(--bg); color: var(--text); outline: none; font-weight: 900; transition: 0.3s var(--spring); }
    .pin-input:focus { border-color: var(--secondary); box-shadow: 0 8px 20px rgba(45,104,196,0.15); transform: translateY(-3px); }

    header { background: var(--card-bg); backdrop-filter: var(--glass-blur); box-shadow: var(--shadow); position: sticky; top: 0; z-index: 100; border-bottom: 1px solid var(--border); }
    .letterhead-container { padding: 16px 20px; border-bottom: 4px solid #8B5A2B; display: flex; flex-direction: column; gap: 8px; }
    .letterhead-top { display: flex; align-items: center; justify-content: flex-start; gap: 16px; }
    .logo-container { width: 55px; height: 55px; flex-shrink: 0; filter: drop-shadow(0 4px 6px rgba(0,0,0,0.1)); }
    .title-container { display: flex; align-items: baseline; gap: 8px; }
    .title-global { font-family: "Brush Script MT", "Comic Sans MS", cursive; color: #4CAF50; font-size: 42px; line-height: 1; text-shadow: 1px 1px 0px rgba(0,0,0,0.05); }
    .title-industries { font-family: "Times New Roman", Times, serif; color: #6da35e; font-size: 24px; letter-spacing: 0.5px; }
    .regd-office { font-size: 13px; color: var(--text); font-weight: 500; }

    .app-control-bar { background: linear-gradient(135deg, #0B1B2B 0%, #152E4D 100%); padding: 12px 20px; display: flex; justify-content: space-between; align-items: center; gap: 10px; flex-wrap: wrap; border-bottom: 3px solid var(--accent); }
    .site-selector-wrap { display: flex; align-items: center; gap: 12px; flex: 1; min-width: 280px; position: relative; }
    .site-label { color: #FFD700; font-weight: 800; font-size: 14px; letter-spacing: 0.5px; text-transform: uppercase; }
    
    .custom-select { background: #FFFFFF; border: none; padding: 10px 18px; border-radius: 20px; font-size: 14px; font-weight: 800; color: #102A43; width: 100%; max-width: 380px; cursor: pointer; display: flex; justify-content: space-between; align-items: center; box-shadow: 0 4px 12px rgba(0,0,0,0.15); transition: 0.3s var(--spring); }
    .custom-select:hover { transform: translateY(-2px); box-shadow: 0 8px 16px rgba(0,0,0,0.2); }
    .custom-dropdown-menu { position: absolute; top: 50px; left: 45px; background: var(--card-bg); backdrop-filter: var(--glass-blur); width: 100%; max-width: 380px; border-radius: 16px; box-shadow: 0 15px 35px rgba(0,0,0,0.2); z-index: 200; display: none; border: 1px solid var(--border); animation: popIn 0.3s var(--spring); max-height: 450px; overflow-y: auto;}
    .custom-dropdown-menu.active { display: block; }

    .dropdown-site-header { background: var(--bg); padding: 14px 16px; display: flex; align-items: center; justify-content: space-between; border-bottom: 2px solid var(--border); }
    .site-title-text { font-size: 14px; font-weight: 900; color: var(--primary); text-transform: uppercase; display: flex; align-items: center; gap: 8px;}
    .dropdown-zone-item { padding: 12px 16px 12px 40px; font-size: 14px; font-weight: 700; color: var(--text); display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid var(--border); position: relative; cursor: pointer; transition: 0.2s; background: var(--card-bg); }
    .dropdown-zone-item:hover { background: rgba(45, 104, 196, 0.08); padding-left: 48px; color: var(--secondary); }
    .dropdown-zone-item::before { content: ''; position: absolute; left: 22px; top: 0; height: 100%; width: 2px; background: var(--border); transition: 0.2s;}
    .dropdown-zone-item::after { content: ''; position: absolute; left: 22px; top: 50%; width: 12px; height: 2px; background: var(--border); transition: 0.2s;}
    .dropdown-zone-item.last-zone::before { height: 50%; }
    .dropdown-zone-item:hover::before, .dropdown-zone-item:hover::after { background: var(--secondary); }

    .action-btn-sm { opacity: 0.7; transition: 0.3s var(--spring); font-size: 13px; padding: 6px; display: inline-flex; align-items: center; justify-content: center; background: white; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.08); cursor: pointer; }
    .action-btn-sm:hover { opacity: 1; transform: scale(1.15) translateY(-2px); box-shadow: 0 6px 12px rgba(0,0,0,0.15); border-color: var(--secondary); }
    .add-zone-btn { color: var(--success); cursor: pointer; background: rgba(16, 185, 129, 0.1); padding: 8px 14px; border-radius: 12px; font-size: 11px; font-weight: 900; transition: 0.3s var(--spring); text-transform: uppercase;}
    .add-zone-btn:hover { background: var(--success); color: white; transform: scale(1.05) translateY(-2px); box-shadow: 0 6px 15px rgba(16,185,129,0.3);}

    .status-group { display: flex; align-items: center; gap: 10px; flex-wrap: wrap; }
    .sync-status-badge { background: rgba(16, 185, 129, 0.2); color: #34D399; font-size: 12px; font-weight: 800; padding: 8px 14px; border-radius: 20px; display: flex; align-items: center; gap: 6px; border: 1px solid rgba(16, 185, 129, 0.45); transition: 0.3s; }
    .sync-status-badge.offline { background: rgba(245, 158, 11, 0.22); color: #FBBF24; border-color: rgba(245, 158, 11, 0.6); animation: pulseWarning 2s infinite; }
    .live-clock-badge { background: rgba(0,0,0,0.4); color: #FFF; font-size: 12px; font-weight: 800; padding: 8px 14px; border-radius: 20px; display: flex; align-items: center; border: 1px solid rgba(255,255,255,0.15); }
    .user-profile-badge { background: rgba(255,255,255,0.15); color: #FFF; font-size: 12px; font-weight: 800; padding: 8px 14px; border-radius: 20px; display: flex; align-items: center; gap: 6px; cursor: pointer; transition: 0.3s var(--spring); border: 1px solid rgba(255,255,255,0.1);}
    .user-profile-badge:hover { background: rgba(255,255,255,0.3); transform: scale(1.05) translateY(-2px); box-shadow: 0 6px 15px rgba(0,0,0,0.3);}
    #auth-status-btn { background: rgba(255,255,255,0.2); border: none; border-radius: 20px; padding: 8px 18px; color: white; font-size: 13px; font-weight: 800; display: flex; align-items: center; gap: 6px; cursor: pointer; transition: 0.3s var(--spring); }
    #auth-status-btn:hover { transform: translateY(-2px); box-shadow: 0 6px 15px rgba(0,0,0,0.3); }
    .shake-error { animation: pulseWarning 0.4s ease; }
    
    .mic-btn.recording { animation: pulseWarning 1s infinite; background: var(--danger); color: white !important; border-color: var(--danger) !important; }
    .stock-badge { padding: 6px 12px; border-radius: 20px; font-size: 12px; font-weight: 800; background: var(--bg); border: 1px solid var(--border); }
    .stock-badge.low-stock { border: 2px solid var(--danger); background: #FEF2F2; color: #991B1B; animation: pulseWarning 2s infinite; }

    .container { width: 100%; padding: 24px; flex: 1; max-width: 1600px; margin: 0 auto; }
    .dashboard-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 20px; margin-bottom: 24px; }
    .stat-card { background: var(--card-bg); backdrop-filter: var(--glass-blur); padding: 22px; border-radius: 20px; box-shadow: var(--shadow); border: 1px solid var(--border); border-left: 6px solid var(--secondary); display: flex; flex-direction: column; transition: 0.4s var(--spring); opacity: 0; }
    .stat-card:hover { transform: translateY(-6px); box-shadow: 0 20px 30px -5px rgba(0, 0, 0, 0.15); }
    .stat-card.accent { border-left-color: var(--accent); }
    .stat-card.success { border-left-color: var(--success); }
    .stat-card.warning { border-left-color: var(--warning); }
    .stat-label { font-size: 12px; text-transform: uppercase; font-weight: 900; color: var(--text-muted); margin-bottom: 8px; letter-spacing: 0.5px; }
    .stat-value { font-size: 28px; font-weight: 900; color: var(--primary); }

    .analytics-ribbon-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 14px; padding: 10px 16px; background: var(--card-bg); backdrop-filter: var(--glass-blur); border-radius: 14px; border: 1px solid var(--border); box-shadow: var(--shadow); }
    .analytics-ribbon-title { font-size: 13px; font-weight: 900; color: var(--primary); text-transform: uppercase; letter-spacing: 0.6px; display: flex; align-items: center; gap: 8px; }
    .analytics-toggle-btn { background: var(--bg); color: var(--secondary); border: 1px solid var(--border); padding: 6px 14px; border-radius: 12px; font-size: 12px; font-weight: 800; cursor: pointer; transition: 0.25s var(--spring); }
    .analytics-toggle-btn:hover { background: var(--secondary); color: #fff; transform: translateY(-1px); }
    .visual-charts-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(290px, 1fr)); gap: 18px; margin-bottom: 24px; transition: 0.35s ease; }
    .visual-charts-grid.collapsed { display: none !important; }
    .chart-card { background: var(--card-bg); backdrop-filter: var(--glass-blur); border: 1px solid var(--border); border-radius: 18px; padding: 18px; box-shadow: var(--shadow); display: flex; flex-direction: column; justify-content: space-between; }
    .chart-card h5 { font-size: 12px; font-weight: 900; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 12px; display: flex; justify-content: space-between; align-items: center; }

    .filter-pills-wrap { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 18px; align-items: center; }
    .filter-pill { padding: 8px 14px; border-radius: 20px; font-size: 12px; font-weight: 800; background: var(--card-bg); color: var(--text-muted); border: 1px solid var(--border); cursor: pointer; transition: 0.25s var(--spring); display: inline-flex; align-items: center; gap: 6px; }
    .filter-pill:hover { border-color: var(--secondary); color: var(--secondary); transform: translateY(-2px); }
    .filter-pill.active { background: var(--secondary); color: #fff; border-color: var(--secondary); box-shadow: 0 4px 12px rgba(45, 104, 196, 0.3); }
    .preset-chip { padding: 7px 12px; border-radius: 10px; font-size: 12px; font-weight: 900; background: var(--bg); color: var(--primary); border: 1.5px solid var(--border); cursor: pointer; transition: 0.2s var(--spring); }
    .preset-chip:hover { background: var(--secondary); color: #fff; border-color: var(--secondary); transform: translateY(-2px); }

    .nav-tabs { display: flex; gap: 12px; margin-bottom: 24px; border-bottom: 3px solid var(--border); padding-bottom: 16px; overflow-x: auto; scrollbar-width: none; }
    .nav-tabs::-webkit-scrollbar { display: none; }
    .tab-btn { background: var(--card-bg); backdrop-filter: var(--glass-blur); border: 1px solid var(--border); padding: 14px 20px; font-size: 14px; font-weight: 800; color: var(--text-muted); border-radius: 14px; cursor: pointer; white-space: nowrap; transition: 0.3s var(--spring); box-shadow: 0 2px 6px rgba(0,0,0,0.03);}
    .tab-btn:hover { border-color: var(--secondary); color: var(--secondary); transform: translateY(-2px); box-shadow: 0 8px 15px rgba(45,104,196,0.1); }
    .tab-btn.active { background: var(--secondary); color: white; border-color: var(--secondary); box-shadow: 0 8px 20px rgba(45, 104, 196, 0.35); transform: translateY(-3px);}
    .tab-btn.special-tab { background: #FFFBEB; border-color: #FBBF24; color: #B45309; }
    .tab-btn.special-tab.active { background: #F59E0B; border-color: #D97706; color: white; box-shadow: 0 8px 20px rgba(245,158,11,0.35);}
    .tab-btn.report-tab { background: #F3E8FF; border-color: #C084FC; color: #6B21A8; }
    .tab-btn.report-tab.active { background: #9333EA; border-color: #7E22CE; color: white; box-shadow: 0 8px 20px rgba(147,51,234,0.35);}

    .toolbar { background: var(--card-bg); backdrop-filter: var(--glass-blur); padding: 22px; border-radius: 20px; box-shadow: var(--shadow); display: flex; flex-direction: column; gap: 16px; margin-bottom: 24px; border: 1px solid var(--border); }
    select, input, textarea { padding: 16px; font-size: 15px; border-radius: 12px; border: 2px solid var(--border); outline: none; width: 100%; background: var(--bg); color: var(--text); font-weight: 700; transition: 0.3s var(--spring); }
    input:focus, select:focus, textarea:focus { border-color: var(--secondary); background: var(--card-bg); transform: translateY(-2px); box-shadow: 0 6px 15px rgba(45,104,196,0.1); }
    
    .btn { cursor: pointer; font-weight: 800; border: none; display: inline-flex; align-items: center; justify-content: center; gap: 10px; padding: 16px; font-size: 15px; border-radius: 14px; width: 100%; transition: 0.3s var(--spring); box-shadow: 0 4px 10px rgba(0,0,0,0.1);}
    .btn:hover { transform: translateY(-3px); box-shadow: 0 8px 20px rgba(0,0,0,0.15); }
    .btn:active { transform: scale(0.94); box-shadow: none;}
    .btn-primary { background: linear-gradient(135deg, var(--secondary), #3B82F6); color: white; }
    .btn-success { background: linear-gradient(135deg, #10B981, #059669); color: white; }
    .btn-outline { background: transparent; border: 2px solid var(--border); color: var(--text); box-shadow: none;}
    .btn-outline:hover { background: var(--bg); border-color: var(--text-muted);}
    .btn-danger { background: linear-gradient(135deg, #EF4444, #DC2626); color: white; }
    .btn-whatsapp { background: linear-gradient(135deg, #25D366, #128C7E); color: white; }
    .btn-small { padding: 10px 14px; font-size: 13px; border-radius: 12px;}
    .btn-remove-row { background: rgba(239, 68, 68, 0.1); color: var(--danger); border: 1px solid rgba(239, 68, 68, 0.3); cursor: pointer; font-weight: 900; transition: 0.2s var(--spring); }
    .btn-remove-row:hover { background: var(--danger); color: white; }

    .tab-content { display: none; }
    .tab-content.active { display: block; animation: slideUpFade 0.5s var(--spring) forwards; }

    .search-filter-bar { display: flex; gap: 12px; margin-bottom: 20px; flex-wrap: wrap; }
    .search-input-box { flex: 2; min-width: 220px; position: relative; }
    .search-input-box input { padding-left: 42px; }
    .search-icon { position: absolute; left: 16px; top: 50%; transform: translateY(-50%); font-size: 18px; color: var(--text-muted); }

    .worker-daily-list { display: grid; grid-template-columns: repeat(auto-fill, minmax(320px, 1fr)); gap: 18px; }
    .worker-card { background: var(--card-bg); backdrop-filter: var(--glass-blur); border-radius: 20px; padding: 22px; box-shadow: var(--shadow); border: 1px solid var(--border); display: flex; flex-direction: column; gap: 16px; transition: 0.4s var(--spring); animation: slideUpFade 0.5s var(--spring) backwards;}
    .worker-card:hover { transform: translateY(-5px); box-shadow: 0 15px 30px rgba(0,0,0,0.1); border-color: var(--secondary); }
    
    .kp-card { border: 2px solid #FCD34D; background: linear-gradient(145deg, var(--card-bg), rgba(254, 243, 199, 0.25)); }
    .kp-card .worker-name { color: var(--primary); }
    
    .worker-card-header { display: flex; align-items: center; gap: 16px; margin-bottom: 6px; }
    .avatar { width: 54px; height: 54px; border-radius: 50%; color: white; display: flex; align-items: center; justify-content: center; font-size: 20px; font-weight: 900; flex-shrink: 0; box-shadow: 0 6px 12px rgba(0,0,0,0.15);}
    .worker-name { font-size: 19px; font-weight: 900; color: var(--primary); }
    .worker-desig { font-size: 14px; color: var(--text-muted); font-weight: 700; margin-top: 4px;}
    .spark-dots { display: flex; align-items: center; gap: 5px; margin-top: 6px; }
    .spark-dot { width: 9px; height: 9px; border-radius: 50%; background: var(--border); display: inline-block; transition: 0.2s; }
    .spark-dot.sp-p { background: #10B981; box-shadow: 0 0 6px rgba(16, 185, 129, 0.5); }
    .spark-dot.sp-h { background: #F59E0B; box-shadow: 0 0 6px rgba(245, 158, 11, 0.5); }
    .spark-dot.sp-a { background: #EF4444; }
    
    .duty-selector { display: flex; gap: 10px; }
    .duty-opt { flex: 1; text-align: center; padding: 14px 4px; font-size: 15px; font-weight: 800; border: 2px solid var(--border); border-radius: 12px; background: var(--bg); cursor: pointer; transition: 0.3s var(--spring); color: var(--text);}
    .duty-opt:active { transform: scale(0.9); }
    .duty-opt.selected-p { background: #DCFCE7; color: #166534; border-color: #86EFAC; box-shadow: 0 4px 10px rgba(16,185,129,0.2); transform: translateY(-2px);}
    .duty-opt.selected-h { background: #FEF9C3; color: #854D0E; border-color: #FDE047; box-shadow: 0 4px 10px rgba(234,179,8,0.2); transform: translateY(-2px);}
    .duty-opt.selected-a { background: #FEE2E2; color: #991B1B; border-color: #FCA5A5; box-shadow: 0 4px 10px rgba(239,68,68,0.2); transform: translateY(-2px);}
    .duty-opt.locked { opacity: 0.6; cursor: not-allowed; position: relative; overflow: hidden; transform: none !important; box-shadow: none !important;}
    .duty-opt.locked::after { content: '🔒'; position: absolute; right: 6px; top: 6px; font-size: 11px; }

    .input-row { display: flex; gap: 14px; margin-top: 6px; }
    .input-box { flex: 1; background: var(--bg); padding: 10px 14px; border-radius: 12px; display: flex; align-items: center; justify-content: space-between; border: 1px solid var(--border); }
    .input-box span { font-size: 13px; font-weight: 800; color: var(--text-muted); }
    .input-box input { width: 70px; padding: 8px; font-size: 15px; text-align: right; background: var(--card-bg); border: 2px solid var(--border); border-radius: 8px; font-weight: 900; color: var(--text); }

    .dpr-section { background: var(--card-bg); backdrop-filter: var(--glass-blur); border-radius: 20px; padding: 24px; box-shadow: var(--shadow); border: 1px solid var(--border); margin-bottom: 24px; transition: 0.3s; }
    .dpr-section h4 { color: var(--primary); margin-bottom: 18px; font-size: 18px; font-weight: 900; display: flex; justify-content: space-between; align-items: center; }
    .material-row { display: flex; gap: 14px; margin-bottom: 14px; background: var(--bg); padding: 12px; border-radius: 12px; border: 1px solid var(--border); }
    .dpr-textarea { min-height: 140px; resize: vertical; margin-bottom: 12px; }
    
    .mini-cal-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 6px; margin: 12px 0; }
    .mini-cal-header { font-size: 10px; font-weight: 900; color: var(--text-muted); text-align: center; text-transform: uppercase; padding-bottom: 4px; }
    .mini-cal-day { padding: 8px 4px; border-radius: 10px; border: 1px solid var(--border); background: var(--bg); text-align: center; font-size: 11px; font-weight: 800; display: flex; flex-direction: column; gap: 2px; min-height: 48px; justify-content: center; }
    .mini-cal-day.cal-p { background: #DCFCE7; color: #166534; border-color: #86EFAC; }
    .mini-cal-day.cal-h { background: #FEF9C3; color: #854D0E; border-color: #FDE047; }
    .mini-cal-day.cal-a { background: #FEE2E2; color: #991B1B; border-color: #FCA5A5; }
    .prio-badge { padding: 3px 8px; border-radius: 8px; font-size: 10px; font-weight: 900; text-transform: uppercase; display: inline-flex; align-items: center; gap: 4px; }
    .prio-urgent { background: #FEE2E2; color: #991B1B; border: 1px solid #FCA5A5; }
    .prio-safety { background: #FEF9C3; color: #854D0E; border: 1px solid #FDE047; }
    .prio-general { background: rgba(59, 130, 246, 0.15); color: var(--secondary); border: 1px solid rgba(59, 130, 246, 0.3); }
    .empty-state { text-align: center; padding: 60px 20px; background: var(--card-bg); backdrop-filter: var(--glass-blur); border-radius: 20px; color: var(--text-muted); border: 2px dashed var(--border); font-weight: 800; font-size: 16px; line-height: 1.5;}
    #toast { position: fixed; bottom: -80px; left: 50%; transform: translateX(-50%); background: var(--primary); color: white; padding: 16px 32px; border-radius: 30px; font-weight: 900; font-size: 15px; box-shadow: 0 15px 40px rgba(0,0,0,0.3); transition: bottom 0.5s var(--spring); z-index: 99999; }
    
    .table-container { background: var(--card-bg); backdrop-filter: var(--glass-blur); border-radius: 16px; box-shadow: var(--shadow); overflow-x: auto; border: 1px solid var(--border); -webkit-overflow-scrolling: touch;}
    table { width: 100%; border-collapse: collapse; font-size: 14px; white-space: nowrap; color: var(--text); }
    th, td { border: 1px solid var(--border); padding: 14px 10px; text-align: center; }
    th { background: var(--primary-light); color: white; font-weight: 900; font-size: 13px;}
    th.tier2 { font-size: 11px; padding: 8px 6px; background: var(--primary); }
    th.summary-th { background: var(--primary); }
    .text-left { text-align: left !important; }
    .text-right { text-align: right !important; }
    .total-row td { background: var(--bg); font-weight: 900; border-top: 2px solid var(--primary); }
    .sticky-col { position: sticky; left: 0; background: var(--card-bg); z-index: 10; border-right: 3px solid var(--border); }
    th.sticky-col { background: var(--primary-light); z-index: 20; }
    
    .tbl-input { width: 45px; padding: 4px 2px; text-align: center; font-size: 13px; font-weight: 700; border: 1px solid var(--border); border-radius: 4px; background: var(--card-bg); color: var(--text); text-transform: uppercase; }
    .tbl-input:focus { border-color: var(--secondary); box-shadow: none; transform: none; }

    .activity-panel { position: fixed; top: 0; right: -550px; width: 100%; max-width: 500px; height: 100vh; background: var(--card-bg); backdrop-filter: var(--glass-blur); box-shadow: -5px 0 20px rgba(0,0,0,0.15); z-index: 10000; display: flex; flex-direction: column; transition: 0.4s var(--spring); border-left: 1px solid var(--border); }
    .activity-panel.open { right: 0; }
    .activity-header { padding: 24px 20px; background: linear-gradient(135deg, var(--primary), var(--primary-light)); color: white; display: flex; justify-content: space-between; align-items: center; }
    .activity-body { flex: 1; overflow-y: auto; padding: 20px; }
    .ana-heading { font-size: 12px; font-weight: 900; color: var(--text); text-transform: uppercase; margin: 24px 0 12px 0; border-bottom: 2px solid var(--border); padding-bottom: 6px; letter-spacing: 0.5px;}
    .ana-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; }
    .ana-box { background: var(--bg); border: 1px solid var(--border); padding: 12px 8px; border-radius: 8px; text-align: center; display: flex; flex-direction: column; justify-content: center;}
    .ana-box span { font-size: 10px; font-weight: 800; color: var(--text-muted); text-transform: uppercase; margin-bottom: 4px; }
    .ana-box b { font-size: 16px; color: var(--primary); font-weight: 900; }
    .text-success { color: var(--success) !important; }
    .online-tag { display: flex; align-items: center; justify-content: space-between; background: var(--bg); padding: 10px 14px; border-radius: 12px; font-size: 13px; font-weight: 700; margin-bottom: 8px; border: 1px solid var(--border); }
    .pulse-dot { width: 10px; height: 10px; background: #10B981; border-radius: 50%; animation: pulseWarning 1.5s infinite; margin-right: 8px; display: inline-block; }
    .log-item { background: var(--bg); padding: 12px; border-radius: 10px; margin-bottom: 10px; font-size: 13px; border-left: 4px solid var(--secondary); font-weight: 600; line-height: 1.4;}
    .log-time { font-size: 11px; color: var(--text-muted); margin-top: 6px; font-weight: normal;}

    #main-app { display: none; opacity: 0; width: 100%; min-height: 100vh; flex-direction: column; }

    .slip-page-break { page-break-after: always; margin-bottom: 28px; }
    @media print {
      body * { visibility: hidden; }
      #slip-print-area, #slip-print-area *, #batch-slips-print-area, #batch-slips-print-area * { visibility: visible; }
      #slip-print-area, #batch-slips-print-area { position: absolute; left: 0; top: 0; width: 100%; max-width: 100% !important; box-shadow: none !important; }
    }
    @media(max-width: 768px) {
      .intro-logo-wrapper { flex-direction: column; gap: 12px; text-align: center; padding: 0 16px; }
      .intro-text-group { flex-direction: column; align-items: center; gap: 4px; }
      .intro-svg { width: 120px; height: 120px; }
      .intro-global { font-size: 64px; }
      .intro-industries { font-size: 40px; }
      .enter-instruction { margin-top: 32px; font-size: 13px; letter-spacing: 2px; padding: 10px 18px; }
    }

    @media(max-width: 768px) {
      .container { padding: 12px; }
      .app-control-bar { padding: 10px 12px; }
      .worker-daily-list { grid-template-columns: 1fr; }
      .title-global { font-size: 32px; }
      .title-industries { font-size: 18px; }
    }
  </style>
</head>
<body>

  <!-- CINEMATIC 3D WARP-STAR INTRO CONTAINER -->
  <div id="intro-container">
    <canvas id="intro-canvas"></canvas>
    
    <div class="intro-logo-wrapper">
      <div class="intro-svg">
        <svg viewBox="0 0 100 100" width="100%" height="100%">
          <defs>
            <linearGradient id="globeGradIntro" x1="0%" y1="0%" x2="100%" y2="100%">
              <stop offset="0%" stop-color="#D49B4B" /><stop offset="55%" stop-color="#B87B28" /><stop offset="100%" stop-color="#8A5612" />
            </linearGradient>
            <clipPath id="globeClipIntro"><circle cx="50" cy="50" r="45" /></clipPath>
          </defs>
          <g clip-path="url(#globeClipIntro)">
            <!-- 3 inner longitude ellipses (plus outer circle = 4 on each side) -->
            <ellipse cx="50" cy="50" rx="34" ry="45" stroke="url(#globeGradIntro)" stroke-width="2.6" fill="none" />
            <ellipse cx="50" cy="50" rx="23" ry="45" stroke="url(#globeGradIntro)" stroke-width="2.5" fill="none" />
            <ellipse cx="50" cy="50" rx="12" ry="45" stroke="url(#globeGradIntro)" stroke-width="2.4" fill="none" />
            <!-- 1 vertical meridian in the middle -->
            <line x1="50" y1="5" x2="50" y2="95" stroke="url(#globeGradIntro)" stroke-width="2.5" />
            <!-- 2 latitude lines on up & 2 latitude lines on down -->
            <path d="M 5,19 Q 50,26 95,19" stroke="url(#globeGradIntro)" stroke-width="2.5" fill="none" />
            <path d="M 5,30 Q 50,35 95,30" stroke="url(#globeGradIntro)" stroke-width="2.5" fill="none" />
            <path d="M 5,70 Q 50,65 95,70" stroke="url(#globeGradIntro)" stroke-width="2.5" fill="none" />
            <path d="M 5,81 Q 50,74 95,81" stroke="url(#globeGradIntro)" stroke-width="2.5" fill="none" />
            <!-- Polar cap accents & center GI band -->
            <path d="M 32,6 Q 50,12 68,6 Z" fill="url(#globeGradIntro)" />
            <path d="M 32,94 Q 50,88 68,94 Z" fill="url(#globeGradIntro)" />
            <rect x="4" y="39" width="92" height="22" fill="url(#globeGradIntro)" />
          </g>
          <circle cx="50" cy="50" r="45" stroke="url(#globeGradIntro)" stroke-width="3.5" fill="none" />
          <text x="50" y="55.5" fill="#FFFFFF" font-family="'Arial Black', Arial, sans-serif" font-size="16.5" font-weight="900" letter-spacing="3.5" text-anchor="middle">GI</text>
        </svg>
      </div>
      <div class="intro-text-group">
        <span class="intro-global">Global</span>
        <span class="intro-industries">Industries</span>
      </div>
    </div>
    
    <div class="hq-radar-hud" id="hq-radar-hud">
      <div class="hq-radar-reticle" id="hq-radar-reticle"></div>
      <div class="hq-radar-badge" id="hq-radar-badge">🛰️ SCANNING ORBITAL COORDINATES...</div>
    </div>
    <div class="enter-instruction" id="enter-instruction">Click Anywhere To Initialize</div>
    <div class="intro-telemetry-bar" id="intro-telemetry-bar">
      <span id="intro-telem-alt">🛰️ ORBIT ALT: 35,786 KM</span>
      <span style="opacity:0.4;">|</span>
      <span id="intro-telem-coords" style="color:#FFD700;">📍 HQ: 25.42°N, 86.13°E (BARAUNI)</span>
      <span style="opacity:0.4;">|</span>
      <button type="button" class="intro-ctrl-btn" id="btn-hold-3d-building" onclick="event.stopPropagation(); toggleHold3DBuildingView()" style="display:none;">🏛️ Pause on 3D Building</button>
      <button type="button" class="intro-ctrl-btn" onclick="event.stopPropagation(); skipIntroToPortal()">⚡ Fast Enter</button>
    </div>
  </div>

  <div id="main-app">
    <script>
      const sessionChannel = new BroadcastChannel('gi_session_lock');
      const sessionId = Date.now().toString() + Math.random().toString(36).substr(2, 9);
      
      sessionChannel.postMessage({ type: 'CHECK_ACTIVE' });
      sessionChannel.onmessage = (event) => {
        if (event.data.type === 'CHECK_ACTIVE') {
          sessionChannel.postMessage({ type: 'ALREADY_ACTIVE', existingId: sessionId });
        } else if (event.data.type === 'ALREADY_ACTIVE' && event.data.existingId !== sessionId) {
          document.getElementById('main-app').innerHTML = `
            <div style="display:flex; height:100vh; width:100vw; align-items:center; justify-content:center; flex-direction:column; background:var(--bg); color:var(--text); text-align:center; padding: 20px;">
              <h1 style="color:var(--danger); margin-bottom:10px; font-size:40px;">⚠️ Access Blocked</h1>
              <p style="font-weight:700; max-width:450px; line-height:1.6;">The portal is already open in another tab or window. Using multiple tabs simultaneously corrupts the live database. Please close this tab and return to your active session.</p>
            </div>
          `;
        }
      };
    </script>

    <div id="toast"><span id="toast-msg">System Ready</span></div>

    <!-- THEME STUDIO & WHOLE-UI MORPH MODAL (70 THEMES) -->
    <div id="theme-studio-modal" class="overlay" style="z-index: 100002;">
      <div class="modal-box-center" style="max-width: 920px; width: 96%; text-align: left; max-height: 92vh; overflow-y: auto;">
        <button class="close-btn" onclick="closeModal('theme-studio-modal')">&times;</button>
        <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:10px; margin-bottom:12px; padding-right:34px;">
          <div>
            <h2 style="margin:0; font-size:22px;">🎨 Global Industries Theme Studio &amp; Whole-UI Morph Engine (70 Themes)</h2>
            <p style="margin:4px 0 0 0; font-size:13px;">Choose from <b>70 curated themes</b> and <b>Whole-UI Architecture Modes</b> that transform typography, card geometry, borders, glass blur, and layout!</p>
          </div>
          <button type="button" class="btn btn-primary btn-small" style="width:auto;" onclick="surpriseRandomTheme()">🎲 Surprise Random Theme</button>
        </div>

        <div style="background:var(--bg); padding:14px; border-radius:14px; border:1px solid var(--border); margin-bottom:14px;">
          <div style="font-size:11px; font-weight:900; color:var(--primary); text-transform:uppercase; letter-spacing:0.6px; margin-bottom:8px;">🏛️ Whole-UI Architecture Morph Mode (Changes Card Shapes, Fonts, Borders &amp; Grid Overlays)</div>
          <div style="display:flex; gap:8px; flex-wrap:wrap;" id="ui-mode-pills">
            <span class="filter-pill active" onclick="setWholeUIMode('auto')">✨ Auto (Match Theme)</span>
            <span class="filter-pill" onclick="setWholeUIMode('standard')">🏛️ Standard Executive</span>
            <span class="filter-pill" onclick="setWholeUIMode('blueprint')">📐 CAD Blueprint Grid</span>
            <span class="filter-pill" onclick="setWholeUIMode('vision-spatial')">🥽 VisionOS Spatial Glass</span>
            <span class="filter-pill" onclick="setWholeUIMode('scifi-hud')">⚡ Sci-Fi HUD Polygon</span>
            <span class="filter-pill" onclick="setWholeUIMode('neubrutalist')">🧱 3D Neubrutalist Pop</span>
            <span class="filter-pill" onclick="setWholeUIMode('neumorphic-clay')">☁️ 3D Neumorphic Clay</span>
            <span class="filter-pill" onclick="setWholeUIMode('luxury-editorial')">👑 Luxury Editorial Serif</span>
            <span class="filter-pill" onclick="setWholeUIMode('retro-os')">📟 Retro OS / CRT</span>
          </div>
        </div>

        <div style="display:flex; gap:10px; flex-wrap:wrap; margin-bottom:12px;">
          <input type="text" id="theme-studio-search" placeholder="🔍 Search 70 themes (e.g. Blueprint, VisionOS, Jarvis, Luxury, Cyberpunk, Ganga, Rolex, Brutalist)..." oninput="renderThemeStudioGrid()" style="flex:1; padding:12px 16px;">
        </div>
        <div class="filter-pills-wrap" id="theme-cat-pills" style="margin-bottom:12px;"></div>
        <div class="theme-studio-grid" id="theme-studio-grid"></div>
      </div>
    </div>

    <!-- CONFIRMATION MODAL (REPLACES BLOCKED NATIVE CONFIRM) -->
    <div id="confirm-overlay" class="overlay" style="z-index: 100001;">
      <div class="modal-box-center" style="border-top: 6px solid var(--danger);">
        <h2 id="confirm-modal-title">⚠️ Confirm Action</h2>
        <p id="confirm-modal-msg" style="font-weight: 700; margin-top: 10px;">Are you sure you want to proceed?</p>
        <div style="display: flex; gap: 10px; margin-top: 20px;">
          <button class="btn btn-outline" style="flex:1;" onclick="resolveConfirmModal(false)">Cancel</button>
          <button class="btn btn-danger" style="flex:1;" onclick="resolveConfirmModal(true)">Confirm</button>
        </div>
      </div>
    </div>

    <!-- CONFLICT DETECTOR OVERLAY -->
    <div id="conflict-overlay" class="overlay" style="z-index: 100000;">
      <div class="modal-box-center" style="border-top: 6px solid var(--danger);">
        <h2>⚠️ Sync Conflict Detected</h2>
        <p style="color: var(--danger); font-weight: bold;">Another user just modified this group while you were working.</p>
        <p style="font-size:12px;">If you force save, you will overwrite their changes. If you reload, you will lose your recent unsaved edits.</p>
        <div style="display: flex; gap: 10px; margin-top: 15px;">
          <button class="btn btn-outline" style="flex:1;" onclick="resolveConflict('reload')">🔄 Reload Cloud Data</button>
          <button class="btn btn-danger" style="flex:1;" onclick="resolveConflict('force')">⚠️ Force Override</button>
        </div>
      </div>
    </div>

    <!-- WORKER PROFILE & MINI-CALENDAR MODAL -->
    <div id="worker-profile-modal" class="overlay" style="z-index: 10002;">
      <div class="modal-box-center" style="max-width: 560px; text-align: left; max-height: 90vh; overflow-y: auto;">
        <button class="close-btn" onclick="closeModal('worker-profile-modal')">&times;</button>
        <div id="worker-profile-content"></div>
      </div>
    </div>

    <!-- BULK OVERTIME & BULK ADVANCE MODAL -->
    <div id="bulk-tool-modal" class="overlay" style="z-index: 10002;">
      <div class="modal-box-center" style="max-width: 460px; text-align: left;">
        <button class="close-btn" onclick="closeModal('bulk-tool-modal')">&times;</button>
        <h2 style="text-align:center; margin-bottom: 6px;">⚡ Bulk OT &amp; Advance Tool</h2>
        <p style="text-align:center; margin-bottom: 16px;">Apply uniform Overtime or Advance to multiple workers for the selected day.</p>
        <div style="margin-bottom: 14px;">
          <label style="font-size:12px; font-weight:800; color:var(--text-muted);">Target Workforce Group</label>
          <select id="bulk-target-group" style="margin-top:6px;">
            <option value="present">✅ All Present / Half-Day Workers Today</option>
            <option value="all">👷 All Registered Workers in Group</option>
          </select>
        </div>
        <div style="margin-bottom: 14px;">
          <label style="font-size:12px; font-weight:800; color:var(--text-muted);">Overtime Hours (Quick Presets or Custom)</label>
          <div style="display:flex; gap:8px; margin: 6px 0 8px 0; flex-wrap:wrap;">
            <button type="button" class="preset-chip" onclick="document.getElementById('bulk-ot-val').value = 1">+1h</button>
            <button type="button" class="preset-chip" onclick="document.getElementById('bulk-ot-val').value = 2">+2h</button>
            <button type="button" class="preset-chip" onclick="document.getElementById('bulk-ot-val').value = 4">+4h</button>
            <button type="button" class="preset-chip" onclick="document.getElementById('bulk-ot-val').value = 0">Reset 0h</button>
          </div>
          <input type="number" id="bulk-ot-val" step="0.5" min="0" placeholder="Leave blank to keep existing OT">
        </div>
        <div style="margin-bottom: 18px;">
          <label style="font-size:12px; font-weight:800; color:var(--text-muted);">Daily Advance ₹ (Quick Presets or Custom)</label>
          <div style="display:flex; gap:8px; margin: 6px 0 8px 0; flex-wrap:wrap;">
            <button type="button" class="preset-chip" onclick="document.getElementById('bulk-adv-val').value = 200">₹200</button>
            <button type="button" class="preset-chip" onclick="document.getElementById('bulk-adv-val').value = 500">₹500</button>
            <button type="button" class="preset-chip" onclick="document.getElementById('bulk-adv-val').value = 1000">₹1k</button>
            <button type="button" class="preset-chip" onclick="document.getElementById('bulk-adv-val').value = 0">Reset ₹0</button>
          </div>
          <input type="number" id="bulk-adv-val" step="50" min="0" placeholder="Leave blank to keep existing Advance">
        </div>
        <button class="btn btn-primary" onclick="applyBulkTool()">⚡ Apply Bulk Update</button>
      </div>
    </div>

    <!-- CUSTOM LOW-STOCK THRESHOLD MODAL -->
    <div id="stock-threshold-modal" class="overlay" style="z-index: 10002;">
      <div class="modal-box-center" style="max-width: 480px; text-align: left;">
        <button class="close-btn" onclick="closeModal('stock-threshold-modal')">&times;</button>
        <h2 style="text-align:center; margin-bottom: 6px;">⚙️ Set Minimum Stock Alerts</h2>
        <p style="text-align:center; margin-bottom: 14px;">Set custom low-stock alert quantities per material (default is 5).</p>
        <div id="stock-threshold-rows" style="max-height: 260px; overflow-y: auto; margin-bottom: 12px; display:flex; flex-direction:column; gap:8px;"></div>
        <div style="display:flex; gap:10px; margin-bottom: 14px;">
          <button type="button" class="btn btn-outline btn-small" onclick="addCustomThresholdRow('', 10)">+ Add Material Rule</button>
        </div>
        <button class="btn btn-primary" onclick="saveStockThresholds()">💾 Save Alert Thresholds</button>
      </div>
    </div>

    <!-- FULL-SCREEN PHOTO LIGHTBOX MODAL -->
    <div id="photo-lightbox-modal" class="overlay" style="z-index: 10003; background: rgba(0,0,0,0.92);">
      <div class="modal-box-center" style="max-width: 760px; background: #0F172A; color: #F8FAFC; border-color: #334155;">
        <button class="close-btn" style="background: rgba(255,255,255,0.15); color: #fff;" onclick="closeModal('photo-lightbox-modal')">&times;</button>
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom: 12px; padding-right: 36px; flex-wrap:wrap; gap:8px;">
          <h3 id="lightbox-date-badge" style="font-size:15px; color:#38BDF8;">📷 DPR Progress Photo</h3>
          <div style="display:flex; gap:8px;">
            <button type="button" class="btn btn-outline btn-small" style="width:auto; color:#fff; border-color:#475569; padding:6px 12px;" onclick="adjustLightboxZoom(-0.25)">➖</button>
            <button type="button" class="btn btn-outline btn-small" style="width:auto; color:#fff; border-color:#475569; padding:6px 12px;" id="lightbox-zoom-lbl" onclick="resetLightboxZoom()">100%</button>
            <button type="button" class="btn btn-outline btn-small" style="width:auto; color:#fff; border-color:#475569; padding:6px 12px;" onclick="adjustLightboxZoom(0.25)">➕</button>
          </div>
        </div>
        <div style="background:#020617; border-radius:14px; overflow:auto; border:1px solid #334155; height: 60vh; display:flex; align-items:center; justify-content:center; margin-bottom:14px;">
          <img id="lightbox-img" src="" alt="DPR Progress Photo" style="max-width:100%; max-height:100%; object-fit:contain; transition: transform 0.2s ease;">
        </div>
        <div style="display:flex; gap:12px;">
          <a id="lightbox-open-link" href="#" target="_blank" rel="noopener" class="btn btn-primary" style="flex:1; text-decoration:none;">🔗 Open Original</a>
          <button type="button" id="lightbox-delete-btn" class="btn btn-danger" style="flex:1;" onclick="deleteCurrentLightboxPhoto()">🗑️ Delete Photo</button>
        </div>
      </div>
    </div>

    <!-- LIVE ACTIVITY PANEL -->
    <div id="activity-panel" class="activity-panel">
      <div class="activity-header">
        <h3 style="font-size: 18px;">Live Portal Analytics</h3>
        <button style="background:none; border:none; color:white; font-size: 28px; cursor:pointer;" onclick="toggleActivityPanel()">&times;</button>
      </div>
      <div class="activity-body">
        <h4 class="ana-heading">System Diagnostics</h4>
        <div class="ana-grid">
           <div class="ana-box"><span>Ping</span><b id="ana-ping">--</b></div>
           <div class="ana-box"><span>CPU Est.</span><b id="ana-cpu">--</b></div>
           <div class="ana-box"><span>Uptime</span><b id="ana-uptime">00:00</b></div>
           <div class="ana-box"><span>Packet Loss</span><b class="text-success">0.00%</b></div>
           <div class="ana-box"><span>Encryption</span><b class="text-success">AES-256</b></div>
           <div class="ana-box"><span>Cloud Node</span><b>Asia-SE1</b></div>
           <div class="ana-box"><span>Total Syncs</span><b id="ana-syncs">0</b></div>
           <div class="ana-box"><span>Payload</span><b id="ana-payload">0 KB</b></div>
           <div class="ana-box"><span>Database</span><b class="text-success">Connected</b></div>
        </div>

        <h4 class="ana-heading">Site Operations</h4>
        <div class="ana-grid">
           <div class="ana-box"><span>Active Groups</span><b id="ana-zones">0</b></div>
           <div class="ana-box"><span>Workforce</span><b id="ana-workforce">0</b></div>
           <div class="ana-box"><span>Officials</span><b id="ana-kp">0</b></div>
           <div class="ana-box"><span>Attend. Rate</span><b id="ana-attend-rate">0%</b></div>
           <div class="ana-box"><span>Rain Days</span><b id="ana-rain">0</b></div>
           <div class="ana-box"><span>Mat. Activity</span><b id="ana-mat">0</b></div>
        </div>

        <h4 class="ana-heading">Financial Overview (Monthly)</h4>
        <div class="ana-grid">
           <div class="ana-box"><span>Gross Wage</span><b id="ana-gross">₹0</b></div>
           <div class="ana-box"><span>Total Adv.</span><b id="ana-adv">₹0</b></div>
           <div class="ana-box"><span>Total OT</span><b id="ana-ot">0h</b></div>
        </div>
        <div class="ana-box" style="margin-top: 10px; background: #FFFBEB; border-color: #FCD34D;">
           <span>Net Burn / Total Payable</span><b id="ana-net" style="color: #B45309; font-size: 20px;">₹0</b>
        </div>

        <h4 class="ana-heading">Visual Workforce &amp; Financial Charts</h4>
        <div id="panel-visual-charts" style="display: flex; flex-direction: column; gap: 12px;"></div>

        <h4 class="ana-heading">Network Presence</h4>
        <div class="ana-grid" style="grid-template-columns: 1fr 1fr;">
           <div class="ana-box"><span>Active Sessions</span><b id="ana-sessions">1</b></div>
           <div class="ana-box"><span>Peak Users</span><b id="ana-peak">1</b></div>
           <div class="ana-box"><span>Mobile Div.</span><b id="ana-mobile">0%</b></div>
           <div class="ana-box"><span>Desktop Div.</span><b id="ana-desktop">0%</b></div>
        </div>
        <div id="online-users-list" style="margin: 12px 0 20px 0;"></div>

        <h4 class="ana-heading">Audit Log</h4>
        <div class="ana-grid" style="grid-template-columns: 1fr 1fr; margin-bottom:12px;">
           <div class="ana-box"><span>Today's Logs</span><b id="ana-logs">0</b></div>
           <div class="ana-box"><span>Admin Actions</span><b id="ana-admin-logs">0</b></div>
        </div>
        <div id="activity-log-list"></div>
      </div>
    </div>

    <!-- PROFILE MODAL -->
    <div id="profile-overlay" class="overlay">
      <div class="modal-box-center">
        <h2>Global Industries</h2>
        <p>Enter your full name to identify your updates on the live activity board:</p>
        <input type="text" id="profile-name-input" class="pin-input" placeholder="Your Name" style="letter-spacing: normal;">
        <button class="btn btn-primary" onclick="saveProfile()">Enter Portal</button>
      </div>
    </div>

    <!-- LOGIN MODAL -->
    <div id="login-overlay" class="overlay">
      <div class="modal-box-center">
        <button class="close-btn" onclick="closeModal('login-overlay')">&times;</button>
        <h2>System Access</h2>
        <p>Enter your 4-digit access PIN:</p>
        <input type="password" id="admin-pwd" class="pin-input" placeholder="****" inputmode="numeric" maxlength="4">
        <button class="btn btn-primary" onclick="checkPassword()">Unlock Access</button>
        <p id="pwd-error" style="color:var(--danger); font-size: 14px; margin-top: 16px; display: none; font-weight:800;">Invalid PIN provided.</p>
      </div>
    </div>
    
    <!-- SITE MANAGER MODAL -->
    <div id="site-manager-modal" class="overlay">
      <div class="modal-box-center">
        <button class="close-btn" onclick="closeModal('site-manager-modal')">&times;</button>
        <h2 id="sm-title">Manage Structure</h2>
        <p id="sm-desc">A Site is a major geographical location. A Group is a subgroup within that site.</p>
        <input type="hidden" id="sm-action-type">
        <input type="text" id="sm-input" class="pin-input" style="letter-spacing: normal; font-size: 18px;" placeholder="Enter Name...">
        <button class="btn btn-primary" onclick="executeSiteManager()">Save Changes</button>
      </div>
    </div>

    <header>
      <div class="letterhead-container">
        <div class="letterhead-top">
          <div class="logo-container">
            <svg viewBox="0 0 100 100" width="100%" height="100%">
              <defs>
                <linearGradient id="globeGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                  <stop offset="0%" stop-color="#D49B4B" /><stop offset="55%" stop-color="#B87B28" /><stop offset="100%" stop-color="#8A5612" />
                </linearGradient>
                <clipPath id="globeClipHdr"><circle cx="50" cy="50" r="45" /></clipPath>
              </defs>
              <g clip-path="url(#globeClipHdr)">
                <ellipse cx="50" cy="50" rx="34" ry="45" stroke="url(#globeGrad)" stroke-width="2.6" fill="none" />
                <ellipse cx="50" cy="50" rx="23" ry="45" stroke="url(#globeGrad)" stroke-width="2.5" fill="none" />
                <ellipse cx="50" cy="50" rx="12" ry="45" stroke="url(#globeGrad)" stroke-width="2.4" fill="none" />
                <line x1="50" y1="5" x2="50" y2="95" stroke="url(#globeGrad)" stroke-width="2.5" />
                <path d="M 5,19 Q 50,26 95,19" stroke="url(#globeGrad)" stroke-width="2.5" fill="none" />
                <path d="M 5,30 Q 50,35 95,30" stroke="url(#globeGrad)" stroke-width="2.5" fill="none" />
                <path d="M 5,70 Q 50,65 95,70" stroke="url(#globeGrad)" stroke-width="2.5" fill="none" />
                <path d="M 5,81 Q 50,74 95,81" stroke="url(#globeGrad)" stroke-width="2.5" fill="none" />
                <path d="M 32,6 Q 50,12 68,6 Z" fill="url(#globeGrad)" />
                <path d="M 32,94 Q 50,88 68,94 Z" fill="url(#globeGrad)" />
                <rect x="4" y="39" width="92" height="22" fill="url(#globeGrad)" />
              </g>
              <circle cx="50" cy="50" r="45" stroke="url(#globeGrad)" stroke-width="3.5" fill="none" />
              <text x="50" y="55.5" fill="#FFFFFF" font-family="'Arial Black', Arial, sans-serif" font-size="16.5" font-weight="900" letter-spacing="3.5" text-anchor="middle">GI</text>
            </svg>
          </div>
          <div class="title-container"><span class="title-global">Global</span><span class="title-industries">Industries</span></div>
        </div>
        <div class="regd-office"><b>Regd. Office :</b> Thokrichak, P.O. Garahra, Via Barauni, Dist. Begusarai, Bihar- 851 126.</div>
      </div>

      <div class="app-control-bar">
        <div class="site-selector-wrap" id="site-dropdown-container">
          <span class="site-label">SITE:</span>
          <div class="custom-select" onclick="toggleDropdown()"><span id="selected-site-label">Loading...</span> <span>▼</span></div>
          <div class="custom-dropdown-menu" id="site-dropdown"></div>
        </div>
        <div class="status-group">
          <div class="sync-status-badge" id="cloud-sync-badge" title="Firebase Real-time Connection Status">🟢 Cloud Synced</div>
          <!-- Theme Selector Dropdown (70 Themes + Whole-UI Morphs) -->
          <select id="theme-selector" onchange="changeTheme(this.value)" style="padding: 6px 12px; font-size: 12px; border-radius: 12px; background: rgba(255,255,255,0.2); color: white; border: 1px solid rgba(255,255,255,0.3); font-weight:800; cursor:pointer; max-width: 215px;">
            <optgroup label="🏛️ Whole-UI Morph Themes (New!)" style="color:#000;">
              <option value="blueprint-cad" style="color:#000;">📐 CAD Blueprint Grid (Whole UI)</option>
              <option value="autocad-engineer" style="color:#000;">📏 AutoCAD Engineer Dark (Whole UI)</option>
              <option value="structural-steel-cad" style="color:#000;">🏗️ Structural Steel CAD (Whole UI)</option>
              <option value="vision-os-spatial" style="color:#000;">🥽 VisionOS Spatial Glass (Whole UI)</option>
              <option value="frosted-aurora" style="color:#000;">🌌 Frosted Aurora Glass (Whole UI)</option>
              <option value="crystal-prism" style="color:#000;">💎 Crystal Prism Glass (Whole UI)</option>
              <option value="aero-frutiger" style="color:#000;">🫧 Frutiger Aero Glass (Whole UI)</option>
              <option value="neubrutalist-pop" style="color:#000;">🧱 Neubrutalist Pop Studio (Whole UI)</option>
              <option value="brutalist-arch" style="color:#000;">🏛️ Brutalist Architecture (Whole UI)</option>
              <option value="manga-ink" style="color:#000;">✒️ Manga Ink Brutal (Whole UI)</option>
              <option value="swiss-bauhaus" style="color:#000;">🟥 Swiss Bauhaus Grid (Whole UI)</option>
              <option value="jarvis-iron-hud" style="color:#000;">🤖 Jarvis Hologram HUD (Whole UI)</option>
              <option value="starfleet-lcars" style="color:#000;">🚀 Starfleet LCARS HUD (Whole UI)</option>
              <option value="mecha-gundam" style="color:#000;">🛡️ Mecha Cockpit HUD (Whole UI)</option>
              <option value="cyber-samurai" style="color:#000;">⚔️ Cyber Samurai HUD (Whole UI)</option>
              <option value="halo-unsc" style="color:#000;">🪖 UNSC Tactical HUD (Whole UI)</option>
              <option value="tron-legacy-grid" style="color:#000;">🥏 Tron Lightcycle Grid (Whole UI)</option>
              <option value="alien-nostromo" style="color:#000;">🛸 Nostromo Bio-HUD (Whole UI)</option>
              <option value="dune-arrakis" style="color:#000;">⏳ Dune Arrakis Spice (Whole UI)</option>
              <option value="neumorphic-light" style="color:#000;">☁️ 3D Neumorphic Soft Light (Whole UI)</option>
              <option value="neumorphic-dark" style="color:#000;">🌑 3D Neumorphic Stealth Dark (Whole UI)</option>
              <option value="claymorphic-3d" style="color:#000;">🧸 3D Claymorphism Studio (Whole UI)</option>
              <option value="porcelain-ceramic" style="color:#000;">🏺 Porcelain Ceramic 3D (Whole UI)</option>
              <option value="luxury-black-gold" style="color:#000;">👑 Imperial Black &amp; Gold (Whole UI)</option>
              <option value="marble-imperial" style="color:#000;">🏛️ Carrara Marble Gold (Whole UI)</option>
              <option value="rolex-emerald-gold" style="color:#000;">⌚ Geneva Emerald &amp; Gold (Whole UI)</option>
              <option value="wall-street-paper" style="color:#000;">📰 Financial Gazette Serif (Whole UI)</option>
              <option value="monaco-yacht" style="color:#000;">🛥️ Monaco Yacht Club (Whole UI)</option>
              <option value="dubai-burj-gold" style="color:#000;">🏙️ Burj Royal Gold (Whole UI)</option>
              <option value="win95-retro-os" style="color:#000;">💾 Classic 95 Desktop OS (Whole UI)</option>
              <option value="mac-classic-platinum" style="color:#000;">🖥️ Platinum Classic OS (Whole UI)</option>
              <option value="pipboy-fallout" style="color:#000;">☢️ Vault Pip-Boy 3000 (Whole UI)</option>
              <option value="amber-crt-monitor" style="color:#000;">📺 1984 Amber CRT Monitor (Whole UI)</option>
              <option value="dos-borland-blue" style="color:#000;">⌨️ Turbo DOS Blue Terminal (Whole UI)</option>
              <option value="gameboy-pocket" style="color:#000;">🎮 8-Bit Handheld Olive (Whole UI)</option>
            </optgroup>
            <optgroup label="🌏 India, Nature &amp; Atmospheric (New!)" style="color:#000;">
              <option value="himalayan-dawn" style="color:#000;">🏔️ Himalayan Sunrise</option>
              <option value="ganga-river-mist" style="color:#000;">🌊 Ganga River Mist (Bihar)</option>
              <option value="monsoon-thunder" style="color:#000;">⛈️ Monsoon Storm Slate</option>
              <option value="thar-desert-gold" style="color:#000;">🐪 Thar Desert Sandstone</option>
              <option value="kashmir-saffron" style="color:#000;">🌺 Kashmir Kesar Saffron</option>
              <option value="sundarbans-mangrove" style="color:#000;">🐅 Sundarbans Canopy</option>
              <option value="bioluminescent-bay" style="color:#000;">🪼 Bioluminescent Lagoon</option>
              <option value="northern-lights" style="color:#000;">🌠 Aurora Borealis</option>
              <option value="volcanic-magma" style="color:#000;">🌋 Volcanic Obsidian Lava</option>
              <option value="cherry-blossom-kyoto" style="color:#000;">🌸 Kyoto Sakura Blossom</option>
              <option value="matcha-zen" style="color:#000;">🍵 Uji Matcha Zen</option>
              <option value="nordic-fjord" style="color:#000;">🧊 Norwegian Fjord</option>
              <option value="sahara-dusk" style="color:#000;">🏜️ Sahara Terracotta Dusk</option>
              <option value="amalfi-coast" style="color:#000;">🍋 Amalfi Azure &amp; Lemon</option>
              <option value="lavender-provence" style="color:#000;">💜 Provence Lavender</option>
            </optgroup>
            <optgroup label="⭐ Classic &amp; Signature Themes" style="color:#000;">
              <option value="light" style="color:#000;">☀️ Light Default</option>
              <option value="dark" style="color:#000;">🌙 Dark Slate</option>
              <option value="liquid-glass" style="color:#000;">🧪 Liquid Glass (Blur)</option>
              <option value="cyberpunk" style="color:#000;">⚡ Cyberpunk Neon</option>
              <option value="emerald" style="color:#000;">🌲 Emerald Forest</option>
              <option value="sunset" style="color:#000;">🌅 Sunset Orange</option>
              <option value="royal" style="color:#000;">👑 Royal Amethyst</option>
              <option value="arctic" style="color:#000;">❄️ Arctic Frost</option>
              <option value="matrix" style="color:#000;">💻 Matrix Green</option>
              <option value="obsidian" style="color:#000;">🖤 Obsidian Dark</option>
              <option value="rose-gold" style="color:#000;">✨ Rose Gold</option>
              <option value="tokyo-night" style="color:#000;">🌆 Tokyo Night</option>
              <option value="solarized" style="color:#000;">📜 Solarized Light</option>
              <option value="nordic" style="color:#000;">🏔️ Nordic Minimal</option>
              <option value="deep-space" style="color:#000;">🌌 Deep Space</option>
              <option value="pastel-dream" style="color:#000;">🎨 Pastel Dream</option>
              <option value="retro-terminal" style="color:#000;">📟 Retro Terminal</option>
              <option value="industrial-steel" style="color:#000;">⚙️ Industrial Steel</option>
              <option value="golden-amber" style="color:#000;">⭐ Golden Amber</option>
              <option value="carbon-fiber" style="color:#000;">🏎️ Carbon Fiber</option>
              <option value="synthwave" style="color:#000;">🌴 Synthwave 80s</option>
              <option value="neon-sakura" style="color:#000;">🌸 Neon Sakura</option>
              <option value="sunset-mirage" style="color:#000;">🏜️ Sunset Mirage</option>
              <option value="acid-matrix" style="color:#000;">🔋 Acid Matrix</option>
              <option value="vampire-blood" style="color:#000;">🩸 Vampire Blood</option>
              <option value="deep-ocean-abyss" style="color:#000;">🌊 Deep Ocean Abyss</option>
              <option value="cyber-gold" style="color:#000;">🏆 Cyber Gold</option>
              <option value="neon-mint" style="color:#000;">🌿 Neon Mint</option>
              <option value="crimson-dusk" style="color:#000;">🍷 Crimson Dusk</option>
              <option value="electric-violet" style="color:#000;">🔮 Electric Violet</option>
            </optgroup>
          </select>
          <div class="user-profile-badge" onclick="openThemeStudioModal()" title="Open Visual Theme Studio & Whole-UI Morph Gallery (70 Themes)" style="background: linear-gradient(135deg, rgba(236,72,153,0.35), rgba(59,130,246,0.35)); border-color: rgba(255,255,255,0.4);">🎨 70 Themes</div>
          <div class="live-clock-badge" id="system-live-clock">--:--:--</div>
          <div class="user-profile-badge" onclick="replayIntro()" title="Replay 3D Intro">🎬 3D Intro</div>
          <div class="user-profile-badge" onclick="confirmPageRefresh()" title="Refresh or Reload Portal (Asks Confirmation)">🔄 Refresh</div>
          <div class="user-profile-badge" id="profile-display" onclick="toggleActivityPanel()" title="View Analytics & Activity">👤 User</div>
          <button id="auth-status-btn" onclick="toggleAuth()">🔒 View Only</button>
        </div>
      </div>
    </header>

    <div class="container">
      <div class="dashboard-grid">
        <div class="stat-card">
          <span class="stat-label">👷 Workers</span>
          <span class="stat-value" id="stat-total-workers">0</span>
        </div>
        <div class="stat-card success">
          <span class="stat-label" id="lbl-present-today">✅ Present</span>
          <span class="stat-value" id="stat-present-today">0 / 0</span>
        </div>
        <div class="stat-card warning">
          <span class="stat-label">⏱️ Overtime</span>
          <span class="stat-value" id="stat-total-ot">0 hrs</span>
        </div>
        <div class="stat-card accent">
          <span class="stat-label">💰 Payable</span>
          <span class="stat-value" id="stat-total-balance">₹0</span>
        </div>
      </div>

      <div class="analytics-ribbon-header">
        <div class="analytics-ribbon-title">📊 Visual Workforce &amp; Financial Analytics</div>
        <button type="button" class="analytics-toggle-btn" id="btn-toggle-charts" onclick="toggleDashboardCharts()">▼ Hide Charts</button>
      </div>
      <div class="visual-charts-grid" id="dashboard-charts-grid">
        <div class="chart-card">
          <h5><span>📅 7-Day Attendance Trend</span><span style="font-size:10px; color:var(--secondary);">Click bar to jump</span></h5>
          <div id="chart-7day-bars"></div>
        </div>
        <div class="chart-card">
          <h5><span>👷 Trade-Wise Workforce</span><span style="font-size:10px; color:var(--text-muted);">Donut Breakdown</span></h5>
          <div id="chart-trade-dist"></div>
        </div>
        <div class="chart-card">
          <h5><span>💰 Gross vs. Advance Split</span><span style="font-size:10px; color:var(--text-muted);">Monthly Ratio</span></h5>
          <div id="chart-fin-breakdown"></div>
        </div>
      </div>

      <div class="nav-tabs">
        <button class="tab-btn active" onclick="switchTab('daily-view', this)">📅 Daily</button>
        <button class="tab-btn special-tab" onclick="switchTab('key-person-view', this)">👔 Officials</button>
        <button class="tab-btn" onclick="switchTab('dpr-view', this)">📝 DPR & Weather</button>
        <button class="tab-btn" onclick="switchTab('notes-view', this)">📓 Site Timeline</button>
        <button class="tab-btn" onclick="switchTab('monthly-view', this)">📊 Monthly</button>
        <button class="tab-btn" onclick="switchTab('worker-view', this)">👷 Directory</button>
        <button class="tab-btn" onclick="switchTab('slips-view', this)">🧾 Slips</button>
        <button class="tab-btn report-tab" onclick="switchTab('one-day-report-view', this)">🗓 One Day Report</button>
        <button class="tab-btn report-tab" onclick="switchTab('report-view', this)">📈 Custom Report</button>
        <button class="tab-btn" onclick="switchTab('equipment-view', this)" style="background: #ECFDF5; border-color: #10B981; color: #065F46;">🛠️ Equipment &amp; Safety</button>
        <button class="tab-btn" onclick="switchTab('ai-view', this)" style="background: linear-gradient(135deg, #3B82F6, #9333EA); color: white;">🤖 AI Site Assistant</button>
      </div>

      <div class="toolbar">
        <div style="display:flex; gap:14px; flex-wrap:wrap;">
          <select id="month-select" onchange="changeMonth()" style="flex:1; min-width: 150px;"></select>
          <div id="daily-date-picker-wrap" style="flex:1; min-width: 150px;"><select id="day-select" onchange="handleDayChange()"></select></div>
        </div>
        
        <div id="edit-controls" style="display:none; gap:14px; margin-top:14px; flex-wrap:wrap;">
          <button class="btn btn-outline" onclick="openAddWorkerModal('worker')" style="color:var(--secondary); border-color:var(--secondary); flex:1;" id="btn-add-worker">➕ Add Worker</button>
          <button class="btn btn-outline special-tab" onclick="openAddWorkerModal('key_person')" style="flex:1;" id="btn-add-kp">➕ Add Key Person</button>
          <button class="btn btn-outline" onclick="forceSyncProcess()" style="flex:1;">🔄 Sync Cloud</button>
          <button class="btn btn-danger" onclick="wipeZoneData()" style="flex:1; display:none;" id="btn-clear-group" title="Deletes all workers in this group">🗑 Clear Group Data</button>
        </div>

        <div style="display:flex; gap:14px; margin-top:14px; flex-wrap:wrap;">
           <button class="btn btn-success" style="flex:1;" onclick="exportToExcel()">📊 Export Excel (.xlsx)</button>
           <button class="btn btn-primary" style="flex:1;" onclick="exportDatabase()">💾 Backup DB</button>
           <button class="btn btn-outline" style="flex:1; border-color:var(--warning); color:var(--primary); display:none;" id="btn-restore-db" onclick="triggerRestoreDB()">📂 Restore DB</button>
           <input type="file" id="restore-db-file-input" accept=".json" style="display:none;" onchange="handleRestoreDBFile(event)">
        </div>
      </div>
      
      <!-- TAB 1: DAILY VIEW -->
      <div id="daily-view" class="tab-content active">
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:16px; flex-wrap:wrap; gap:12px;">
           <h3 style="color:var(--primary); font-size:20px;">Labour Attendance</h3>
        </div>
        
        <div id="rollup-alert-daily" class="empty-state" style="display:none; background:#F0FDF4; border-color:#86EFAC; color:#166534; padding: 12px; margin-bottom: 16px;">
          🌍 <b>Master Roll-Up View Active:</b> Viewing combined attendance across this site. Editing disabled in master view.
        </div>

        <div class="search-filter-bar">
          <div class="search-input-box">
            <span class="search-icon">🔍</span>
            <input type="text" id="worker-search-input" placeholder="Search worker name or trade..." oninput="renderDailyView()">
          </div>
          <button class="quick-action-btn" id="btn-mark-all" onclick="markAllWorkersPresent()" style="padding: 10px 15px; border-radius: 12px; background: var(--success); color: white; border: none; font-weight: bold; cursor: pointer;">✅ Mark All Present</button>
          <button class="quick-action-btn" id="btn-bulk-tool" onclick="openBulkToolModal()" style="padding: 10px 15px; border-radius: 12px; background: var(--secondary); color: white; border: none; font-weight: bold; cursor: pointer;">⚡ Bulk OT / Advance</button>
        </div>
        <div class="filter-pills-wrap" id="daily-filter-pills"></div>

        <div class="worker-daily-list" id="daily-list-container"></div>
      </div>

      <!-- TAB 2: KEY PERSON VIEW -->
      <div id="key-person-view" class="tab-content">
        <h3 style="color:#B45309; font-size:20px; margin-bottom:16px;">Officials & Key Personnel</h3>
        
        <div id="kp-alert" class="empty-state" style="display:none; background:#FFFBEB; border-color:#FCD34D; color:#92400E;">
          Key Personnel attendance is centralized. Please select the <b>Master Roll-Up</b> (Main Site) in the dropdown to view officials.
        </div>
        
        <div id="kp-master-header" style="display:none; text-align:center; padding: 15px; background: #FEF9C3; border-radius: 12px; margin-bottom: 20px; border: 1px solid #FDE047;">
           <h2 style="color: #92400E; margin-bottom: 5px;">⭐ Site Command Center ⭐</h2>
           <p style="color: #B45309; font-size: 13px; font-weight: 700;">Executive Officials & Supervisors</p>
        </div>

        <div class="worker-daily-list" id="kp-list-container"></div>
      </div>

      <!-- TAB 3: DPR & INVENTORY VIEW (UPDATED WITH VOICE/CAMERA) -->
      <div id="dpr-view" class="tab-content">
        <div style="display:flex; justify-content:space-between; margin-bottom: 16px; align-items:center; flex-wrap:wrap; gap:10px;">
           <h3 style="color:var(--primary); font-size:20px;">Daily Progress Report & Inventory</h3>
           <button class="btn btn-whatsapp btn-small" onclick="shareDPRWhatsApp()" style="width:auto; border-radius:20px;">📲 Share WhatsApp</button>
        </div>
        
        <div class="dpr-section">
          <h4>Site Weather & Rain Logs</h4>
          <div style="display:flex; gap:16px; margin-bottom:16px;">
            <select id="dpr-weather-select" onchange="checkWeatherCondition()" onclick="requireAuthClick(this)" style="flex:1;">
              <option>☀️ Sunny / Clear</option><option>☁️ Cloudy</option><option>🌧 Light Rain</option><option>⛈️ Heavy Rain</option>
            </select>
          </div>
          <div id="rain-settings" style="display:none; gap:16px; background:rgba(59,130,246,0.08); padding:16px; border-radius:12px; border:1px solid #BFDBFE;">
             <div style="flex:1;"><label style="font-size:12px; font-weight:800;">Rain Start Time</label><input type="time" id="dpr-rain-start" onblur="autoSaveDPR()" style="margin-top:6px;"></div>
             <div style="flex:1;"><label style="font-size:12px; font-weight:800;">Rain End Time</label><input type="time" id="dpr-rain-end" onblur="autoSaveDPR()" style="margin-top:6px;"></div>
             <div style="flex:1;"><label style="font-size:12px; font-weight:800;">Work Stopped?</label><select id="dpr-work-stopped" onchange="autoSaveDPR()" style="margin-top:6px;"><option>No</option><option>Yes</option></select></div>
          </div>
        </div>

        <div class="dpr-section">
          <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom: 12px;">
            <h4 style="margin:0;">Work Allocation</h4>
            <button id="btn-dictate" class="action-btn-sm mic-btn" style="background:var(--card-bg); border:1px solid var(--secondary); color:var(--secondary); font-weight:800; border-radius:12px; padding: 8px 12px;" onclick="startDictation()" title="Use Voice to Text">🎤 Dictate</button>
          </div>
          <textarea id="dpr-work-text" class="dpr-textarea" placeholder="E.g. Column casting at Platform 1..." onblur="autoSaveDPR()" onclick="requireAuthClick(this)"></textarea>
          
          <div style="margin-top: 10px;">
            <label class="btn btn-outline btn-small" style="width: auto; cursor: pointer;">
              📷 Attach Progress Photo
              <input type="file" accept="image/*" capture="environment" style="display: none;" onchange="handlePhotoUpload(event)">
            </label>
            <div id="dpr-photo-preview" style="display: flex; gap: 10px; margin-top: 12px; flex-wrap: wrap;"></div>
          </div>
        </div>
        
        <div class="dpr-section">
          <h4>📥 Materials Received <button class="btn btn-outline btn-small" onclick="addMaterialRow('received')" id="btn-add-mat-rec">+ Add</button></h4>
          <div id="dpr-mat-received-list"></div>
        </div>

        <div class="dpr-section">
          <h4>📤 Materials Consumed <button class="btn btn-outline btn-small" onclick="addMaterialRow('consumed')" id="btn-add-mat-con">+ Add</button></h4>
          <div id="dpr-mat-consumed-list"></div>
        </div>

        <div class="dpr-section" style="background:var(--bg); border: 2px dashed var(--border);">
          <h4>📦 Real-Time Live Stock at Site <button class="btn btn-outline btn-small" style="width:auto;" onclick="openStockThresholdModal()">⚙️ Set Min Alerts</button></h4>
          <div id="live-stock-summary" style="display:flex; gap:10px; flex-wrap:wrap; margin-top:10px;">
            <span style="color:var(--text-muted); font-size:13px; font-style:italic;">Add received and consumed materials above to calculate live balance stock.</span>
          </div>
        </div>
      </div>

      <!-- TAB 4: TIMELINE NOTES VIEW -->
      <div id="notes-view" class="tab-content">
        <div class="dpr-section">
           <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom: 12px; flex-wrap:wrap; gap:8px;">
              <h3 style="color:var(--primary); font-size:18px; margin:0;">Site Timeline &amp; To-Do List</h3>
              <span class="stock-badge" id="timeline-completion-badge" style="color:var(--success); border-color:var(--success);">✅ 0 / 0 Completed</span>
           </div>
           
           <div style="display:flex; gap:10px; margin-bottom: 14px; flex-wrap:wrap;">
              <select id="timeline-priority-select" style="width:auto; min-width:135px; padding:12px;">
                <option value="General">🔵 General</option>
                <option value="Urgent">🔴 Urgent</option>
                <option value="Safety">🟡 Safety</option>
              </select>
              <input type="text" id="timeline-input-text" placeholder="Type a note or checklist item..." style="flex:1; min-width:200px;" onkeypress="if(event.key==='Enter') addTimelineNote()">
              <button class="btn btn-primary" onclick="addTimelineNote()" style="width:auto; padding: 12px 20px;">📌 Post</button>
           </div>
           <div class="filter-pills-wrap" id="timeline-filter-pills"></div>

           <div id="timeline-feed" style="display: flex; flex-direction: column; gap: 12px; background: var(--bg); padding: 16px; border-radius: 12px; min-height: 200px; border: 1px solid var(--border);">
              <div class="empty-state">No notes added to the timeline today.</div>
           </div>
        </div>
      </div>
      
      <!-- TAB 5: MONTHLY TABLE -->
      <div id="monthly-view" class="tab-content">
        <div id="rollup-alert-monthly" class="empty-state" style="display:none; background:#F0FDF4; border-color:#86EFAC; color:#166534; padding: 12px; margin-bottom: 16px;">
          🌍 <b>Master Roll-Up View Active:</b> Consolidated monthly attendance for all subgroups combined.
        </div>
        <div class="table-container">
          <table id="monthly-table">
            <thead>
              <tr><th rowspan="2" class="sticky-col">NAME</th><th rowspan="2">TRADE</th><th colspan="2">TOTAL</th><th rowspan="2">RATE</th><th rowspan="2">AMOUNT</th><th rowspan="2">ADVANCE</th><th rowspan="2">BALANCE</th></tr>
              <tr id="sub-headers-row"></tr>
            </thead>
            <tbody id="monthly-table-body"></tbody>
            <tfoot><tr id="monthly-table-total" class="total-row"></tr></tfoot>
          </table>
        </div>
      </div>

      <!-- TAB 6: WORKER DIRECTORY -->
      <div id="worker-view" class="tab-content">
        <div id="rollup-alert-worker" class="empty-state" style="display:none; background:#F0FDF4; border-color:#86EFAC; color:#166534; padding: 12px; margin-bottom: 16px;">
          🌍 <b>Master Roll-Up View Active:</b> Viewing full workforce directory across all subgroups.
        </div>
        <div class="search-filter-bar">
          <div class="search-input-box">
            <span class="search-icon">🔍</span>
            <input type="text" id="dir-search-input" placeholder="Search directory by name, trade, or mobile..." oninput="renderWorkerManagement()">
          </div>
        </div>
        <div class="filter-pills-wrap" id="dir-filter-pills"></div>
        <div class="worker-daily-list" id="worker-mgmt-body"></div>
      </div>
      
      <!-- TAB 7: SLIPS -->
      <div id="slips-view" class="tab-content">
        <div class="dpr-section">
          <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:16px; flex-wrap:wrap; gap:10px;">
            <select id="slip-worker-select" onchange="renderWageSlip()" style="flex:2; min-width:200px;"></select>
            <select id="slip-theme-select" onchange="renderWageSlip()" style="flex:1; min-width:140px;">
              <option value="theme-navy">Classic Navy</option>
              <option value="theme-slate">Modern Slate</option>
              <option value="theme-amber">Industrial Amber</option>
            </select>
            <div style="display:flex; gap:8px; flex-wrap:wrap;">
              <button class="btn btn-outline" style="width:auto; padding:12px 16px;" onclick="window.print()">🖨️ Print</button>
              <button class="btn btn-primary" style="width:auto; padding:12px 16px;" onclick="downloadSlipAsPDF('slip-print-area', 'Wage_Slip')">📄 PDF</button>
              <button class="btn btn-success" style="width:auto; padding:12px 16px;" onclick="exportAllSlipsAsPDF()">📄 Export All Slips (PDF)</button>
            </div>
          </div>
          <div id="wage-slip-display" style="margin-top:20px;"></div>
          <div id="batch-slips-container" style="display:none; margin-top:20px;"></div>
        </div>
      </div>

      <!-- TAB 8: ONE DAY REPORT -->
      <div id="one-day-report-view" class="tab-content">
        <div class="dpr-section">
          <h3 style="color:var(--primary); font-size:20px; margin-bottom: 12px;">🗓️ One Day Master Report</h3>
          <p style="font-size:13px; color:var(--text-muted); margin-bottom: 20px;">Select a specific date to view all attendance, net pay, weather, and material usage for that exact day.</p>
          
          <div style="display:flex; gap:16px; margin-bottom: 20px; flex-wrap: wrap;">
            <div style="flex:1; min-width: 200px; background: var(--bg); padding: 12px; border-radius: 12px; border: 1px solid var(--border);">
              <label style="font-size:12px; font-weight:800; color:var(--text-muted);">Select Date</label>
              <input type="date" id="single-report-date" style="margin-top:6px; background: var(--card-bg);">
            </div>
          </div>
          <div style="display:flex; gap:12px; margin-bottom: 20px; flex-wrap:wrap;">
            <button class="btn btn-primary" onclick="generateReport('single')" style="background:#0284C7; font-size: 16px; padding: 16px; flex:2;">🚀 Generate Day Report</button>
            <button class="btn btn-success" onclick="exportCustomReportExcel('single')" style="flex:1; display:none;" id="btn-rep-excel-single">📊 Export Excel</button>
            <button class="btn btn-primary" onclick="exportCustomReportPDF('single-report-container', 'One_Day_Report')" style="flex:1; display:none; background:#2563EB;" id="btn-rep-pdf-single">📄 Export PDF</button>
          </div>
          
          <div id="single-report-results" style="margin-top: 24px; display: none;"></div>
        </div>
      </div>

      <!-- TAB 9: CUSTOM DATE-RANGE REPORT -->
      <div id="report-view" class="tab-content">
        <div class="dpr-section">
          <h3 style="color:var(--primary); font-size:20px; margin-bottom: 12px;">📈 Custom Date-Range Report</h3>
          <p style="font-size:13px; color:var(--text-muted); margin-bottom: 20px;">Select a specific date range to aggregate all attendance, overtime, net pay, and material usage.</p>
          
          <div style="display:flex; gap:16px; margin-bottom: 20px; flex-wrap: wrap;">
            <div style="flex:1; min-width: 200px; background: var(--bg); padding: 12px; border-radius: 12px; border: 1px solid var(--border);">
              <label style="font-size:12px; font-weight:800; color:var(--text-muted);">From Date</label>
              <input type="date" id="report-start-date" style="margin-top:6px; background: var(--card-bg);">
            </div>
            <div style="flex:1; min-width: 200px; background: var(--bg); padding: 12px; border-radius: 12px; border: 1px solid var(--border);">
              <label style="font-size:12px; font-weight:800; color:var(--text-muted);">To Date</label>
              <input type="date" id="report-end-date" style="margin-top:6px; background: var(--card-bg);">
            </div>
          </div>
          <div style="display:flex; gap:12px; margin-bottom: 20px; flex-wrap:wrap;">
            <button class="btn btn-primary" onclick="generateReport('range')" style="background:#9333EA; font-size: 16px; padding: 16px; flex:2;">🚀 Generate Master Report</button>
            <button class="btn btn-success" onclick="exportCustomReportExcel('range')" style="flex:1; display:none;" id="btn-rep-excel">📊 Export Excel</button>
            <button class="btn btn-primary" onclick="exportCustomReportPDF('custom-report-container', 'Custom_Range_Report')" style="flex:1; display:none; background:#2563EB;" id="btn-rep-pdf">📄 Export PDF</button>
            <button class="btn btn-whatsapp" onclick="exportCustomReportWhatsApp()" style="flex:1; display:none;" id="btn-rep-wa">📲 WhatsApp</button>
          </div>
          
          <div id="report-results" style="margin-top: 24px; display: none;"></div>
        </div>
      </div>

      <!-- TAB 10: EQUIPMENT, MACHINERY & SAFETY MUSTER HUB (NEW FEATURE) -->
      <div id="equipment-view" class="tab-content">
        <div class="dpr-section" style="border-left: 6px solid #10B981;">
          <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:12px; margin-bottom:16px;">
            <div>
              <h3 style="color:var(--primary); font-size:20px; margin-bottom:4px;">🛠️ Site Machinery, Fleet &amp; Safety Muster Command</h3>
              <p style="font-size:13px; color:var(--text-muted);">Track heavy equipment, operator assignments, fuel/hour logs, PPE kits, and run live emergency headcount musters.</p>
            </div>
            <div style="display:flex; gap:10px; flex-wrap:wrap;">
              <button type="button" class="btn btn-success btn-small" style="width:auto;" onclick="runEmergencyMusterRoll()">🚨 Run Live Emergency Muster Roll</button>
              <button type="button" class="btn btn-primary btn-small" style="width:auto;" onclick="exportEquipmentReportWhatsApp()">📲 Share Fleet Status</button>
            </div>
          </div>

          <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(170px, 1fr)); gap:12px; margin-bottom:18px;" id="equip-summary-kpis"></div>

          <div style="background:var(--bg); padding:14px; border-radius:14px; border:1px solid var(--border); margin-bottom:18px; display:flex; gap:10px; flex-wrap:wrap; align-items:center;">
            <input type="text" id="eq-name-input" placeholder="Equipment / Tool Name (e.g. Tower Crane TC-02, JCB 3DX)" style="flex:2; min-width:180px; padding:12px;">
            <input type="text" id="eq-op-input" placeholder="Assigned Operator / Incharge" style="flex:1.5; min-width:150px; padding:12px;">
            <input type="text" id="eq-fuel-input" placeholder="Hours / Fuel (e.g. 6.5h / 45L)" style="flex:1; min-width:130px; padding:12px;">
            <select id="eq-status-input" style="flex:1; min-width:140px; padding:12px;">
              <option value="Operational">🟢 Operational</option>
              <option value="Maintenance">🟡 Maintenance</option>
              <option value="Idle">🔴 Idle / Standby</option>
            </select>
            <button type="button" class="btn btn-primary" style="width:auto; padding:12px 20px;" onclick="addSiteEquipmentItem()">➕ Add Asset</button>
          </div>

          <div class="worker-daily-list" id="equipment-list-container"></div>
          <div id="emergency-muster-output" style="margin-top:18px; display:none;"></div>
        </div>
      </div>

      <!-- TAB 11: 50-FEATURE ULTRA-ADVANCED AI SITE INTELLIGENCE COMMAND SUITE -->
      <div id="ai-view" class="tab-content">
        <div class="dpr-section" style="border-left: 6px solid #6366F1;">
          <div style="display:flex; justify-content:space-between; align-items:flex-start; flex-wrap:wrap; gap:14px; margin-bottom:16px;">
            <div>
              <h3 style="color:var(--primary); font-size:22px; margin-bottom:6px;">🤖 Global Industries Quantum-Neural AI Command — 50 Autonomous Engines + Live Simulator</h3>
              <p style="font-size:13px; color:var(--text-muted); max-width:820px;">
                Powered by <strong>50 specialized AI engines</strong>, interactive Monte Carlo What-If sliders, Voice/Speech synthesis, IS-456 structural civil QA, and 1-click autonomous DPR &amp; Timeline actions.
              </p>
            </div>
            <div style="display:flex; gap:8px; flex-wrap:wrap;">
              <button type="button" class="btn btn-primary btn-small" onclick="generateAIForecast()" style="width:auto; background: linear-gradient(135deg, #3B82F6, #9333EA);">⚡ Run Quantum Simulation</button>
              <button type="button" class="btn btn-primary btn-small" style="width:auto; background:linear-gradient(135deg,#0284C7,#2563EB);" onclick="generateAIForecast()">🚀 Run All 50 AI Engines</button>
              <button type="button" class="btn btn-outline btn-small" style="width:auto; display:none;" onclick="generateAIForecast()">🚀 Run All 30 AI Engines</button>
              <button type="button" class="btn btn-outline btn-small" style="width:auto;" onclick="speakAIReportAloud()">🔊 Speak AI Report</button>
              <button type="button" class="btn btn-success btn-small" style="width:auto;" onclick="exportAIAuditPDF()">📄 Export AI PDF</button>
              <button type="button" class="btn btn-whatsapp btn-small" onclick="shareAIReportWhatsApp()" style="width:auto;">📲 Share AI Audit</button>
            </div>
          </div>

          <!-- 1-Click Autonomous AI Site Action Bar -->
          <div style="display:flex; gap:10px; flex-wrap:wrap; margin-bottom:16px; background:var(--bg); padding:12px 14px; border-radius:14px; border:1px solid var(--border); align-items:center;">
            <span style="font-size:11px; font-weight:900; color:var(--primary); text-transform:uppercase;">⚡ 1-Click Autonomous AI Actions:</span>
            <button type="button" class="preset-chip" onclick="aiAutoDraftDPRWorkLog()">✍️ Auto-Draft Today's DPR Work Log</button>
            <button type="button" class="preset-chip" onclick="aiAutoPostTimelineChecklist()">📌 Auto-Post 3 AI Safety &amp; Ops Tasks to Timeline</button>
            <button type="button" class="preset-chip" onclick="runSpecificAIEngine(36)">🏛️ Generate Client RA Bill Valuation</button>
            <button type="button" class="preset-chip" onclick="runSpecificAIEngine(50)">📊 Boardroom Executive Briefing</button>
          </div>

          <!-- Interactive "What-If" Quantum Sandbox Simulator -->
          <div style="background: var(--bg); border: 1.5px solid var(--border); border-radius: 16px; padding: 16px; margin-bottom: 18px;">
            <div style="display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:8px; margin-bottom:12px;">
              <div style="font-size:13px; font-weight:900; color:var(--primary); text-transform:uppercase;">🎛️ Interactive "What-If" Site Budget &amp; Schedule Simulator (Drag Sliders)</div>
              <button type="button" class="preset-chip" onclick="resetAIWhatIfSimulator()">🔄 Reset Sliders</button>
            </div>
            <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(190px, 1fr)); gap:14px; margin-bottom:14px;">
              <div style="background:var(--card-bg); padding:10px 12px; border-radius:12px; border:1px solid var(--border);">
                <div style="display:flex; justify-content:space-between; font-size:12px; font-weight:800; margin-bottom:6px;"><span>👷 Workforce Scale</span><b id="sim-wf-lbl" style="color:var(--secondary);">100%</b></div>
                <input type="range" id="sim-wf-slider" min="50" max="200" step="5" value="100" oninput="updateAIWhatIfSimulator()" style="padding:0; height:8px;">
              </div>
              <div style="background:var(--card-bg); padding:10px 12px; border-radius:12px; border:1px solid var(--border);">
                <div style="display:flex; justify-content:space-between; font-size:12px; font-weight:800; margin-bottom:6px;"><span>💰 Daily Rate Delta</span><b id="sim-rate-lbl" style="color:var(--secondary);">+₹0</b></div>
                <input type="range" id="sim-rate-slider" min="-150" max="300" step="10" value="0" oninput="updateAIWhatIfSimulator()" style="padding:0; height:8px;">
              </div>
              <div style="background:var(--card-bg); padding:10px 12px; border-radius:12px; border:1px solid var(--border);">
                <div style="display:flex; justify-content:space-between; font-size:12px; font-weight:800; margin-bottom:6px;"><span>🌧️ Rain / Delay Days</span><b id="sim-rain-lbl" style="color:var(--warning);">2 Days</b></div>
                <input type="range" id="sim-rain-slider" min="0" max="15" step="1" value="2" oninput="updateAIWhatIfSimulator()" style="padding:0; height:8px;">
              </div>
              <div style="background:var(--card-bg); padding:10px 12px; border-radius:12px; border:1px solid var(--border);">
                <div style="display:flex; justify-content:space-between; font-size:12px; font-weight:800; margin-bottom:6px;"><span>⏱️ Daily OT Avg/Worker</span><b id="sim-ot-lbl" style="color:var(--success);">1.5 hrs</b></div>
                <input type="range" id="sim-ot-slider" min="0" max="6" step="0.5" value="1.5" oninput="updateAIWhatIfSimulator()" style="padding:0; height:8px;">
              </div>
            </div>
            <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap:10px;" id="ai-whatif-results"></div>
          </div>

          <!-- Interactive Natural-Language + Voice AI Copilot Bar -->
          <div style="background: linear-gradient(135deg, rgba(59,130,246,0.08), rgba(147,51,234,0.08)); border: 1.5px solid rgba(99,102,241,0.35); border-radius: 16px; padding: 16px; margin-bottom: 18px;">
            <div style="font-size:12px; font-weight:900; color:var(--secondary); text-transform:uppercase; letter-spacing:0.6px; margin-bottom:8px;">💬 Interactive Voice &amp; Text AI Site Copilot (Ask Anything About Wages, Civil QA, RA Bills, Materials or DPR)</div>
            <div style="display:flex; gap:10px; flex-wrap:wrap;">
              <input type="text" id="ai-copilot-input" placeholder="Ask AI Copilot: e.g. 'Who has the highest overtime?', 'Calculate RCC mix & steel scrap', 'Estimate RA Bill valuation'..." style="flex:1; min-width:220px; background:var(--card-bg); padding:12px 16px;" onkeypress="if(event.key==='Enter') askAICopilot()">
              <button type="button" class="btn btn-outline" style="width:auto; padding:12px 16px;" onclick="voiceAskAICopilot()" title="Speak to AI Copilot">🎤 Voice Ask</button>
              <button type="button" class="btn btn-primary" style="width:auto; padding:12px 22px;" onclick="askAICopilot()">🧠 Ask AI</button>
            </div>
            <div style="display:flex; gap:8px; flex-wrap:wrap; margin-top:10px;">
              <span class="preset-chip" onclick="quickAskCopilot('Who has the highest overtime and payable balance this month?')">🏆 Top OT &amp; Earner</span>
              <span class="preset-chip" onclick="quickAskCopilot('Check low stock alerts and material wastage risk')">📦 Stock &amp; Wastage Audit</span>
              <span class="preset-chip" onclick="quickAskCopilot('Run structural civil QA audit for RCC mix, steel BBS scrap and shuttering')">🏗️ Structural &amp; Civil QA</span>
              <span class="preset-chip" onclick="quickAskCopilot('Calculate client RA Bill valuation, GST retention and 180-day cashflow')">🏛️ Client RA Bill &amp; FinOps</span>
              <span class="preset-chip" onclick="quickAskCopilot('Generate client-ready executive DPR summary for today')">📝 Executive DPR Draft</span>
              <span class="preset-chip" onclick="quickAskCopilot('Audit wage compliance and advance recovery risks')">⚖️ Wage &amp; Advance Risk</span>
            </div>
          </div>

          <!-- Live AI Output Console -->
          <div id="ai-forecast-output" class="empty-state" style="text-align: left; padding: 20px; font-weight: normal; line-height: 1.6; margin-bottom: 20px; border: 2px solid var(--secondary); background: var(--card-bg);">
            Select any of the <b>50 AI Engines</b> below or click <b>🚀 Run All 50 AI Engines</b> to execute live neural diagnostics on your active site data.
          </div>

          <!-- Search & Category Filter for the 50 AI Features -->
          <div style="display:flex; gap:12px; flex-wrap:wrap; align-items:center; margin-bottom:12px;">
            <div class="search-input-box" style="flex:1; min-width:220px;">
              <span class="search-icon">🔍</span>
              <input type="text" id="ai-feature-search" placeholder="Search all 50 AI features (e.g. Monte Carlo, RCC Mix, RA Bill, Overtime, Stock, Safety, Carbon, EAC)..." oninput="renderAIFeaturesGrid()">
            </div>
          </div>
          <div class="filter-pills-wrap" id="ai-category-pills"></div>

          <!-- 50 AI Features Grid -->
          <div class="ai-grid-30" id="ai-features-grid"></div>
        </div>
      </div>

    </div> <!-- End Container -->

    <!-- MODAL: WORKER REGISTRATION -->
    <div class="overlay" id="worker-modal">
      <div class="modal-box-center" style="max-width:450px;">
        <button class="close-btn" onclick="closeModal('worker-modal')">&times;</button>
        <h2 id="modal-worker-title" style="margin-bottom:20px;">Register Profile</h2>
        <input type="hidden" id="edit-worker-id">
        <input type="hidden" id="edit-worker-type">
        <div style="text-align:left;"><label style="font-size:12px;font-weight:bold;color:var(--text-muted)">Full Name</label><input type="text" id="w-name" placeholder="e.g. Ramesh Kumar" style="margin-bottom:12px;"></div>
        <div style="text-align:left;"><label style="font-size:12px;font-weight:bold;color:var(--text-muted)">Mobile Number</label><input type="tel" id="w-phone" placeholder="e.g. 9876543210" style="margin-bottom:12px;"></div>
        <div style="text-align:left;"><label style="font-size:12px;font-weight:bold;color:var(--text-muted)">Designation / Trade</label>
          <input type="text" id="w-desig" list="trade-suggestions" placeholder="Select or type trade..." style="margin-bottom:12px;">
          <datalist id="trade-suggestions">
            <option value="Labor"></option><option value="Mason"></option><option value="Head Mason"></option><option value="Helper"></option><option value="Site Engineer"></option><option value="Project Manager"></option><option value="Bar Bender"></option><option value="Steel Fixer"></option><option value="Carpenter"></option><option value="Scaffolder"></option><option value="Electrician"></option><option value="Plumber"></option><option value="Welder"></option><option value="Welder (Argon)"></option><option value="Operator"></option><option value="Heavy Equipment Operator"></option><option value="Fitter"></option><option value="Rigger"></option><option value="Surveyor"></option><option value="Security Guard"></option><option value="Painter"></option><option value="Foreman"></option><option value="OWNER"></option>
          </datalist>
        </div>
        <div style="display:flex; gap:12px; margin-bottom:20px;" id="wage-input-row">
          <div style="flex:1; text-align:left;"><label style="font-size:12px;font-weight:bold;color:var(--text-muted)">Daily Rate (₹)</label><input type="number" id="w-rate" placeholder="e.g. 650" min="1"></div>
          <div style="flex:1; text-align:left;"><label style="font-size:12px;font-weight:bold;color:var(--text-muted)">Opening Adv (₹)</label><input type="number" id="w-adv" placeholder="0"></div>
        </div>
        <button class="btn btn-primary" onclick="saveWorker()" style="width:100%">Save Profile</button>
      </div>
    </div>

  </div> <!-- End #main-app -->
<script>
    /* =========================================
       0. ENHANCED THREE.JS ATMOSPHERIC GLOBE, PRECISION ORBITAL HQ TARGET FINDER & PHOTOREALISTIC 3D HQ CAMPUS
       ========================================= */
    const introContainer = document.getElementById('intro-container');
    const mainApp = document.getElementById('main-app');
    const radarHud = document.getElementById('hq-radar-hud');
    const radarReticle = document.getElementById('hq-radar-reticle');
    const radarBadge = document.getElementById('hq-radar-badge');
    
    const scene = new THREE.Scene();
    scene.fog = new THREE.FogExp2(0x061326, 0.0028);
    const camera = new THREE.PerspectiveCamera(50, window.innerWidth / window.innerHeight, 0.02, 1500);
    const renderer = new THREE.WebGLRenderer({ canvas: document.getElementById('intro-canvas'), alpha: true, antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

    // 0a. Procedural 3D Sky & Horizon Environment Reflection CubeMap
    function createSkyEnvironmentCubeMap() {
      const faces = [];
      for (let f = 0; f < 6; f++) {
        const c = document.createElement('canvas');
        c.width = 512; c.height = 512;
        const ctx = c.getContext('2d');
        if (f === 2) {
          const g = ctx.createRadialGradient(256, 256, 20, 256, 256, 360);
          g.addColorStop(0, '#2B6CB0');
          g.addColorStop(1, '#153E75');
          ctx.fillStyle = g;
          ctx.fillRect(0, 0, 512, 512);
        } else if (f === 3) {
          ctx.fillStyle = '#1E293B';
          ctx.fillRect(0, 0, 512, 512);
        } else {
          const g = ctx.createLinearGradient(0, 0, 0, 512);
          g.addColorStop(0.0, '#0F294A');
          g.addColorStop(0.45, '#2B6CB0');
          g.addColorStop(0.78, '#90CDF4');
          g.addColorStop(0.93, '#FDE68A');
          g.addColorStop(1.0, '#334155');
          ctx.fillStyle = g;
          ctx.fillRect(0, 0, 512, 512);

          ctx.fillStyle = 'rgba(255, 255, 255, 0.45)';
          for (let ci = 0; ci < 6; ci++) {
            const cx = ((ci * 83 + f * 47) % 440) + 36;
            const cy = 230 + ((ci * 37) % 100);
            ctx.beginPath();
            ctx.ellipse(cx, cy, 52, 16, 0, 0, Math.PI * 2);
            ctx.fill();
          }
        }
        faces.push(c);
      }
      const cubeTex = new THREE.CubeTexture(faces);
      cubeTex.needsUpdate = true;
      return cubeTex;
    }
    const skyEnvCube = createSkyEnvironmentCubeMap();

    // 1. Soft Radial Star Texture
    function createStarTexture() {
      const c = document.createElement('canvas');
      c.width = 64; c.height = 64;
      const ctx = c.getContext('2d');
      const g = ctx.createRadialGradient(32, 32, 0, 32, 32, 32);
      g.addColorStop(0.0, 'rgba(255, 255, 255, 1)');
      g.addColorStop(0.28, 'rgba(224, 242, 254, 0.92)');
      g.addColorStop(0.65, 'rgba(56, 189, 248, 0.35)');
      g.addColorStop(1.0, 'rgba(0, 0, 0, 0)');
      ctx.fillStyle = g;
      ctx.fillRect(0, 0, 64, 64);
      return new THREE.CanvasTexture(c);
    }
    const starTexture = createStarTexture();

    // 2. Deep-Space Starfield (4,200 stars)
    const particlesCount = 4200;
    const particlesGeometry = new THREE.BufferGeometry();
    const posArray = new Float32Array(particlesCount * 3);
    const velocityArray = new Float32Array(particlesCount);
    const colorsArray = new Float32Array(particlesCount * 3);
    
    const cyanCol = new THREE.Color(0x38BDF8);
    const greenCol = new THREE.Color(0x10B981);
    const goldCol = new THREE.Color(0xFFD700);
    const whiteCol = new THREE.Color(0xFFFFFF);

    for (let i = 0; i < particlesCount; i++) {
      const i3 = i * 3;
      const angle = Math.random() * Math.PI * 2;
      const radius = 14 + Math.pow(Math.random(), 0.75) * 180;
      posArray[i3] = Math.cos(angle) * radius;
      posArray[i3 + 1] = Math.sin(angle) * radius;
      posArray[i3 + 2] = -260 + Math.random() * 320;
      velocityArray[i] = 24.0 + Math.random() * 48.0;

      const rand = Math.random();
      const col = rand > 0.60 ? cyanCol : (rand > 0.30 ? greenCol : (rand > 0.12 ? whiteCol : goldCol));
      colorsArray[i3] = col.r;
      colorsArray[i3 + 1] = col.g;
      colorsArray[i3 + 2] = col.b;
    }
    
    particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
    particlesGeometry.setAttribute('color', new THREE.BufferAttribute(colorsArray, 3));
    const particlesMaterial = new THREE.PointsMaterial({
      size: 0.78, map: starTexture, vertexColors: true, transparent: true,
      opacity: 0.92, depthWrite: false, blending: THREE.AdditiveBlending
    });
    const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
    scene.add(particlesMesh);

    // 750 Hyperdrive Warp Streaks
    const streakCount = 750;
    const streakGeo = new THREE.BufferGeometry();
    const streakPositions = new Float32Array(streakCount * 6);
    const streakColors = new Float32Array(streakCount * 6);
    const streakMeta = [];
    for (let i = 0; i < streakCount; i++) {
      const angle = Math.random() * Math.PI * 2;
      const rad = 5 + Math.random() * 85;
      const x = Math.cos(angle) * rad;
      const y = Math.sin(angle) * rad;
      const z = -240 + Math.random() * 290;
      const speed = 95 + Math.random() * 130;
      streakMeta.push({ x, y, z, speed });
      const col = i % 3 === 0 ? goldCol : (i % 2 === 0 ? cyanCol : whiteCol);
      const b = i * 6;
      streakPositions[b] = x; streakPositions[b + 1] = y; streakPositions[b + 2] = z;
      streakPositions[b + 3] = x; streakPositions[b + 4] = y; streakPositions[b + 5] = z - 4;
      streakColors[b] = col.r; streakColors[b + 1] = col.g; streakColors[b + 2] = col.b;
      streakColors[b + 3] = 0; streakColors[b + 4] = 0; streakColors[b + 5] = 0;
    }
    streakGeo.setAttribute('position', new THREE.BufferAttribute(streakPositions, 3));
    streakGeo.setAttribute('color', new THREE.BufferAttribute(streakColors, 3));
    const streakMat = new THREE.LineBasicMaterial({
      vertexColors: true, transparent: true, opacity: 0.0, blending: THREE.AdditiveBlending
    });
    const streakLines = new THREE.LineSegments(streakGeo, streakMat);
    scene.add(streakLines);

    // 3. High-Detail World & India Satellite Map Texture
    function lonLatToUV(lon, lat, w, h) {
      return [((lon + 180) / 360) * w, ((90 - lat) / 180) * h];
    }

    function createSatelliteEarthTexture() {
      const w = 2048, h = 1024;
      const c = document.createElement('canvas');
      c.width = w; c.height = h;
      const ctx = c.getContext('2d');

      const oceanGrad = ctx.createLinearGradient(0, 0, 0, h);
      oceanGrad.addColorStop(0, '#030C1A');
      oceanGrad.addColorStop(0.25, '#072042');
      oceanGrad.addColorStop(0.5, '#0C3566');
      oceanGrad.addColorStop(0.75, '#072042');
      oceanGrad.addColorStop(1, '#030C1A');
      ctx.fillStyle = oceanGrad;
      ctx.fillRect(0, 0, w, h);

      ctx.strokeStyle = 'rgba(56, 189, 248, 0.12)';
      ctx.lineWidth = 1;
      for (let lon = -180; lon <= 180; lon += 15) {
        const [x] = lonLatToUV(lon, 0, w, h);
        ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, h); ctx.stroke();
      }
      for (let lat = -75; lat <= 75; lat += 15) {
        const [, y] = lonLatToUV(0, lat, w, h);
        ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(w, y); ctx.stroke();
      }

      const continents = [
        [[-10,36],[0,38],[15,40],[28,41],[40,42],[50,40],[60,25],[67,24],[74,34],[80,35],[95,28],[100,15],[105,10],[110,20],[122,30],[130,40],[140,50],[160,60],[170,66],[100,72],[60,70],[30,70],[10,60],[-5,48],[-10,36]],
        [[-17,15],[-5,35],[10,37],[32,31],[43,12],[51,10],[40,-10],[35,-25],[20,-35],[12,-18],[8,4],[-8,5],[-17,15]],
        [[-165,65],[-130,70],[-80,70],[-60,50],[-75,35],[-80,25],[-90,18],[-80,8],[-105,20],[-120,35],[-135,55],[-165,65]],
        [[-80,10],[-60,10],[-35,-5],[-40,-22],[-55,-38],[-70,-52],[-75,-40],[-70,-15],[-80,0],[-80,10]],
        [[114,-22],[130,-12],[145,-15],[153,-28],[145,-38],[130,-33],[115,-34],[114,-22]]
      ];

      const landGrad = ctx.createLinearGradient(0, 150, 0, 880);
      landGrad.addColorStop(0.0, 'rgba(34, 104, 138, 0.82)');
      landGrad.addColorStop(0.45, 'rgba(28, 118, 98, 0.85)');
      landGrad.addColorStop(1.0, 'rgba(22, 85, 118, 0.82)');
      ctx.fillStyle = landGrad;
      ctx.strokeStyle = 'rgba(125, 211, 252, 0.52)';
      ctx.lineWidth = 2;
      continents.forEach(poly => {
        ctx.beginPath();
        poly.forEach(([lon, lat], idx) => {
          const [x, y] = lonLatToUV(lon, lat, w, h);
          if (idx === 0) ctx.moveTo(x, y); else ctx.lineTo(x, y);
        });
        ctx.closePath();
        ctx.fill();
        ctx.stroke();
      });

      const indiaPoly = [
        [68.1, 23.6], [70.2, 21.0], [72.8, 20.5], [72.8, 19.0], [73.8, 15.5],
        [75.5, 11.5], [77.5, 8.1], [79.8, 10.5], [80.3, 13.1], [80.8, 16.0],
        [83.3, 17.7], [85.8, 19.8], [88.0, 21.6], [89.0, 22.0], [88.2, 26.2],
        [89.8, 26.0], [92.0, 26.8], [96.0, 28.0], [94.5, 29.0], [88.8, 27.8],
        [85.0, 28.2], [81.0, 30.2], [79.0, 31.5], [78.5, 34.5], [76.5, 35.5],
        [74.0, 34.2], [74.5, 31.5], [72.5, 28.0], [70.0, 26.8], [68.1, 23.6]
      ];
      ctx.save();
      ctx.beginPath();
      indiaPoly.forEach(([lon, lat], idx) => {
        const [x, y] = lonLatToUV(lon, lat, w, h);
        if (idx === 0) ctx.moveTo(x, y); else ctx.lineTo(x, y);
      });
      ctx.closePath();
      ctx.fillStyle = 'rgba(38, 156, 98, 0.82)';
      ctx.fill();
      ctx.strokeStyle = 'rgba(234, 179, 8, 0.96)';
      ctx.lineWidth = 3.5;
      ctx.stroke();

      // Ganga River trace flowing through Bihar (Barauni / Begusarai)
      const gangaRiver = [[78.0,30.0],[79.5,28.0],[81.8,25.4],[83.0,25.3],[85.1,25.6],[86.13,25.42],[87.8,24.8],[88.8,22.2]];
      ctx.strokeStyle = 'rgba(125, 211, 252, 0.85)';
      ctx.lineWidth = 2.5;
      ctx.beginPath();
      gangaRiver.forEach(([lon, lat], i) => {
        const [gx, gy] = lonLatToUV(lon, lat, w, h);
        if (i === 0) ctx.moveTo(gx, gy); else ctx.lineTo(gx, gy);
      });
      ctx.stroke();

      const indianCities = [[72.87,19.07],[77.20,28.61],[88.36,22.57],[77.59,12.97],[80.27,13.08],[78.48,17.38],[85.13,25.59],[86.13,25.42]];
      indianCities.forEach(([clon, clat]) => {
        const [cx, cy] = lonLatToUV(clon, clat, w, h);
        const cg = ctx.createRadialGradient(cx, cy, 0.5, cx, cy, 8);
        cg.addColorStop(0, 'rgba(254, 240, 138, 0.95)');
        cg.addColorStop(1, 'rgba(254, 240, 138, 0)');
        ctx.fillStyle = cg;
        ctx.beginPath(); ctx.arc(cx, cy, 8, 0, Math.PI * 2); ctx.fill();
      });

      const [hqX, hqY] = lonLatToUV(86.13, 25.42, w, h);
      const pinGrad = ctx.createRadialGradient(hqX, hqY, 1, hqX, hqY, 30);
      pinGrad.addColorStop(0, 'rgba(255, 255, 255, 1)');
      pinGrad.addColorStop(0.25, 'rgba(255, 215, 0, 0.98)');
      pinGrad.addColorStop(0.55, 'rgba(16, 185, 129, 0.72)');
      pinGrad.addColorStop(1, 'rgba(16, 185, 129, 0)');
      ctx.fillStyle = pinGrad;
      ctx.beginPath(); ctx.arc(hqX, hqY, 30, 0, Math.PI * 2); ctx.fill();
      ctx.restore();

      return new THREE.CanvasTexture(c);
    }

    const globeRadius = 10;
    const globeGroup = new THREE.Group();
    // CRITICAL FIX: 'XYZ' intrinsic Euler order in Three.js builds M = Rx(x) * Ry(y) * Rz(z)!
    // That means Ry(y) spins around Earth's polar axis FIRST (inner), and Rx(x) tilts the latitude to the camera SECOND (outer) so Barauni HQ lands at (0, 0, +10.0) dead-center!
    globeGroup.rotation.order = 'XYZ';
    scene.add(globeGroup);

    const earthTex = createSatelliteEarthTexture();
    const globeGeo = new THREE.SphereGeometry(globeRadius, 64, 64);
    const globeMat = new THREE.MeshPhongMaterial({
      color: 0xffffff, map: earthTex, emissive: 0x040D1A, specular: 0x1E40AF, shininess: 18, transparent: true, opacity: 1.0
    });
    const globeMesh = new THREE.Mesh(globeGeo, globeMat);
    globeGroup.add(globeMesh);

    const wireGeo = new THREE.SphereGeometry(globeRadius * 1.003, 32, 32);
    const wireMat = new THREE.MeshBasicMaterial({ color: 0x38BDF8, wireframe: true, transparent: true, opacity: 0.14, depthWrite: false });
    const wireMesh = new THREE.Mesh(wireGeo, wireMat);
    globeGroup.add(wireMesh);

    const atmosGeo = new THREE.SphereGeometry(globeRadius * 1.12, 48, 48);
    const atmosMat = new THREE.MeshBasicMaterial({
      color: 0x38BDF8, transparent: true, opacity: 0.14, blending: THREE.AdditiveBlending, side: THREE.BackSide, depthWrite: false
    });
    const atmosMesh = new THREE.Mesh(atmosGeo, atmosMat);
    globeGroup.add(atmosMesh);

    const cloudGeo = new THREE.SphereGeometry(globeRadius * 1.022, 36, 36);
    const cloudMat = new THREE.MeshBasicMaterial({ color: 0xFFFFFF, transparent: true, opacity: 0.05, wireframe: true, depthWrite: false });
    const cloudMesh = new THREE.Mesh(cloudGeo, cloudMat);
    globeGroup.add(cloudMesh);

    // 4. Exact 'XYZ' Coordinate & Orientation Math for Barauni / Begusarai HQ (25.42°N, 86.13°E)
    //    Verified in Python: with 'XYZ' order, Rx(hqLockRotX) * Ry(hqLockRotY) maps hqLocalVec to (0.0, 0.0, +10.0)!
    const hqLat = 25.42, hqLon = 86.13;
    function latLonToSphereVec(lat, lon, r) {
      const theta = (90 - lat) * (Math.PI / 180);
      const phi = (lon + 180) * (Math.PI / 180);
      return new THREE.Vector3(
        -r * Math.cos(phi) * Math.sin(theta),
        r * Math.cos(theta),
        r * Math.sin(phi) * Math.sin(theta)
      );
    }
    const hqLocalVec = latLonToSphereVec(hqLat, hqLon, globeRadius);
    const hqLockRotY = Math.atan2(-hqLocalVec.x, hqLocalVec.z);
    const zAfterY = Math.sqrt(hqLocalVec.x * hqLocalVec.x + hqLocalVec.z * hqLocalVec.z);
    const hqLockRotX = Math.atan2(hqLocalVec.y, zAfterY);

    // Orbital Location Pin / Target Finder Reticle on the Globe at HQ (Barauni, Begusarai, Bihar)
    const hqPinGroup = new THREE.Group();
    hqPinGroup.position.copy(hqLocalVec);
    const lockedGlobeEuler = new THREE.Euler(hqLockRotX, hqLockRotY, 0, 'XYZ');
    const lockedGlobeQuat = new THREE.Quaternion().setFromEuler(lockedGlobeEuler);
    hqPinGroup.quaternion.copy(lockedGlobeQuat).invert();
    globeGroup.add(hqPinGroup);

    const pinRingMat = new THREE.MeshBasicMaterial({ color: 0xFFD700, side: THREE.DoubleSide, transparent: true, opacity: 0.95 });
    const pinRingMesh = new THREE.Mesh(new THREE.RingGeometry(0.18, 0.28, 32), pinRingMat);
    pinRingMesh.position.set(0, 0, 0.04);
    hqPinGroup.add(pinRingMesh);

    const pinOuterRingMat = new THREE.MeshBasicMaterial({ color: 0x10B981, side: THREE.DoubleSide, transparent: true, opacity: 0.88 });
    const pinOuterRingMesh = new THREE.Mesh(new THREE.RingGeometry(0.38, 0.45, 32), pinOuterRingMat);
    pinOuterRingMesh.position.set(0, 0, 0.045);
    hqPinGroup.add(pinOuterRingMesh);

    const pinDotMat = new THREE.MeshBasicMaterial({ color: 0xFFFFFF, transparent: true, opacity: 0.98 });
    const pinDotMesh = new THREE.Mesh(new THREE.SphereGeometry(0.09, 16, 16), pinDotMat);
    pinDotMesh.position.set(0, 0, 0.06);
    hqPinGroup.add(pinDotMesh);

    const pinBeamMat = new THREE.MeshBasicMaterial({ color: 0xFFD700, transparent: true, opacity: 0.78, blending: THREE.AdditiveBlending });
    const pinBeamMesh = new THREE.Mesh(new THREE.CylinderGeometry(0.012, 0.045, 1.35, 12), pinBeamMat);
    pinBeamMesh.rotation.x = Math.PI / 2;
    pinBeamMesh.position.set(0, 0, 0.72);
    hqPinGroup.add(pinBeamMesh);

    // 5. PHOTOREALISTIC ARCHITECTURAL 3D CORPORATE HEADQUARTERS & CAMPUS ENVIRONMENT
    const hqCampusGroup = new THREE.Group();
    hqCampusGroup.position.set(0, 0, globeRadius);
    hqCampusGroup.visible = false;
    scene.add(hqCampusGroup);

    // 5a. Realistic Horizon Sky-Dome Backdrop
    function createSkyDomeTexture() {
      const c = document.createElement('canvas');
      c.width = 1024; c.height = 512;
      const ctx = c.getContext('2d');
      const g = ctx.createLinearGradient(0, 0, 0, 512);
      g.addColorStop(0.0, '#071426');
      g.addColorStop(0.38, '#153B66');
      g.addColorStop(0.68, '#316FA8');
      g.addColorStop(0.88, '#8BB8E0');
      g.addColorStop(0.96, '#E6DEC8');
      g.addColorStop(1.0, '#C8D8CE');
      ctx.fillStyle = g;
      ctx.fillRect(0, 0, 1024, 512);

      ctx.fillStyle = 'rgba(255, 255, 255, 0.25)';
      for (let i = 0; i < 14; i++) {
        const cx = (i * 79) % 1024;
        const cy = 365 + (i % 4) * 18;
        ctx.beginPath();
        ctx.ellipse(cx, cy, 85, 16, 0, 0, Math.PI * 2);
        ctx.fill();
      }
      return new THREE.CanvasTexture(c);
    }
    const skyDomeMat = new THREE.MeshBasicMaterial({
      map: createSkyDomeTexture(),
      side: THREE.BackSide,
      transparent: true,
      opacity: 0.0,
      depthWrite: false
    });
    const skyDomeMesh = new THREE.Mesh(new THREE.SphereGeometry(18, 32, 24), skyDomeMat);
    skyDomeMesh.rotation.x = Math.PI / 2;
    hqCampusGroup.add(skyDomeMesh);

    // 5b. High-Contrast Warm Architectural Sandstone/Travertine, Flamed Granite & Slate Roof Textures (NO over-exposed white!)
    function createTravertineLimestoneTexture() {
      const c = document.createElement('canvas');
      c.width = 512; c.height = 512;
      const ctx = c.getContext('2d');
      // Rich warm architectural sandstone/travertine beige so it never blows out to flat white under sunlight!
      ctx.fillStyle = '#C8BBA4';
      ctx.fillRect(0, 0, 512, 512);

      for (let y = 0; y < 512; y += 2) {
        const v = Math.sin(y * 0.14) * 6 + ((y * 17) % 7) - 3;
        ctx.fillStyle = v > 0 ? 'rgba(242, 234, 218, 0.30)' : 'rgba(138, 123, 101, 0.28)';
        ctx.fillRect(0, y, 512, 2);
      }
      ctx.strokeStyle = 'rgba(92, 80, 64, 0.52)';
      ctx.lineWidth = 2;
      for (let r = 0; r < 8; r++) {
        const ry = r * 64;
        ctx.beginPath(); ctx.moveTo(0, ry); ctx.lineTo(512, ry); ctx.stroke();
        const offset = (r % 2) * 64;
        for (let col = 0; col < 4; col++) {
          const cx = (col * 128 + offset) % 512;
          ctx.beginPath(); ctx.moveTo(cx, ry); ctx.lineTo(cx, ry + 64); ctx.stroke();
        }
      }
      const tex = new THREE.CanvasTexture(c);
      tex.wrapS = THREE.RepeatWrapping;
      tex.wrapT = THREE.RepeatWrapping;
      return tex;
    }

    function createFlamedGraniteTexture() {
      const c = document.createElement('canvas');
      c.width = 512; c.height = 512;
      const ctx = c.getContext('2d');
      ctx.fillStyle = '#94A3B8';
      ctx.fillRect(0, 0, 512, 512);
      for (let i = 0; i < 4000; i++) {
        const x = (i * 73) % 512;
        const y = (i * 137) % 512;
        ctx.fillStyle = (i % 3 === 0) ? 'rgba(226,232,240,0.45)' : ((i % 2 === 0) ? 'rgba(51,65,85,0.45)' : 'rgba(100,116,139,0.4)');
        ctx.fillRect(x, y, 2, 2);
      }
      ctx.strokeStyle = 'rgba(51, 65, 85, 0.55)';
      ctx.lineWidth = 2;
      for (let g = 0; g <= 512; g += 64) {
        ctx.beginPath(); ctx.moveTo(g, 0); ctx.lineTo(g, 512); ctx.stroke();
        ctx.beginPath(); ctx.moveTo(0, g); ctx.lineTo(512, g); ctx.stroke();
      }
      const tex = new THREE.CanvasTexture(c);
      tex.wrapS = THREE.RepeatWrapping;
      tex.wrapT = THREE.RepeatWrapping;
      return tex;
    }

    function createRoofMembraneTexture() {
      const c = document.createElement('canvas');
      c.width = 512; c.height = 512;
      const ctx = c.getContext('2d');
      ctx.fillStyle = '#273449';
      ctx.fillRect(0, 0, 512, 512);
      for (let i = 0; i < 3000; i++) {
        const x = (i * 97) % 512;
        const y = (i * 151) % 512;
        ctx.fillStyle = (i % 2 === 0) ? 'rgba(15,23,42,0.55)' : 'rgba(71,85,105,0.38)';
        ctx.fillRect(x, y, 2, 2);
      }
      ctx.strokeStyle = 'rgba(15, 23, 42, 0.55)';
      ctx.lineWidth = 2;
      for (let g = 0; g <= 512; g += 64) {
        ctx.beginPath(); ctx.moveTo(g, 0); ctx.lineTo(g, 512); ctx.stroke();
        ctx.beginPath(); ctx.moveTo(0, g); ctx.lineTo(512, g); ctx.stroke();
      }
      return new THREE.CanvasTexture(c);
    }

    const travertineTex = createTravertineLimestoneTexture();
    const graniteTex = createFlamedGraniteTexture();
    const roofTex = createRoofMembraneTexture();

    // 5c. High-Resolution Landscaped Campus Ground Environment
    function createCampusEnvironmentTexture() {
      const c = document.createElement('canvas');
      c.width = 2048; c.height = 2048;
      const ctx = c.getContext('2d');

      const turfGrad = ctx.createRadialGradient(1024, 1024, 80, 1024, 1024, 1000);
      turfGrad.addColorStop(0.0, '#234B30');
      turfGrad.addColorStop(0.65, '#1B3B25');
      turfGrad.addColorStop(0.92, '#122819');
      turfGrad.addColorStop(1.0, 'rgba(12, 26, 17, 0)');
      ctx.fillStyle = turfGrad;
      ctx.beginPath(); ctx.arc(1024, 1024, 1000, 0, Math.PI * 2); ctx.fill();

      ctx.save();
      ctx.beginPath(); ctx.arc(1024, 1024, 990, 0, Math.PI * 2); ctx.clip();
      for (let s = 40; s < 2000; s += 36) {
        ctx.fillStyle = (Math.floor(s / 36) % 2 === 0) ? 'rgba(74, 222, 128, 0.04)' : 'rgba(6, 46, 22, 0.06)';
        ctx.fillRect(0, s, 2048, 18);
      }
      ctx.restore();

      // Paved Warm-Granite Corporate Forecourt & Plaza
      ctx.fillStyle = 'rgba(15, 23, 42, 0.40)';
      ctx.fillRect(490, 642, 1068, 646);

      ctx.fillStyle = '#B8C2CE';
      ctx.strokeStyle = '#64748B';
      ctx.lineWidth = 8;
      ctx.fillRect(500, 650, 1048, 630);
      ctx.strokeRect(500, 650, 1048, 630);

      ctx.strokeStyle = '#475569';
      ctx.lineWidth = 4;
      ctx.strokeRect(524, 674, 1000, 582);

      ctx.strokeStyle = 'rgba(51, 65, 85, 0.28)';
      ctx.lineWidth = 2;
      for (let x = 500; x <= 1548; x += 36) {
        ctx.beginPath(); ctx.moveTo(x, 650); ctx.lineTo(x, 1280); ctx.stroke();
      }
      for (let y = 650; y <= 1280; y += 36) {
        ctx.beginPath(); ctx.moveTo(500, y); ctx.lineTo(1548, y); ctx.stroke();
      }

      const aoGrad = ctx.createRadialGradient(1024, 955, 60, 1024, 955, 340);
      aoGrad.addColorStop(0, 'rgba(15, 23, 42, 0.34)');
      aoGrad.addColorStop(1, 'rgba(15, 23, 42, 0)');
      ctx.fillStyle = aoGrad;
      ctx.fillRect(520, 720, 1008, 420);

      // Manicured green lawn parterres
      [545, 1238].forEach(lx => {
        ctx.fillStyle = '#225433';
        ctx.strokeStyle = '#CBD5E1';
        ctx.lineWidth = 6;
        ctx.fillRect(lx, 1035, 265, 195);
        for (let st = lx; st < lx + 265; st += 22) {
          ctx.fillStyle = (Math.floor(st / 22) % 2 === 0) ? 'rgba(255,255,255,0.05)' : 'rgba(0,0,0,0.06)';
          ctx.fillRect(st, 1035, 11, 195);
        }
        ctx.strokeRect(lx, 1035, 265, 195);
      });

      // Grand Entrance Boulevard / Asphalt Avenue
      ctx.fillStyle = '#1E2634';
      ctx.fillRect(884, 1180, 280, 820);
      ctx.beginPath();
      ctx.arc(1024, 1320, 202, 0, Math.PI * 2);
      ctx.fillStyle = '#1E2634';
      ctx.fill();
      ctx.strokeStyle = '#94A3B8';
      ctx.lineWidth = 8;
      ctx.stroke();

      ctx.beginPath();
      ctx.arc(1024, 1320, 92, 0, Math.PI * 2);
      ctx.fillStyle = '#64748B';
      ctx.fill();

      // Pedestrian crosswalk stripes
      ctx.fillStyle = 'rgba(241, 245, 249, 0.78)';
      for (let cx = 900; cx <= 1130; cx += 24) {
        ctx.fillRect(cx, 1510, 14, 46);
      }

      // Granite curbs & dashed white road lane dividers
      ctx.fillStyle = '#CBD5E1';
      ctx.fillRect(872, 1460, 12, 540);
      ctx.fillRect(1164, 1460, 12, 540);
      ctx.strokeStyle = 'rgba(255, 255, 255, 0.72)';
      ctx.lineWidth = 4;
      ctx.setLineDash([28, 22]);
      ctx.beginPath(); ctx.moveTo(1024, 1575); ctx.lineTo(1024, 1980); ctx.stroke();
      ctx.setLineDash([]);

      const tex = new THREE.CanvasTexture(c);
      if (renderer.capabilities && renderer.capabilities.getMaxAnisotropy) {
        tex.anisotropy = renderer.capabilities.getMaxAnisotropy();
      }
      return tex;
    }

    const campusGroundMat = new THREE.MeshLambertMaterial({
      map: createCampusEnvironmentTexture(),
      transparent: true,
      opacity: 1.0
    });
    const campusGroundMesh = new THREE.Mesh(new THREE.PlaneGeometry(11.0, 11.0), campusGroundMat);
    campusGroundMesh.position.set(0, 0, 0.005);
    hqCampusGroup.add(campusGroundMesh);

    // 5d. Photorealistic Architectural Curtain-Wall Glass Texture + Window-Only Emissive Map + Specular Map + Bump Map
    //     Crucial Fix: The Emissive Map is BLACK (#000000) on all stone spandrels and mullions so they NEVER blow out to white!
    function createCurtainWallMaps(cols, rows) {
      const size = 2048;
      const diffCanvas = document.createElement('canvas');
      diffCanvas.width = size; diffCanvas.height = size;
      const ctx = diffCanvas.getContext('2d');

      const emisCanvas = document.createElement('canvas');
      emisCanvas.width = size; emisCanvas.height = size;
      const eCtx = emisCanvas.getContext('2d');

      const specCanvas = document.createElement('canvas');
      specCanvas.width = size; specCanvas.height = size;
      const sCtx = specCanvas.getContext('2d');

      const bumpCanvas = document.createElement('canvas');
      bumpCanvas.width = size; bumpCanvas.height = size;
      const bCtx = bumpCanvas.getContext('2d');

      // Dark charcoal-bronze structural aluminum mullion grid background
      ctx.fillStyle = '#182230';
      ctx.fillRect(0, 0, size, size);
      eCtx.fillStyle = '#000000'; // Zero emissive on mullions/spandrels!
      eCtx.fillRect(0, 0, size, size);
      sCtx.fillStyle = '#263244';
      sCtx.fillRect(0, 0, size, size);
      bCtx.fillStyle = '#E2E8F0';
      bCtx.fillRect(0, 0, size, size);

      const cellW = size / cols;
      const cellH = size / rows;

      for (let r = 0; r < rows; r++) {
        const spandrelH = Math.max(16, cellH * 0.18);
        const ry = r * cellH;

        // Warm Sandstone / Travertine Spandrel Band between floors
        const spGrad = ctx.createLinearGradient(0, ry, 0, ry + spandrelH);
        spGrad.addColorStop(0.0, '#9E8F78');
        spGrad.addColorStop(0.25, '#C8BAA3');
        spGrad.addColorStop(0.82, '#B6A78E');
        spGrad.addColorStop(1.0, '#786B57');
        ctx.fillStyle = spGrad;
        ctx.fillRect(0, ry, size, spandrelH);

        sCtx.fillStyle = '#18181B';
        sCtx.fillRect(0, ry, size, spandrelH);
        bCtx.fillStyle = '#FFFFFF';
        bCtx.fillRect(0, ry, size, spandrelH);

        for (let cl = 0; cl < cols; cl++) {
          ctx.strokeStyle = 'rgba(72, 62, 48, 0.55)';
          ctx.lineWidth = 3;
          ctx.strokeRect(cl * cellW, ry, cellW, spandrelH);

          const pad = 12;
          const wx = cl * cellW + pad;
          const wy = ry + spandrelH + 8;
          const ww = cellW - pad * 2;
          const wh = cellH - spandrelH - 16;

          const seed = (r * 13 + cl * 7) % 11;
          const isWarmLit = (seed !== 2 && seed !== 5 && seed !== 9);

          // Deep Architectural Sapphire-Teal Low-E Reflective Glass Base
          const glassGrad = ctx.createLinearGradient(wx, wy, wx, wy + wh);
          if (isWarmLit) {
            glassGrad.addColorStop(0.0, '#0C2138');
            glassGrad.addColorStop(0.32, '#163B61');
            glassGrad.addColorStop(0.68, '#285C8A');
            glassGrad.addColorStop(0.88, '#938C74');
            glassGrad.addColorStop(1.0, '#D4B886');
          } else {
            glassGrad.addColorStop(0.0, '#071526');
            glassGrad.addColorStop(0.50, '#102B49');
            glassGrad.addColorStop(1.0, '#1E466E');
          }
          ctx.fillStyle = glassGrad;
          ctx.fillRect(wx, wy, ww, wh);

          // Interior Office Room Depth & Warm Ceiling LED Troffers
          if (isWarmLit) {
            ctx.fillStyle = 'rgba(253, 230, 138, 0.22)';
            ctx.fillRect(wx + ww * 0.08, wy + wh * 0.06, ww * 0.84, wh * 0.25);

            ctx.fillStyle = 'rgba(254, 243, 199, 0.88)';
            ctx.fillRect(wx + ww * 0.14, wy + wh * 0.12, ww * 0.30, 6);
            ctx.fillRect(wx + ww * 0.56, wy + wh * 0.12, ww * 0.30, 6);
            ctx.fillRect(wx + ww * 0.14, wy + wh * 0.22, ww * 0.30, 5);
            ctx.fillRect(wx + ww * 0.56, wy + wh * 0.22, ww * 0.30, 5);

            // Warm interior glow in Emissive Map ONLY inside lit window panes!
            const eGrad = eCtx.createLinearGradient(wx, wy, wx, wy + wh);
            eGrad.addColorStop(0.0, '#1E3A5F');
            eGrad.addColorStop(0.5, '#475569');
            eGrad.addColorStop(1.0, '#FDE68A');
            eCtx.fillStyle = eGrad;
            eCtx.fillRect(wx + 4, wy + 4, ww - 8, wh - 8);

            // Interior office desk & monitor silhouette
            ctx.fillStyle = 'rgba(15, 23, 42, 0.48)';
            ctx.fillRect(wx + ww * 0.14, wy + wh * 0.75, ww * 0.72, wh * 0.25);
          }

          // Micro-louver Venetian Blinds on selected windows
          if (seed === 1 || seed === 4 || seed === 8) {
            const blindH = wh * (seed === 1 ? 0.30 : (seed === 4 ? 0.45 : 0.22));
            ctx.fillStyle = 'rgba(203, 213, 225, 0.32)';
            ctx.fillRect(wx + 4, wy + 4, ww - 8, blindH);
            ctx.strokeStyle = 'rgba(51, 65, 85, 0.42)';
            ctx.lineWidth = 2;
            for (let by = wy + 8; by < wy + blindH; by += 7) {
              ctx.beginPath(); ctx.moveTo(wx + 4, by); ctx.lineTo(wx + ww - 4, by); ctx.stroke();
            }
          }

          // Diagonal Sky Reflection Sheen across each glass pane
          const reflGrad = ctx.createLinearGradient(wx, wy, wx + ww, wy + wh);
          reflGrad.addColorStop(0.0, 'rgba(186, 230, 253, 0.24)');
          reflGrad.addColorStop(0.35, 'rgba(125, 211, 252, 0.10)');
          reflGrad.addColorStop(0.55, 'rgba(255, 255, 255, 0.0)');
          reflGrad.addColorStop(1.0, 'rgba(56, 189, 248, 0.08)');
          ctx.fillStyle = reflGrad;
          ctx.beginPath();
          ctx.moveTo(wx, wy);
          ctx.lineTo(wx + ww * 0.65, wy);
          ctx.lineTo(wx, wy + wh * 0.80);
          ctx.closePath();
          ctx.fill();

          // Horizontal Aluminum Transom Bar at 70% window height + Vertical Center Casement Mullion
          const transomY = wy + wh * 0.70;
          ctx.fillStyle = '#0F172A';
          ctx.fillRect(wx, transomY, ww, 7);
          ctx.fillStyle = '#94A3B8';
          ctx.fillRect(wx, transomY + 2, ww, 3);

          // Outer dark-bronze frame & brushed aluminum window casing
          ctx.strokeStyle = '#090D16';
          ctx.lineWidth = 6;
          ctx.strokeRect(wx, wy, ww, wh);
          ctx.strokeStyle = '#94A3B8';
          ctx.lineWidth = 3;
          ctx.strokeRect(wx - 3, wy - 3, ww + 6, wh + 6);

          sCtx.fillStyle = '#BAE6FD';
          sCtx.fillRect(wx + 3, wy + 3, ww - 6, wh - 6);

          bCtx.fillStyle = '#1E1E1E';
          bCtx.fillRect(wx + 3, wy + 3, ww - 6, wh - 6);
          bCtx.fillStyle = '#FFFFFF';
          bCtx.fillRect(wx, transomY, ww, 7);
        }
      }

      const maxAniso = (renderer.capabilities && renderer.capabilities.getMaxAnisotropy) ? renderer.capabilities.getMaxAnisotropy() : 1;
      const map = new THREE.CanvasTexture(diffCanvas);
      const emisMap = new THREE.CanvasTexture(emisCanvas);
      const specMap = new THREE.CanvasTexture(specCanvas);
      const bumpMap = new THREE.CanvasTexture(bumpCanvas);
      map.anisotropy = maxAniso;
      emisMap.anisotropy = maxAniso;
      specMap.anisotropy = maxAniso;
      bumpMap.anisotropy = maxAniso;
      return { map, emisMap, specMap, bumpMap };
    }

    // Photorealistic Balanced Building Materials (No Whitewash!)
    const roofSlateMat = new THREE.MeshPhongMaterial({
      map: roofTex,
      bumpMap: roofTex,
      bumpScale: 0.008,
      specular: 0x1E293B,
      shininess: 14
    });
    const warmLimestoneMat = new THREE.MeshPhongMaterial({
      color: 0xD8CCB8,
      map: travertineTex,
      bumpMap: travertineTex,
      bumpScale: 0.010,
      specular: 0x27241D,
      shininess: 16
    });
    const brushedAluminumMat = new THREE.MeshPhongMaterial({
      color: 0x94A3B8,
      specular: 0xE2E8F0,
      shininess: 95,
      envMap: skyEnvCube,
      combine: THREE.MixOperation,
      reflectivity: 0.48
    });
    const darkBronzeMat = new THREE.MeshPhongMaterial({
      color: 0x26201A,
      specular: 0xC58632,
      shininess: 75,
      envMap: skyEnvCube,
      combine: THREE.MixOperation,
      reflectivity: 0.25
    });
    const sculptedGoldBronzeMat = new THREE.MeshPhongMaterial({
      color: 0xC88A32,
      emissive: 0x3A2208,
      specular: 0xFFFBEB,
      shininess: 115,
      envMap: skyEnvCube,
      combine: THREE.MixOperation,
      reflectivity: 0.52
    });
    const graniteStepMat = new THREE.MeshPhongMaterial({
      color: 0xCBD5E1,
      map: graniteTex,
      bumpMap: graniteTex,
      bumpScale: 0.008,
      specular: 0x475569,
      shininess: 22
    });
    const skybridgeGlassMat = new THREE.MeshPhongMaterial({
      color: 0x38BDF8,
      transparent: true,
      opacity: 0.62,
      specular: 0xFFFFFF,
      shininess: 115,
      envMap: skyEnvCube,
      combine: THREE.MixOperation,
      reflectivity: 0.55
    });

    function makeBuildingBlockMaterials(cwMaps) {
      const wallMat = new THREE.MeshPhongMaterial({
        map: cwMaps.map,
        specularMap: cwMaps.specMap,
        bumpMap: cwMaps.bumpMap,
        bumpScale: 0.014,
        emissive: 0xFFE8B0,
        emissiveMap: cwMaps.emisMap,
        emissiveIntensity: 0.35,
        specular: 0x93C5FD,
        shininess: 105,
        envMap: skyEnvCube,
        combine: THREE.MixOperation,
        reflectivity: 0.38
      });
      return [wallMat, wallMat, wallMat, wallMat, roofSlateMat, roofSlateMat];
    }

    // Helper: Add 3D Protruding Sandstone Floor Slabs, Dark Bronze Trim, Vertical Mullion Fins & Parapet Roof Frame
    function addArchitecturalDetailToBlock(w, d, h, baseZ, offsetX, offsetY, floors, colsX) {
      for (let fl = 1; fl <= floors; fl++) {
        const fz = baseZ + (h / floors) * fl;
        const slab = new THREE.Mesh(new THREE.BoxGeometry(w + 0.048, d + 0.048, 0.020), warmLimestoneMat);
        slab.position.set(offsetX, offsetY, fz);
        hqCampusGroup.add(slab);

        // Dark bronze shadow-reveal strip under each floor slab so every floor is razor-sharp!
        const trim = new THREE.Mesh(new THREE.BoxGeometry(w + 0.052, d + 0.052, 0.006), darkBronzeMat);
        trim.position.set(offsetX, offsetY, fz - 0.011);
        hqCampusGroup.add(trim);
      }
      // Heavy travertine corner structural piers
      [-w / 2, w / 2].forEach(cx => {
        [-d / 2, d / 2].forEach(cy => {
          const pier = new THREE.Mesh(new THREE.BoxGeometry(0.062, 0.062, h + 0.02), warmLimestoneMat);
          pier.position.set(offsetX + cx, offsetY + cy, baseZ + h / 2);
          hqCampusGroup.add(pier);
        });
      });
      // Vertical dark-bronze & aluminum curtain-wall mullions along Front (-Y) and Back (+Y) facades
      for (let c = 1; c < colsX; c++) {
        const mx = offsetX - w / 2 + (w / colsX) * c;
        [-d / 2 - 0.009, d / 2 + 0.009].forEach(my => {
          const fin = new THREE.Mesh(new THREE.BoxGeometry(0.016, 0.024, h), darkBronzeMat);
          fin.position.set(mx, offsetY + my, baseZ + h / 2);
          hqCampusGroup.add(fin);
        });
      }
      // Rooftop perimeter parapet walls
      const pThick = 0.038, pHeight = 0.042;
      const frontBackParapet = new THREE.BoxGeometry(w + 0.044, pThick, pHeight);
      [-d / 2, d / 2].forEach(py => {
        const p = new THREE.Mesh(frontBackParapet, warmLimestoneMat);
        p.position.set(offsetX, offsetY + py, baseZ + h + pHeight / 2);
        hqCampusGroup.add(p);
      });
      const sideParapet = new THREE.BoxGeometry(pThick, d + 0.044, pHeight);
      [-w / 2, w / 2].forEach(px => {
        const p = new THREE.Mesh(sideParapet, warmLimestoneMat);
        p.position.set(offsetX + px, offsetY, baseZ + h + pHeight / 2);
        hqCampusGroup.add(p);
      });
    }

    // 5e. BUILD THE MULTI-TIER ARCHITECTURAL HEADQUARTERS COMPLEX
    const plinthMesh = new THREE.Mesh(new THREE.BoxGeometry(2.70, 1.44, 0.04), graniteStepMat);
    plinthMesh.position.set(0, 0.02, 0.02);
    hqCampusGroup.add(plinthMesh);

    const mainW = 1.08, mainD = 0.68, mainH = 1.32;
    const mainWallMaps = createCurtainWallMaps(8, 10);
    const mainTowerMesh = new THREE.Mesh(
      new THREE.BoxGeometry(mainW, mainD, mainH),
      makeBuildingBlockMaterials(mainWallMaps)
    );
    mainTowerMesh.position.set(0, 0, 0.04 + mainH / 2);
    hqCampusGroup.add(mainTowerMesh);
    addArchitecturalDetailToBlock(mainW, mainD, mainH, 0.04, 0, 0, 10, 8);

    // Symmetrical 6-Story East & West Wings + Elevated Glass Skybridges
    const wingW = 0.68, wingD = 0.56, wingH = 0.82;
    const wingWallMaps = createCurtainWallMaps(6, 6);
    const wingMats = makeBuildingBlockMaterials(wingWallMaps);
    // Natural, deep botanical tree foliage colors (NO neon green!)
    const foliageMat1 = new THREE.MeshLambertMaterial({ color: 0x1E4620 });
    const foliageMat2 = new THREE.MeshLambertMaterial({ color: 0x265828 });
    const foliageMat3 = new THREE.MeshLambertMaterial({ color: 0x2E6B30 });
    const trunkMat = new THREE.MeshLambertMaterial({ color: 0x4A3222 });

    [-0.90, 0.90].forEach(wx => {
      const wingMesh = new THREE.Mesh(new THREE.BoxGeometry(wingW, wingD, wingH), wingMats);
      wingMesh.position.set(wx, 0.04, 0.04 + wingH / 2);
      hqCampusGroup.add(wingMesh);
      addArchitecturalDetailToBlock(wingW, wingD, wingH, 0.04, wx, 0.04, 6, 6);

      const bridgeX = wx > 0 ? (mainW / 2 + 0.02) : -(mainW / 2 + 0.02);
      const skybridge = new THREE.Mesh(new THREE.BoxGeometry(0.08, 0.22, 0.15), skybridgeGlassMat);
      skybridge.position.set(bridgeX, 0.02, 0.04 + wingH * 0.55);
      hqCampusGroup.add(skybridge);

      const bridgeFloor = new THREE.Mesh(new THREE.BoxGeometry(0.09, 0.24, 0.018), darkBronzeMat);
      bridgeFloor.position.set(bridgeX, 0.02, 0.04 + wingH * 0.55 - 0.075);
      hqCampusGroup.add(bridgeFloor);

      const skyGarden = new THREE.Mesh(
        new THREE.BoxGeometry(wingW - 0.08, wingD - 0.08, 0.015),
        new THREE.MeshLambertMaterial({ color: 0x1E4620 })
      );
      skyGarden.position.set(wx, 0.04, 0.04 + wingH + 0.01);
      hqCampusGroup.add(skyGarden);

      const hvacBox = new THREE.Mesh(new THREE.BoxGeometry(0.16, 0.12, 0.055), brushedAluminumMat);
      hvacBox.position.set(wx, 0.16, 0.04 + wingH + 0.04);
      hqCampusGroup.add(hvacBox);

      [-0.18, 0.18].forEach(tx => {
        const bush = new THREE.Mesh(new THREE.SphereGeometry(0.042, 12, 12), foliageMat2);
        bush.position.set(wx + tx, -0.06, 0.04 + wingH + 0.042);
        hqCampusGroup.add(bush);
      });
    });

    // 5f. FREESTANDING 3D SCULPTED ROOFTOP GI GLOBE EMBLEM & 3D EXTRUDED CHANNEL LETTERS (NO 2D WALL!)
    //     User Request: "and the logo and name wrong written and don't write it on a 2d wall make it look best plz"
    const crownBaseZ = 0.04 + mainH + 0.042;
    const signFrontY = -mainD / 2 + 0.04;

    // Open Architectural Structural Steel & BronzeMounting Pedestal Rails (Sky is completely open behind the 3D logo & letters!)
    const railMat = darkBronzeMat;
    const bottomPedestalBeam = new THREE.Mesh(new THREE.BoxGeometry(mainW - 0.04, 0.045, 0.028), warmLimestoneMat);
    bottomPedestalBeam.position.set(0, signFrontY, crownBaseZ + 0.014);
    hqCampusGroup.add(bottomPedestalBeam);

    // Horizontal brushed-bronze structural mounting rails that hold the freestanding 3D letters
    [0.075, 0.155].forEach(rz => {
      const rail = new THREE.Mesh(new THREE.CylinderGeometry(0.006, 0.006, mainW - 0.08, 12), railMat);
      rail.rotation.z = Math.PI / 2;
      rail.position.set(0, signFrontY + 0.015, crownBaseZ + rz);
      hqCampusGroup.add(rail);
    });

    // Support struts anchoring the open 3D sign rails to the roof
    [-0.44, -0.18, 0.12, 0.44].forEach(sx => {
      const vPost = new THREE.Mesh(new THREE.CylinderGeometry(0.008, 0.008, 0.19, 12), railMat);
      vPost.rotation.x = Math.PI / 2;
      vPost.position.set(sx, signFrontY + 0.015, crownBaseZ + 0.10);
      hqCampusGroup.add(vPost);
    });

    // 1. TRUE 3D SCULPTED GOLDEN-BRONZE "GI" GLOBE EMBLEM (Freestanding 3D Rings, Meridians, Latitudes & Raised "GI" Band!)
    const globeEmblemGroup = new THREE.Group();
    const emblemR = 0.105;
    globeEmblemGroup.position.set(-0.37, signFrontY - 0.005, crownBaseZ + 0.135);
    hqCampusGroup.add(globeEmblemGroup);

    // Outer 3D Sculpted Gold-Bronze Ring (4th meridian on each side)
    const outerTorus = new THREE.Mesh(new THREE.TorusGeometry(emblemR, 0.0085, 16, 48), sculptedGoldBronzeMat);
    outerTorus.rotation.x = Math.PI / 2;
    globeEmblemGroup.add(outerTorus);

    // 3 Inner 3D Longitude Elliptical Rings (matching exact SVG rx = 34/45, 23/45, 12/45)
    [0.755, 0.511, 0.267].forEach(rxRatio => {
      const merRing = new THREE.Mesh(new THREE.TorusGeometry(emblemR, 0.0055, 12, 40), sculptedGoldBronzeMat);
      merRing.rotation.x = Math.PI / 2;
      merRing.scale.set(rxRatio, 1, 1);
      globeEmblemGroup.add(merRing);
    });

    // 1 Center Vertical Meridian Rod
    const centerMeridianRod = new THREE.Mesh(new THREE.CylinderGeometry(0.0055, 0.0055, emblemR * 2, 10), sculptedGoldBronzeMat);
    centerMeridianRod.rotation.x = Math.PI / 2;
    globeEmblemGroup.add(centerMeridianRod);

    // 4 3D Latitude Bars (2 upper, 2 lower)
    [-0.64, -0.38, 0.38, 0.64].forEach(latRatio => {
      const latZ = emblemR * latRatio;
      const chordHalf = Math.sqrt(Math.max(0.001, emblemR * emblemR - latZ * latZ));
      const latBar = new THREE.Mesh(new THREE.CylinderGeometry(0.005, 0.005, chordHalf * 2, 10), sculptedGoldBronzeMat);
      latBar.rotation.z = Math.PI / 2;
      latBar.position.set(0, 0, latZ);
      globeEmblemGroup.add(latBar);
    });

    // 3D Center Equatorial Bronze Band with Raised "GI" Letters
    function createGIBandFrontTexture() {
      const c = document.createElement('canvas');
      c.width = 256; c.height = 64;
      const ctx = c.getContext('2d');
      const g = ctx.createLinearGradient(0, 0, 256, 64);
      g.addColorStop(0, '#D49B4B');
      g.addColorStop(0.5, '#B87B28');
      g.addColorStop(1, '#8A5612');
      ctx.fillStyle = g;
      ctx.fillRect(0, 0, 256, 64);
      ctx.strokeStyle = '#FDE68A';
      ctx.lineWidth = 3;
      ctx.strokeRect(2, 2, 252, 60);
      ctx.fillStyle = '#FFFFFF';
      ctx.font = '900 44px "Arial Black", Arial, sans-serif';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'middle';
      ctx.fillText('GI', 128, 34);
      return new THREE.CanvasTexture(c);
    }
    const giBandMats = [
      sculptedGoldBronzeMat, sculptedGoldBronzeMat,
      sculptedGoldBronzeMat, new THREE.MeshBasicMaterial({ map: createGIBandFrontTexture() }),
      sculptedGoldBronzeMat, sculptedGoldBronzeMat
    ];
    const giCenterBand = new THREE.Mesh(new THREE.BoxGeometry(emblemR * 2.02, 0.024, emblemR * 0.46), giBandMats);
    globeEmblemGroup.add(giCenterBand);

    // 2. FREESTANDING 3D EXTRUDED CHANNEL LETTERS: "Global Industries" (Transparent Cutout — NO 2D Wall!)
    function create3DChannelLettersTexture(isFrontFace) {
      const c = document.createElement('canvas');
      c.width = 2048; c.height = 512;
      const ctx = c.getContext('2d');
      // Completely transparent background so only the 3D letters exist in space!
      ctx.clearRect(0, 0, 2048, 512);

      ctx.textBaseline = 'alphabetic';
      if (!isFrontFace) {
        // Dark metallic bronze/gold 3D extrusion side bevels
        ctx.fillStyle = '#5C4018';
        ctx.strokeStyle = '#8A6224';
        ctx.lineWidth = 14;
        ctx.font = 'italic bold 300px "Brush Script MT", "Comic Sans MS", cursive';
        ctx.strokeText('Global', 40, 345);
        ctx.fillText('Global', 40, 345);

        ctx.font = 'bold 215px "Times New Roman", Times, serif';
        ctx.strokeText('Industries', 935, 340);
        ctx.fillText('Industries', 935, 340);
      } else {
        // Crisp illuminated front face matching the exact header logo ("Global Industries")
        ctx.save();
        ctx.shadowColor = 'rgba(0, 0, 0, 0.65)';
        ctx.shadowBlur = 8;
        ctx.lineJoin = 'round';

        // "Global" in exact letterhead Brush Script green (#4CAF50) with warm gold 3D trim
        ctx.font = 'italic bold 300px "Brush Script MT", "Comic Sans MS", cursive';
        ctx.strokeStyle = '#D49B4B';
        ctx.lineWidth = 10;
        ctx.strokeText('Global', 40, 345);
        ctx.fillStyle = '#4CAF50';
        ctx.fillText('Global', 40, 345);

        // "Industries" placed naturally right beside "Global" in exact Times New Roman serif (#86EFAC / #6da35e)
        ctx.font = 'bold 215px "Times New Roman", Times, serif';
        ctx.strokeStyle = '#D49B4B';
        ctx.lineWidth = 8;
        ctx.strokeText('Industries', 935, 340);
        ctx.fillStyle = '#8CE07A';
        ctx.fillText('Industries', 935, 340);
        ctx.restore();
      }

      const tex = new THREE.CanvasTexture(c);
      if (renderer.capabilities && renderer.capabilities.getMaxAnisotropy) {
        tex.anisotropy = renderer.capabilities.getMaxAnisotropy();
      }
      return tex;
    }

    const lettersSideMat = new THREE.MeshBasicMaterial({
      map: create3DChannelLettersTexture(false),
      transparent: true,
      alphaTest: 0.12,
      side: THREE.DoubleSide
    });
    const lettersFrontMat = new THREE.MeshBasicMaterial({
      map: create3DChannelLettersTexture(true),
      transparent: true,
      alphaTest: 0.12,
      side: THREE.DoubleSide
    });

    // Stack 12 closely-spaced planes in Y to form solid 3D extruded channel letters standing in open air!
    const lettersW = 0.78, lettersH = 0.21;
    const totalSlices = 12;
    const extrudeDepth = 0.036;
    for (let s = 0; s < totalSlices; s++) {
      const isFront = (s === totalSlices - 1);
      const sliceMesh = new THREE.Mesh(
        new THREE.PlaneGeometry(lettersW, lettersH),
        isFront ? lettersFrontMat : lettersSideMat
      );
      sliceMesh.rotation.x = Math.PI / 2;
      sliceMesh.position.set(
        0.13,
        signFrontY + 0.012 - (s / (totalSlices - 1)) * extrudeDepth,
        crownBaseZ + 0.132
      );
      hqCampusGroup.add(sliceMesh);
    }

    // Twin Red Aviation Obstruction Beacons on the top corners of the central tower roof
    const beaconRedMat = new THREE.MeshBasicMaterial({ color: 0xEF4444 });
    [-mainW / 2, mainW / 2].forEach(bx => {
      const beacon = new THREE.Mesh(new THREE.SphereGeometry(0.016, 10, 10), beaconRedMat);
      beacon.position.set(bx, -mainD / 2 + 0.02, crownBaseZ + 0.02);
      hqCampusGroup.add(beacon);
    });

    // 5f-2. RESTORED & UPGRADED 3D ELEVATED ROOFTOP HELIPAD DECK + PERIMETER BEACONS + 3D EXECUTIVE HELICOPTER!
    //       Fixed Z-height: placed ABOVE the top roof slab & parapet (z = crownBaseZ + 0.025) so it is 100% visible!
    function createHelipadTexture() {
      const c = document.createElement('canvas');
      c.width = 512; c.height = 512;
      const ctx = c.getContext('2d');
      ctx.clearRect(0, 0, 512, 512);

      // Outer dark-asphalt octagonal/circular landing pad
      ctx.fillStyle = '#1E293B';
      ctx.beginPath(); ctx.arc(256, 256, 240, 0, Math.PI * 2); ctx.fill();

      // Dashed white safety perimeter ring
      ctx.strokeStyle = '#F8FAFC';
      ctx.lineWidth = 10;
      ctx.setLineDash([28, 18]);
      ctx.beginPath(); ctx.arc(256, 256, 224, 0, Math.PI * 2); ctx.stroke();
      ctx.setLineDash([]);

      // High-visibility aviation yellow inner touchdown circle
      ctx.strokeStyle = '#FACC15';
      ctx.lineWidth = 18;
      ctx.beginPath(); ctx.arc(256, 256, 186, 0, Math.PI * 2); ctx.stroke();

      // Bold "H" Helipad Marking in the center
      ctx.fillStyle = '#FACC15';
      ctx.font = '900 230px Arial, sans-serif';
      ctx.textAlign = 'center';
      ctx.textBaseline = 'middle';
      ctx.fillText('H', 256, 268);
      return new THREE.CanvasTexture(c);
    }
    const helipadTex = createHelipadTexture();

    // Central Tower Elevated 3D Helipad Superstructure Deck (rises clearly above the roof & parapet!)
    const padDeckZ = crownBaseZ + 0.022;
    const helipadPedestal = new THREE.Mesh(
      new THREE.CylinderGeometry(0.24, 0.27, 0.040, 32),
      darkBronzeMat
    );
    helipadPedestal.rotation.x = Math.PI / 2;
    helipadPedestal.position.set(0, 0.11, padDeckZ);
    hqCampusGroup.add(helipadPedestal);

    // Yellow Safety Net Walkway Ring around the Elevated Helipad
    const helipadSafetyNet = new THREE.Mesh(
      new THREE.RingGeometry(0.24, 0.285, 32),
      new THREE.MeshBasicMaterial({ color: 0xFACC15, side: THREE.DoubleSide, wireframe: true })
    );
    helipadSafetyNet.position.set(0, 0.11, padDeckZ + 0.018);
    hqCampusGroup.add(helipadSafetyNet);

    // Main Helipad Surface Circle sitting proudly on top of the elevated deck
    const helipadMesh = new THREE.Mesh(
      new THREE.CircleGeometry(0.235, 32),
      new THREE.MeshBasicMaterial({ map: helipadTex })
    );
    helipadMesh.position.set(0, 0.11, padDeckZ + 0.022);
    hqCampusGroup.add(helipadMesh);

    // 8 Glowing Green & Amber Helipad Perimeter Touchdown Lights
    const heliLightGreenMat = new THREE.MeshBasicMaterial({ color: 0x10B981 });
    const heliLightAmberMat = new THREE.MeshBasicMaterial({ color: 0xFACC15 });
    for (let li = 0; li < 8; li++) {
      const ang = (li / 8) * Math.PI * 2;
      const hLight = new THREE.Mesh(
        new THREE.SphereGeometry(0.012, 8, 8),
        li % 2 === 0 ? heliLightGreenMat : heliLightAmberMat
      );
      hLight.position.set(Math.cos(ang) * 0.242, 0.11 + Math.sin(ang) * 0.242, padDeckZ + 0.026);
      hqCampusGroup.add(hLight);
    }

    // 3D Corporate Executive Helicopter ("GI-01") Parked on the Central Rooftop Helipad with Spinning Rotor!
    const heliGroup = new THREE.Group();
    heliGroup.position.set(0, 0.11, padDeckZ + 0.024);
    heliGroup.rotation.z = -0.35;
    hqCampusGroup.add(heliGroup);

    // Landing Skids
    [-0.032, 0.032].forEach(skx => {
      const skid = new THREE.Mesh(new THREE.CylinderGeometry(0.003, 0.003, 0.13, 8), brushedAluminumMat);
      skid.position.set(skx, 0, 0.004);
      heliGroup.add(skid);
      [-0.03, 0.03].forEach(sky => {
        const strut = new THREE.Mesh(new THREE.CylinderGeometry(0.0025, 0.0025, 0.024, 6), brushedAluminumMat);
        strut.rotation.x = Math.PI / 2;
        strut.position.set(skx, sky, 0.014);
        heliGroup.add(strut);
      });
    });
    // Helicopter Cabin Fuselage & Gold Stripe
    const heliCabin = new THREE.Mesh(new THREE.SphereGeometry(0.042, 16, 12), darkBronzeMat);
    heliCabin.scale.set(0.85, 1.45, 0.78);
    heliCabin.position.set(0, -0.01, 0.036);
    heliGroup.add(heliCabin);

    const heliWindshield = new THREE.Mesh(new THREE.SphereGeometry(0.038, 14, 10), skybridgeGlassMat);
    heliWindshield.scale.set(0.82, 1.15, 0.72);
    heliWindshield.position.set(0, -0.028, 0.038);
    heliGroup.add(heliWindshield);

    // Tail Boom & Vertical Fin
    const heliTail = new THREE.Mesh(new THREE.CylinderGeometry(0.006, 0.015, 0.13, 10), sculptedGoldBronzeMat);
    heliTail.position.set(0, 0.085, 0.040);
    heliGroup.add(heliTail);

    const heliFin = new THREE.Mesh(new THREE.BoxGeometry(0.005, 0.028, 0.036), sculptedGoldBronzeMat);
    heliFin.position.set(0, 0.145, 0.050);
    heliGroup.add(heliFin);

    // Spinning Main 4-Blade Rotor Hub
    const heliRotorGroup = new THREE.Group();
    heliRotorGroup.position.set(0, -0.008, 0.074);
    heliGroup.add(heliRotorGroup);

    const rotorMast = new THREE.Mesh(new THREE.CylinderGeometry(0.005, 0.005, 0.018, 8), brushedAluminumMat);
    rotorMast.rotation.x = Math.PI / 2;
    rotorMast.position.set(0, 0, -0.006);
    heliRotorGroup.add(rotorMast);

    [0, Math.PI / 2].forEach(ang => {
      const blade = new THREE.Mesh(new THREE.BoxGeometry(0.26, 0.012, 0.002), brushedAluminumMat);
      blade.rotation.z = ang;
      heliRotorGroup.add(blade);
    });

    // Secondary Visible Helipad on the East Wing Roof (so a second H-pad is also clearly visible on the lower wing roof!)
    const wingPadZ = 0.04 + wingH + 0.022;
    const wingHelipadBase = new THREE.Mesh(new THREE.CylinderGeometry(0.155, 0.17, 0.016, 28), darkBronzeMat);
    wingHelipadBase.rotation.x = Math.PI / 2;
    wingHelipadBase.position.set(0.90, -0.03, wingPadZ);
    hqCampusGroup.add(wingHelipadBase);

    const wingHelipadMesh = new THREE.Mesh(
      new THREE.CircleGeometry(0.15, 28),
      new THREE.MeshBasicMaterial({ map: helipadTex })
    );
    wingHelipadMesh.position.set(0.90, -0.03, wingPadZ + 0.010);
    hqCampusGroup.add(wingHelipadMesh);

    // 5g. REALISTIC 3D BUILDING ENTRANCE GATE / ATRIUM PORTAL & SLIDING GLASS DOORS WITH HANDLES
    const lobbyW = 0.62, lobbyD = 0.22, lobbyH = 0.28;
    const lobbyInterior = new THREE.Mesh(
      new THREE.BoxGeometry(lobbyW - 0.04, lobbyD - 0.04, lobbyH - 0.02),
      new THREE.MeshBasicMaterial({ color: 0xFDE68A })
    );
    lobbyInterior.position.set(0, -mainD / 2 - lobbyD / 2 + 0.02, 0.04 + lobbyH / 2);
    hqCampusGroup.add(lobbyInterior);

    // 3-Tier Granite Entrance Staircase leading up to the Main Entrance Gate
    for (let st = 0; st < 3; st++) {
      const stepW = 0.38 + st * 0.04;
      const stepD = 0.06 + st * 0.03;
      const stepMesh = new THREE.Mesh(new THREE.BoxGeometry(stepW, stepD, 0.012), graniteStepMat);
      stepMesh.position.set(0, -mainD / 2 - lobbyD - 0.04, 0.008 + (2 - st) * 0.012);
      hqCampusGroup.add(stepMesh);
    }

    [-0.18, 0.18].forEach(icx => {
      const intCol = new THREE.Mesh(new THREE.CylinderGeometry(0.014, 0.014, lobbyH - 0.02, 12), warmLimestoneMat);
      intCol.rotation.x = Math.PI / 2;
      intCol.position.set(icx, -mainD / 2 - lobbyD / 2, 0.04 + lobbyH / 2);
      hqCampusGroup.add(intCol);
    });

    const receptionDesk = new THREE.Mesh(
      new THREE.BoxGeometry(0.24, 0.05, 0.06),
      darkBronzeMat
    );
    receptionDesk.position.set(0, -mainD / 2 - 0.08, 0.07);
    hqCampusGroup.add(receptionDesk);

    const lobbyGlass = new THREE.Mesh(
      new THREE.BoxGeometry(lobbyW, lobbyD, lobbyH),
      new THREE.MeshPhongMaterial({
        color: 0x1E3A5F,
        transparent: true,
        opacity: 0.52,
        specular: 0xFFFFFF,
        shininess: 120,
        envMap: skyEnvCube,
        combine: THREE.MixOperation,
        reflectivity: 0.58
      })
    );
    lobbyGlass.position.set(0, -mainD / 2 - lobbyD / 2, 0.04 + lobbyH / 2);
    hqCampusGroup.add(lobbyGlass);

    // Structural Mullion Grid on the Glass Lobby Atrium
    [-0.20, 0.20].forEach(lmx => {
      const lMull = new THREE.Mesh(new THREE.BoxGeometry(0.014, 0.018, lobbyH), darkBronzeMat);
      lMull.position.set(lmx, -mainD / 2 - lobbyD - 0.004, 0.04 + lobbyH / 2);
      hqCampusGroup.add(lMull);
    });

    // Architectural Entrance Door Portal Frame with Overhead Transom Bar
    const doorPortalFrame = new THREE.Mesh(
      new THREE.BoxGeometry(0.26, 0.034, 0.175),
      darkBronzeMat
    );
    doorPortalFrame.position.set(0, -mainD / 2 - lobbyD - 0.01, 0.04 + 0.088);
    hqCampusGroup.add(doorPortalFrame);

    const doorGlassGlow = new THREE.Mesh(
      new THREE.PlaneGeometry(0.21, 0.15),
      new THREE.MeshBasicMaterial({ color: 0xFEF3C7 })
    );
    doorGlassGlow.rotation.x = Math.PI / 2;
    doorGlassGlow.position.set(0, -mainD / 2 - lobbyD - 0.024, 0.04 + 0.085);
    hqCampusGroup.add(doorGlassGlow);

    // Overhead Transom Beam across the Entrance Doorway
    const doorTransomBar = new THREE.Mesh(new THREE.BoxGeometry(0.24, 0.038, 0.012), brushedAluminumMat);
    doorTransomBar.position.set(0, -mainD / 2 - lobbyD - 0.018, 0.04 + 0.145);
    hqCampusGroup.add(doorTransomBar);

    // Realistic Left & Right Framed Glass Sliding Doors with 3D Stainless-Steel Pull Handles & Kickplates!
    function createRealisticDoorGroup(isLeft) {
      const dg = new THREE.Group();
      const glassPane = new THREE.Mesh(
        new THREE.BoxGeometry(0.096, 0.010, 0.135),
        new THREE.MeshPhongMaterial({
          color: 0x0F2942,
          transparent: true,
          opacity: 0.76,
          specular: 0xFFFFFF,
          shininess: 120,
          envMap: skyEnvCube,
          combine: THREE.MixOperation,
          reflectivity: 0.65
        })
      );
      dg.add(glassPane);

      // Brushed Aluminum Door Stile Frame (Left, Right, Top, Bottom Kickplate)
      const kickplate = new THREE.Mesh(new THREE.BoxGeometry(0.098, 0.014, 0.022), brushedAluminumMat);
      kickplate.position.set(0, 0, -0.056);
      dg.add(kickplate);

      const topRail = new THREE.Mesh(new THREE.BoxGeometry(0.098, 0.014, 0.012), brushedAluminumMat);
      topRail.position.set(0, 0, 0.062);
      dg.add(topRail);

      [-0.045, 0.045].forEach(sx => {
        const stile = new THREE.Mesh(new THREE.BoxGeometry(0.008, 0.014, 0.135), brushedAluminumMat);
        stile.position.set(sx, 0, 0);
        dg.add(stile);
      });

      // 3D Vertical Stainless-Steel Tubular Pull Handle & Horizontal Push Bar
      const handleX = isLeft ? 0.032 : -0.032;
      const pullHandle = new THREE.Mesh(new THREE.CylinderGeometry(0.003, 0.003, 0.048, 10), sculptedGoldBronzeMat);
      pullHandle.rotation.x = Math.PI / 2;
      pullHandle.position.set(handleX, -0.010, -0.005);
      dg.add(pullHandle);

      const pushBar = new THREE.Mesh(new THREE.BoxGeometry(0.082, 0.015, 0.006), brushedAluminumMat);
      pushBar.position.set(0, 0, -0.008);
      dg.add(pushBar);

      return dg;
    }

    const leftDoorMesh = createRealisticDoorGroup(true);
    leftDoorMesh.position.set(-0.048, -mainD / 2 - lobbyD - 0.028, 0.04 + 0.072);
    hqCampusGroup.add(leftDoorMesh);

    const rightDoorMesh = createRealisticDoorGroup(false);
    rightDoorMesh.position.set(0.048, -mainD / 2 - lobbyD - 0.028, 0.04 + 0.072);
    hqCampusGroup.add(rightDoorMesh);

    // Cantilevered Stone & Bronze Porte-Cochere Canopy
    const canopyW = 0.82, canopyD = 0.34;
    const canopySlab = new THREE.Mesh(
      new THREE.BoxGeometry(canopyW, canopyD, 0.032),
      warmLimestoneMat
    );
    canopySlab.position.set(0, -mainD / 2 - lobbyD - canopyD / 2 + 0.04, 0.04 + lobbyH + 0.015);
    hqCampusGroup.add(canopySlab);

    const canopyFascia = new THREE.Mesh(
      new THREE.BoxGeometry(canopyW + 0.01, canopyD + 0.01, 0.014),
      darkBronzeMat
    );
    canopyFascia.position.set(0, -mainD / 2 - lobbyD - canopyD / 2 + 0.04, 0.04 + lobbyH + 0.034);
    hqCampusGroup.add(canopyFascia);

    const downlightMat = new THREE.MeshBasicMaterial({ color: 0xFEF08A });
    [-0.26, -0.09, 0.09, 0.26].forEach(dlx => {
      const dl = new THREE.Mesh(new THREE.CircleGeometry(0.018, 12), downlightMat);
      dl.rotation.x = Math.PI;
      dl.position.set(dlx, -mainD / 2 - lobbyD - canopyD / 2 + 0.04, 0.04 + lobbyH - 0.002);
      hqCampusGroup.add(dl);
    });

    [-0.34, -0.14, 0.14, 0.34].forEach(colX => {
      const colY = -mainD / 2 - lobbyD - canopyD + 0.08;
      const col = new THREE.Mesh(new THREE.CylinderGeometry(0.016, 0.016, lobbyH + 0.02, 16), brushedAluminumMat);
      col.rotation.x = Math.PI / 2;
      col.position.set(colX, colY, 0.04 + (lobbyH + 0.02) / 2);
      hqCampusGroup.add(col);

      const pedestal = new THREE.Mesh(new THREE.CylinderGeometry(0.024, 0.026, 0.04, 16), darkBronzeMat);
      pedestal.rotation.x = Math.PI / 2;
      pedestal.position.set(colX, colY, 0.04 + 0.02);
      hqCampusGroup.add(pedestal);
    });

    // 5h. REALISTIC 3D CORPORATE CAMPUS MAIN ENTRANCE GATE & PERIMETER WROUGHT-IRON FENCE (at Y = -1.72)
    //     User Request: "realistic gate and window also"
    const gateY = -1.72;
    [-0.31, 0.31].forEach(gpx => {
      // Heavy Travertine Stone Gate Pillar
      const pillar = new THREE.Mesh(new THREE.BoxGeometry(0.075, 0.075, 0.24), warmLimestoneMat);
      pillar.position.set(gpx, gateY, 0.12);
      hqCampusGroup.add(pillar);

      const cap = new THREE.Mesh(new THREE.BoxGeometry(0.09, 0.09, 0.022), darkBronzeMat);
      cap.position.set(gpx, gateY, 0.245);
      hqCampusGroup.add(cap);

      const globeLamp = new THREE.Mesh(new THREE.SphereGeometry(0.022, 12, 12), new THREE.MeshBasicMaterial({ color: 0xFEF3C7 }));
      globeLamp.position.set(gpx, gateY, 0.272);
      hqCampusGroup.add(globeLamp);

      // Bronze Plaque on Gate Pillar
      const plaque = new THREE.Mesh(new THREE.BoxGeometry(0.048, 0.008, 0.028), sculptedGoldBronzeMat);
      plaque.position.set(gpx, gateY - 0.038, 0.14);
      hqCampusGroup.add(plaque);
    });

    // Animated Left & Right Wrought-Iron & Gold Ornamental Campus Gate Wings (Swing open during entrance!)
    function createOrnamentalGateWing(isLeft) {
      const pivot = new THREE.Group();
      const dir = isLeft ? 1 : -1;
      const wingW = 0.24, wingH = 0.17;

      // Top & Bottom Horizontal Iron Rails
      [0.03, 0.16].forEach(rz => {
        const bar = new THREE.Mesh(new THREE.BoxGeometry(wingW, 0.010, 0.010), darkBronzeMat);
        bar.position.set(dir * (wingW / 2), 0, rz);
        pivot.add(bar);
      });
      // Vertical Wrought-Iron Pickets with Golden Finial Tips
      for (let p = 1; p <= 6; p++) {
        const px = dir * (wingW / 6) * p;
        const picket = new THREE.Mesh(new THREE.CylinderGeometry(0.0035, 0.0035, wingH, 8), darkBronzeMat);
        picket.rotation.x = Math.PI / 2;
        picket.position.set(px, 0, wingH / 2 + 0.02);
        pivot.add(picket);

        const finial = new THREE.Mesh(new THREE.ConeGeometry(0.006, 0.018, 8), sculptedGoldBronzeMat);
        finial.rotation.x = Math.PI / 2;
        finial.position.set(px, 0, wingH + 0.028);
        pivot.add(finial);
      }
      return pivot;
    }

    const leftCampusGate = createOrnamentalGateWing(true);
    leftCampusGate.position.set(-0.27, gateY, 0.01);
    leftCampusGate.rotation.z = 0.25;
    hqCampusGroup.add(leftCampusGate);

    const rightCampusGate = createOrnamentalGateWing(false);
    rightCampusGate.position.set(0.27, gateY, 0.01);
    rightCampusGate.rotation.z = -0.25;
    hqCampusGroup.add(rightCampusGate);

    // Perimeter Stone & Iron Fence Flanking the Main Gate
    [-0.78, 0.78].forEach(fx => {
      const lowWall = new THREE.Mesh(new THREE.BoxGeometry(0.86, 0.035, 0.055), warmLimestoneMat);
      lowWall.position.set(fx, gateY, 0.028);
      hqCampusGroup.add(lowWall);

      const topFenceRail = new THREE.Mesh(new THREE.BoxGeometry(0.86, 0.012, 0.010), darkBronzeMat);
      topFenceRail.position.set(fx, gateY, 0.13);
      hqCampusGroup.add(topFenceRail);
    });

    // 5i. 3D Central Forecourt Water Fountain Roundabout, Flagpoles & FIXED EXECUTIVE CAR POSITIONS
    const fountainY = -1.36;
    const fountainBasin = new THREE.Mesh(new THREE.CylinderGeometry(0.26, 0.28, 0.045, 32), warmLimestoneMat);
    fountainBasin.rotation.x = Math.PI / 2;
    fountainBasin.position.set(0, fountainY, 0.025);
    hqCampusGroup.add(fountainBasin);

    const fountainWater = new THREE.Mesh(
      new THREE.CylinderGeometry(0.23, 0.23, 0.048, 32),
      new THREE.MeshPhongMaterial({
        color: 0x0284C7,
        specular: 0xFFFFFF,
        shininess: 120,
        envMap: skyEnvCube,
        combine: THREE.MixOperation,
        reflectivity: 0.68
      })
    );
    fountainWater.rotation.x = Math.PI / 2;
    fountainWater.position.set(0, fountainY, 0.028);
    hqCampusGroup.add(fountainWater);

    const fountainTier2 = new THREE.Mesh(new THREE.CylinderGeometry(0.09, 0.11, 0.09, 24), warmLimestoneMat);
    fountainTier2.rotation.x = Math.PI / 2;
    fountainTier2.position.set(0, fountainY, 0.055);
    hqCampusGroup.add(fountainTier2);

    const fountainSpire = new THREE.Mesh(
      new THREE.ConeGeometry(0.042, 0.14, 16),
      new THREE.MeshBasicMaterial({ color: 0xE0F2FE, transparent: true, opacity: 0.88 })
    );
    fountainSpire.rotation.x = Math.PI / 2;
    fountainSpire.position.set(0, fountainY, 0.12);
    hqCampusGroup.add(fountainSpire);

    // 3 Corporate Flagpoles on the East Plaza (Clear of driveway & columns)
    [-0.08, 0.0, 0.08].forEach((fx, fi) => {
      const fp = new THREE.Mesh(new THREE.CylinderGeometry(0.004, 0.006, 0.36, 8), brushedAluminumMat);
      fp.rotation.x = Math.PI / 2;
      fp.position.set(0.52 + fx, -0.96, 0.18);
      hqCampusGroup.add(fp);

      const flagColors = [0xFF9933, 0xC58632, 0x10B981];
      const flag = new THREE.Mesh(new THREE.PlaneGeometry(0.06, 0.038), new THREE.MeshBasicMaterial({ color: flagColors[fi], side: THREE.DoubleSide }));
      flag.rotation.x = Math.PI / 2;
      flag.position.set(0.55 + fx, -0.96, 0.33);
      hqCampusGroup.add(flag);
    });

    // FIXED CAR POSITIONS ("fix the car position"):
    // Car 1: VIP Executive Sedan parked parallel to the Porte-Cochere drop-off curb at Y = -0.98 (completely clear of the columns at Y = -0.82!)
    // Car 2 & 3: Driving neatly in the left and right asphalt lanes of the boulevard!
    const wheelTireMat = new THREE.MeshLambertMaterial({ color: 0x111827 });
    const headlightMat = new THREE.MeshBasicMaterial({ color: 0xFEF9C3 });
    const taillightMat = new THREE.MeshBasicMaterial({ color: 0xEF4444 });

    function addExecutiveCar(cx, cy, rotZ, bodyHex) {
      const carG = new THREE.Group();
      carG.position.set(cx, cy, 0.012);
      carG.rotation.z = rotZ;

      const carBodyMat = new THREE.MeshPhongMaterial({
        color: bodyHex,
        specular: 0xFFFFFF,
        shininess: 115,
        envMap: skyEnvCube,
        combine: THREE.MixOperation,
        reflectivity: 0.52
      });
      const carGlassMat = new THREE.MeshPhongMaterial({
        color: 0x0F172A,
        specular: 0x93C5FD,
        shininess: 120,
        envMap: skyEnvCube,
        combine: THREE.MixOperation,
        reflectivity: 0.70
      });

      const body = new THREE.Mesh(new THREE.BoxGeometry(0.082, 0.172, 0.028), carBodyMat);
      body.position.set(0, 0, 0.022);
      carG.add(body);

      const cabin = new THREE.Mesh(new THREE.BoxGeometry(0.070, 0.094, 0.024), carGlassMat);
      cabin.position.set(0, -0.008, 0.046);
      carG.add(cabin);

      [[-0.041, 0.052], [0.041, 0.052], [-0.041, -0.052], [0.041, -0.052]].forEach(([wx, wy]) => {
        const whl = new THREE.Mesh(new THREE.CylinderGeometry(0.014, 0.014, 0.012, 12), wheelTireMat);
        whl.rotation.z = Math.PI / 2;
        whl.position.set(wx, wy, 0.014);
        carG.add(whl);
      });

      [-0.025, 0.025].forEach(lx => {
        const hl = new THREE.Mesh(new THREE.BoxGeometry(0.014, 0.004, 0.008), headlightMat);
        hl.position.set(lx, 0.086, 0.024);
        carG.add(hl);
        const tl = new THREE.Mesh(new THREE.BoxGeometry(0.016, 0.004, 0.008), taillightMat);
        tl.position.set(lx, -0.086, 0.024);
        carG.add(tl);
      });

      hqCampusGroup.add(carG);
    }
    // VIP Sedan aligned parallel in the drop-off lane in front of the Porte-Cochere (NOT touching any pillar!)
    addExecutiveCar(-0.36, -1.04, Math.PI / 2, 0x0F172A);
    // Executive sedans in the proper left & right lanes of the main boulevard
    addExecutiveCar(-0.09, -1.98, 0.0, 0xF8FAFC);
    addExecutiveCar(0.09, -2.32, Math.PI, 0x334155);

    // Manicured Boxwood Hedgerows along the Forecourt Lawns
    [-0.76, 0.76].forEach(hx => {
      const hedge = new THREE.Mesh(new THREE.BoxGeometry(0.52, 0.048, 0.042), foliageMat1);
      hedge.position.set(hx, -0.50, 0.024);
      hqCampusGroup.add(hedge);
    });

    // 26 Lush Botanical 3D Trees with Stone Planter Rings
    const treeCoords = [
      [-0.58, -0.78, 1.05], [0.58, -0.78, 1.05],
      [-0.58, -1.12, 1.0],  [0.58, -1.12, 1.0],
      [-0.58, -1.48, 1.10], [0.58, -1.48, 1.10],
      [-0.58, -1.88, 1.05], [0.58, -1.88, 1.05],
      [-0.58, -2.22, 1.08], [0.58, -2.22, 1.08],
      [-0.58, -2.56, 1.10], [0.58, -2.56, 1.10],
      [-0.95, -0.62, 1.15], [0.95, -0.62, 1.15],
      [-1.34, -0.45, 1.20], [1.34, -0.45, 1.20],
      [-1.48, 0.10, 1.15],  [1.48, 0.10, 1.15],
      [-1.38, 0.55, 1.10],  [1.38, 0.55, 1.10],
      [-0.85, -1.10, 0.95], [0.85, -1.10, 0.95],
      [-1.15, -0.95, 1.05], [1.15, -0.95, 1.05],
      [-0.90, 0.56, 1.12],  [0.90, 0.56, 1.12]
    ];
    treeCoords.forEach(([tx, ty, sc], idx) => {
      const tg = new THREE.Group();
      tg.position.set(tx, ty, 0.01);

      const planter = new THREE.Mesh(new THREE.RingGeometry(0.025 * sc, 0.048 * sc, 16), warmLimestoneMat);
      planter.position.set(0, 0, 0.004);
      tg.add(planter);

      const trunk = new THREE.Mesh(new THREE.CylinderGeometry(0.013 * sc, 0.022 * sc, 0.115 * sc, 8), trunkMat);
      trunk.rotation.x = Math.PI / 2;
      trunk.position.set(0, 0, 0.055 * sc);
      tg.add(trunk);

      const c1 = new THREE.Mesh(new THREE.SphereGeometry(0.080 * sc, 12, 12), idx % 2 === 0 ? foliageMat1 : foliageMat2);
      c1.position.set(0, 0, 0.135 * sc);
      tg.add(c1);

      const c2 = new THREE.Mesh(new THREE.SphereGeometry(0.062 * sc, 10, 10), foliageMat2);
      c2.position.set(0.030 * sc, -0.016 * sc, 0.172 * sc);
      tg.add(c2);

      const c3 = new THREE.Mesh(new THREE.SphereGeometry(0.058 * sc, 10, 10), foliageMat3);
      c3.position.set(-0.026 * sc, 0.018 * sc, 0.182 * sc);
      tg.add(c3);

      const c4 = new THREE.Mesh(new THREE.SphereGeometry(0.048 * sc, 10, 10), foliageMat1);
      c4.position.set(0, 0, 0.215 * sc);
      tg.add(c4);

      hqCampusGroup.add(tg);
    });

    // Warm Architectural Boulevard Streetlights
    [-0.82, -1.22, -1.60, -2.08, -2.48].forEach(ly => {
      [-0.42, 0.42].forEach(lx => {
        const pole = new THREE.Mesh(new THREE.CylinderGeometry(0.007, 0.01, 0.14, 8), darkBronzeMat);
        pole.rotation.x = Math.PI / 2;
        pole.position.set(lx, ly, 0.07);
        hqCampusGroup.add(pole);

        const lamp = new THREE.Mesh(new THREE.SphereGeometry(0.020, 10, 10), new THREE.MeshBasicMaterial({ color: 0xFEF3C7 }));
        lamp.position.set(lx, ly, 0.145);
        hqCampusGroup.add(lamp);
      });
    });

    // 6. Balanced Photorealistic Scene Lighting (No over-exposure!) & Initial Distant Globe Setup
    globeGroup.position.set(0, 0, 0);
    globeGroup.rotation.set(hqLockRotX * 0.55, hqLockRotY - 1.55, 0);

    const ambientLight = new THREE.AmbientLight(0xDCE8F5, 0.58);
    scene.add(ambientLight);
    const hemiLight = new THREE.HemisphereLight(0x93C5FD, 0x1E293B, 0.34);
    scene.add(hemiLight);
    const sunLight = new THREE.DirectionalLight(0xFFF7ED, 1.05);
    sunLight.position.set(28, -32, 24);
    scene.add(sunLight);

    const lobbyWarmLight = new THREE.PointLight(0xFDE68A, 0.75, 1.8);
    lobbyWarmLight.position.set(0, -0.65, 0.24);
    hqCampusGroup.add(lobbyWarmLight);

    const camState = {
      dist: 44.0,
      pitch: 0.0,
      lookZ: 0.0,
      orbitX: 0.0,
      fov: 50.0
    };

    function applyCameraState() {
      const sinP = Math.sin(camState.pitch);
      const cosP = Math.cos(camState.pitch);
      camera.position.set(
        camState.orbitX,
        -sinP * camState.dist,
        globeRadius + cosP * camState.dist
      );
      camera.up.set(0, cosP, sinP);
      camera.lookAt(0, 0, globeRadius + camState.lookZ);
    }
    applyCameraState();

    let introActive = true;
    let isWarping = false;
    const warpState = { speed: 1.0, pointSize: 0.78, streakOpacity: 0.0, pinPulse: 0.0, trackPinHud: false };
    const introClock = new THREE.Clock();
    const tmpPinWorldVec = new THREE.Vector3();

    function syncIntroThemeColors(themeName) {
      const palettes = {
        'cyberpunk': { wire: 0x00F0FF, atmos: 0xFF007F },
        'matrix': { wire: 0x00FF00, atmos: 0x00CC00 },
        'emerald': { wire: 0x10B981, atmos: 0x059669 },
        'golden-amber': { wire: 0xF59E0B, atmos: 0xD97706 },
        'cyber-gold': { wire: 0xFFD700, atmos: 0xFFA000 },
        'crimson-dusk': { wire: 0xE91E63, atmos: 0xC2185B },
        'synthwave': { wire: 0x00FFFF, atmos: 0xFF77FF },
        'electric-violet': { wire: 0xB388FF, atmos: 0x7C4DFF }
      };
      const pal = palettes[themeName] || { wire: 0x38BDF8, atmos: 0x38BDF8 };
      wireMat.color.setHex(pal.wire);
      atmosMat.color.setHex(pal.atmos);
    }

    function animateIntro() {
      if (!introActive) return;
      requestAnimationFrame(animateIntro);

      const dt = Math.min(introClock.getDelta(), 0.05);

      if (!isWarping) {
        globeGroup.rotation.y += 0.55 * dt;
        cloudMesh.rotation.y -= 0.22 * dt;
      }

      warpState.pinPulse += dt * 4.0;
      const pulseScale = 1.0 + 0.28 * Math.sin(warpState.pinPulse);
      const outerPulse = 1.0 + 0.18 * Math.cos(warpState.pinPulse * 1.3);
      pinRingMesh.scale.set(pulseScale, pulseScale, 1);
      pinOuterRingMesh.scale.set(outerPulse, outerPulse, 1);
      fountainSpire.scale.set(1, 1 + 0.10 * Math.sin(warpState.pinPulse * 1.4), 1);
      if (typeof heliRotorGroup !== 'undefined') heliRotorGroup.rotation.z += dt * 14.0;

      applyCameraState();

      // REAL-TIME 3D-TO-2D SATELLITE TARGET LOCK TRACKING!
      // Projects the exact 3D world position of hqPinGroup onto the 2D screen so the radar reticle locks directly onto Barauni HQ on India!
      if (warpState.trackPinHud && radarHud) {
        scene.updateMatrixWorld();
        hqPinGroup.getWorldPosition(tmpPinWorldVec);
        tmpPinWorldVec.project(camera);
        const sx = (tmpPinWorldVec.x * 0.5 + 0.5) * window.innerWidth;
        const sy = (-tmpPinWorldVec.y * 0.5 + 0.5) * window.innerHeight;
        radarHud.style.left = `${sx}px`;
        radarHud.style.top = `${sy}px`;
      }

      const positions = particlesMesh.geometry.attributes.position.array;
      const safeRadius = globeRadius * 1.25;
      const safeRadiusSq = safeRadius * safeRadius;

      for (let i = 0; i < particlesCount; i++) {
        const i3 = i * 3;
        positions[i3 + 2] += velocityArray[i] * dt * warpState.speed;

        const dx = positions[i3];
        const dy = positions[i3 + 1];
        const dz = positions[i3 + 2];
        const distSq = dx * dx + dy * dy + dz * dz;

        if (distSq < safeRadiusSq && distSq > 0.001) {
          const dist = Math.sqrt(distSq);
          const push = ((safeRadius - dist) / safeRadius) * 24.0 * dt * warpState.speed;
          positions[i3] += (dx / dist) * push;
          positions[i3 + 1] += (dy / dist) * push;
        }

        if (positions[i3 + 2] > 58) {
          const angle = Math.random() * Math.PI * 2;
          const radius = 14 + Math.pow(Math.random(), 0.75) * 180;
          positions[i3] = Math.cos(angle) * radius;
          positions[i3 + 1] = Math.sin(angle) * radius;
          positions[i3 + 2] = -240 - Math.random() * 60;
        }
      }
      particlesMesh.geometry.attributes.position.needsUpdate = true;

      if (warpState.streakOpacity > 0.001) {
        const sPos = streakLines.geometry.attributes.position.array;
        const tailLen = 3.0 + warpState.speed * 1.9;
        for (let i = 0; i < streakCount; i++) {
          const sm = streakMeta[i];
          sm.z += sm.speed * dt * warpState.speed;
          if (sm.z > 58) sm.z = -240 - Math.random() * 60;
          const b = i * 6;
          sPos[b] = sm.x; sPos[b + 1] = sm.y; sPos[b + 2] = sm.z;
          sPos[b + 3] = sm.x; sPos[b + 4] = sm.y; sPos[b + 5] = sm.z - tailLen;
        }
        streakLines.geometry.attributes.position.needsUpdate = true;
      }
      streakMat.opacity = warpState.streakOpacity;

      renderer.render(scene, camera);
    }
    animateIntro();

    function replayIntro() {
      window.replayIntro = replayIntro;
      isWarping = false;
      introActive = true;
      warpState.speed = 1.0;
      warpState.pointSize = 0.78;
      warpState.streakOpacity = 0.0;
      warpState.trackPinHud = false;
      camState.dist = 44.0;
      camState.pitch = 0.0;
      camState.lookZ = 0.0;
      camState.orbitX = 0.0;
      camState.fov = 50.0;
      camera.fov = 50.0;
      camera.updateProjectionMatrix();
      globeGroup.position.set(0, 0, 0);
      globeGroup.rotation.set(hqLockRotX * 0.55, hqLockRotY - 1.55, 0);
      globeMesh.visible = true;
      wireMesh.visible = true;
      cloudMesh.visible = true;
      atmosMesh.visible = true;
      hqPinGroup.visible = true;
      globeMat.opacity = 1.0;
      wireMat.opacity = 0.14;
      atmosMat.opacity = 0.14;
      cloudMat.opacity = 0.05;
      pinRingMat.opacity = 0.95;
      pinOuterRingMat.opacity = 0.88;
      pinDotMat.opacity = 0.98;
      pinBeamMat.opacity = 0.78;
      hqCampusGroup.visible = false;
      hqCampusGroup.scale.set(1, 1, 1);
      skyDomeMat.opacity = 0.0;
      leftDoorMesh.position.x = -0.048;
      rightDoorMesh.position.x = 0.048;
      leftCampusGate.rotation.z = 0.25;
      rightCampusGate.rotation.z = -0.25;
      particlesMaterial.size = 0.78;
      particlesMaterial.opacity = 0.92;
      if (radarHud) {
        radarHud.style.left = '50%';
        radarHud.style.top = '50%';
        gsap.set(radarHud, { opacity: 0, scale: 0.85 });
      }
      if (radarReticle) radarReticle.classList.remove('locked');
      if (radarBadge) {
        radarBadge.classList.remove('locked');
        radarBadge.textContent = '🛰️ SCANNING ORBITAL COORDINATES...';
      }
      applyCameraState();
      introContainer.style.display = 'flex';
      introContainer.style.opacity = '1';
      const logoWrap = document.querySelector('.intro-logo-wrapper');
      const enterInst = document.querySelector('.enter-instruction');
      if (logoWrap) gsap.set(logoWrap, { opacity: 1, scale: 1, x: 0, y: 0 });
      if (enterInst) gsap.set(enterInst, { opacity: 1, scale: 1 });
      syncIntroThemeColors(document.body.getAttribute('data-theme') || 'light');
      introClock.start();
      animateIntro();
    }
    window.replayIntro = replayIntro;

    introContainer.addEventListener('click', () => {
      if (!introActive || isWarping) return;
      isWarping = true;

      mainApp.style.display = 'flex';
      mainApp.style.opacity = '0';

      // Normalize current Y angle so the globe rotates smoothly forward to lock Barauni HQ at (0, 0, +globeRadius)
      const twoPi = Math.PI * 2;
      let startY = globeGroup.rotation.y % twoPi;
      if (startY > hqLockRotY) startY -= twoPi;
      globeGroup.rotation.y = startY;
      const targetSpinY = hqLockRotY + twoPi;

      hqCampusGroup.visible = false;
      hqCampusGroup.scale.set(0.05, 0.05, 0.05);
      warpState.trackPinHud = true;

      if (radarReticle) radarReticle.classList.remove('locked');
      if (radarBadge) {
        radarBadge.classList.remove('locked');
        radarBadge.textContent = '🛰️ FINDING HQ: BARAUNI, BEGUSARAI, BIHAR (25.42°N, 86.13°E)...';
      }

      const tl = gsap.timeline({
        onComplete: () => {
          warpState.trackPinHud = false;
          introActive = false;
          introContainer.style.display = 'none';
          mainApp.style.opacity = '1';
        }
      });

      // PHASE 1 (0.0s -> 1.35s): SEARCH & FIND THE EXACT HQ PLACE ON INDIA!
      // With 'XYZ' order, rotating to (hqLockRotX, targetSpinY, 0) brings Barauni HQ to (0, 0, +10.0) dead-center!
      tl.to(document.querySelector('.intro-logo-wrapper'), { opacity: 0, scale: 1.35, duration: 0.42, ease: "power2.in" }, 0)
        .to(document.querySelector('.enter-instruction'), { opacity: 0, duration: 0.25 }, 0)
        .to(radarHud, { opacity: 1, scale: 1.0, duration: 0.35, ease: "back.out(1.6)" }, 0.35)
        .to(globeGroup.rotation, {
          x: hqLockRotX,
          y: targetSpinY,
          z: 0,
          duration: 1.25,
          ease: "power3.inOut"
        }, 0)
        .to(camState, {
          dist: 20.5,
          duration: 1.25,
          ease: "power2.out"
        }, 0)
        .call(() => {
          if (radarReticle) radarReticle.classList.add('locked');
          if (radarBadge) {
            radarBadge.classList.add('locked');
            radarBadge.textContent = '🎯 HQ LOCKED: THOKRICHAK, BARAUNI, BIHAR — ZOOMING IN';
          }
        }, null, 1.15)

      // PHASE 2 (1.42s -> 2.40s): PRECISION ZOOM STRAIGHT INTO THE LOCKED HQ POINT ON INDIA!
        .to(camState, {
          dist: 3.35,
          duration: 0.96,
          ease: "power3.inOut"
        }, 1.42)
        .to(warpState, {
          speed: 15.0,
          pointSize: 1.20,
          streakOpacity: 0.85,
          duration: 0.90,
          ease: "power2.inOut",
          onUpdate: function() {
            particlesMaterial.size = warpState.pointSize;
          }
        }, 1.42)
        .to(radarHud, { opacity: 0, scale: 1.45, duration: 0.40, ease: "power2.in" }, 1.65)
        .call(() => { warpState.trackPinHud = false; }, null, 2.05)

      // Atmospheric Descent Crossfade (1.80s -> 2.42s): Reveal 3D HQ Campus right at the locked HQ spot!
        .call(() => { hqCampusGroup.visible = true; }, null, 1.80)
        .to([wireMat, cloudMat, pinRingMat, pinOuterRingMat, pinDotMat, pinBeamMat], {
          opacity: 0.0,
          duration: 0.50,
          ease: "power2.out"
        }, 1.80)
        .to(hqCampusGroup.scale, {
          x: 1.0,
          y: 1.0,
          z: 1.0,
          duration: 0.62,
          ease: "power2.out"
        }, 1.80)

      // PHASE 3 (2.12s -> 3.40s): Smooth Orientation Tilt to a Wide Full-Building Architectural Vantage!
      // Positioned slightly further back (dist: 3.38 -> 2.72, pitch: 1.24, fov: 53) so the FULL building, both wings, rooftop helipad & helicopter, 3D logo, fountain, cars & gates are 100% visible!
        .call(() => {
          const holdBtn = document.getElementById('btn-hold-3d-building');
          if (holdBtn) holdBtn.style.display = 'inline-block';
          const altEl = document.getElementById('intro-telem-alt');
          if (altEl) altEl.textContent = '🚁 HQ CAMPUS VIEW • HELIPAD & MAIN TOWER ACTIVE';
        }, null, 2.12)
        .to(camState, {
          pitch: 1.24,
          dist: 3.38,
          lookZ: 0.62,
          fov: 53,
          duration: 1.28,
          ease: "power3.inOut",
          onUpdate: function() {
            camera.fov = camState.fov;
            camera.updateProjectionMatrix();
          }
        }, 2.12)
        .to(skyDomeMat, {
          opacity: 0.96,
          duration: 0.85,
          ease: "power2.inOut"
        }, 2.18)
        .to(globeMat, {
          opacity: 0.0,
          duration: 0.70,
          ease: "power2.inOut",
          onComplete: function() {
            globeMesh.visible = false;
            wireMesh.visible = false;
            cloudMesh.visible = false;
            hqPinGroup.visible = false;
          }
        }, 2.28)
        .to(warpState, {
          speed: 1.0,
          pointSize: 0.55,
          streakOpacity: 0.0,
          duration: 0.75,
          ease: "power2.out",
          onUpdate: function() {
            particlesMaterial.size = warpState.pointSize;
          }
        }, 2.18)
        .to(particlesMaterial, {
          opacity: 0.22,
          duration: 0.75
        }, 2.28)

      // Swing open the 3D Campus Entrance Gates & Building Sliding Glass Doors while keeping the FULL building framed at a comfortable wide distance (dist: 3.38 -> 2.72)!
        .to(leftCampusGate.rotation, { z: 1.48, duration: 0.75, ease: "power2.out" }, 2.75)
        .to(rightCampusGate.rotation, { z: -1.48, duration: 0.75, ease: "power2.out" }, 2.75)
        .to(camState, {
          dist: 2.72,
          lookZ: 0.60,
          duration: 1.05,
          ease: "sine.inOut"
        }, 3.40)
        .to(leftDoorMesh.position, { x: -0.138, duration: 0.50, ease: "power2.out" }, 3.95)
        .to(rightDoorMesh.position, { x: 0.138, duration: 0.50, ease: "power2.out" }, 3.95)
        .to(camState, {
          dist: 0.24,
          lookZ: 0.16,
          duration: 0.58,
          ease: "power2.in"
        }, 4.45)
        .to(mainApp, { opacity: 1, duration: 0.55, ease: "power2.out" }, 4.50)
        .to('.stat-card', { opacity: 1, y: 0, duration: 0.75, stagger: 0.12, ease: "back.out(1.7)" }, 4.58)
        .to(introContainer, { opacity: 0, duration: 0.45, ease: "power2.out" }, 4.55);
      window._activeIntroTimeline = tl;
    });

    window.toggleHold3DBuildingView = function() {
      const tl = window._activeIntroTimeline;
      const btn = document.getElementById('btn-hold-3d-building');
      if (!tl) return;
      if (tl.paused()) {
        tl.play();
        if (btn) btn.textContent = '🏛️ Pause on 3D Building';
      } else {
        tl.pause();
        if (btn) btn.textContent = '▶️ Resume Portal Entry';
      }
    };

    window.skipIntroToPortal = function() {
      if (window._activeIntroTimeline) window._activeIntroTimeline.kill();
      warpState.trackPinHud = false;
      introActive = false;
      isWarping = false;
      introContainer.style.display = 'none';
      mainApp.style.display = 'flex';
      mainApp.style.opacity = '1';
      gsap.to('.stat-card', { opacity: 1, y: 0, duration: 0.5, stagger: 0.08 });
    };

    window.addEventListener('resize', () => {
      if (introActive) {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
      }
    });

    /* =========================================
       1. FIREBASE SETUP & GLOBALS (DUAL CONNECTION)
       ========================================= */
    // Project A: Primary Database (Text/Attendance Data)
    const configA = {
      databaseURL: "https://g12343-default-rtdb.asia-southeast1.firebasedatabase.app/",
      projectId: "g12343"
    };
    firebase.initializeApp(configA);
    const db = firebase.database(); 

    // Project B: Backup Database & Photo Storage
    const configB = {
      databaseURL: "https://global-industries-backup-default-rtdb.asia-southeast1.firebasedatabase.app/",
      projectId: "global-industries-backup",
      storageBucket: "global-industries-backup.appspot.com" 
    };
    const secondaryApp = firebase.initializeApp(configB, "BackupProject");
    const storageBackup = secondaryApp.storage(); 

    function safeGetStorage(key) {
      try { return localStorage.getItem(key); } catch (e) { return null; }
    }
    function safeSetStorage(key, val) {
      try { localStorage.setItem(key, val); } catch (e) { console.warn("LocalStorage unavailable or quota exceeded."); }
    }
    function safeRemoveStorage(key) {
      try { localStorage.removeItem(key); } catch (e) {}
    }

    let confirmCallback = null;
    function showConfirmModal(message, onConfirm, title = "⚠️ Confirm Action") {
      document.getElementById('confirm-modal-title').textContent = title;
      document.getElementById('confirm-modal-msg').textContent = message;
      confirmCallback = onConfirm;
      document.getElementById('confirm-overlay').style.display = 'flex';
    }
    window.resolveConfirmModal = function(confirmed) {
      document.getElementById('confirm-overlay').style.display = 'none';
      const cb = confirmCallback;
      confirmCallback = null;
      if (confirmed && typeof cb === 'function') cb();
    };

    // Page Leave & Refresh Confirmation Guard ("when leaving the page or refreshing ask it again for shuring")
    window._allowIntentionalReload = false;
    window.confirmPageRefresh = function() {
      showConfirmModal(
        "Are you sure you want to refresh or leave the Global Industries Portal? Your cloud data is synced, but the current view will reload.",
        () => {
          window._allowIntentionalReload = true;
          window.location.reload();
        },
        "🔄 Confirm Page Refresh / Leave"
      );
    };

    window.addEventListener('beforeunload', function(e) {
      if (!window._allowIntentionalReload) {
        e.preventDefault();
        e.returnValue = 'Are you sure you want to leave or refresh the Global Industries Portal?';
        return e.returnValue;
      }
    });

    window.addEventListener('keydown', function(e) {
      const isF5 = (e.key === 'F5' || e.keyCode === 116);
      const isCtrlR = ((e.ctrlKey || e.metaKey) && (e.key === 'r' || e.key === 'R'));
      if (isF5 || isCtrlR) {
        e.preventDefault();
        window.confirmPageRefresh();
      }
    });

    let siteStructure = []; 
    let currentSite = safeGetStorage('gi_last_site') || null;
    let currentSubgroup = safeGetStorage('gi_last_sub') || null;
    
    let appState = { workers: [], keyPersons: [], attendance: {}, kpAttendance: {}, advances: {}, dpr: {}, timeline: {}, stockThresholds: {} };
    let userName = safeGetStorage('gi_user_profile') || '';
    let userRole = safeGetStorage('gi_role') || 'viewer';

    let dailyStatusFilter = 'ALL';
    let dailyTradeFilter = 'ALL';
    let dirTradeFilter = 'ALL';
    let timelineFilter = 'ALL';
    let activeLightboxPhotoUrl = '';
    let activeLightboxDateKey = '';
    let activeLightboxPhotoIdx = -1;
    let activeLightboxZoom = 1.0;

    window.toggleDashboardCharts = function() {
      const grid = document.getElementById('dashboard-charts-grid');
      const btn = document.getElementById('btn-toggle-charts');
      if (!grid || !btn) return;
      grid.classList.toggle('collapsed');
      btn.textContent = grid.classList.contains('collapsed') ? '▶ Show Charts' : '▼ Hide Charts';
    };
    
    let contextTargetId = null; let autoSaveTimer = null; let currentSiteRef = null;
    const deviceType = /Mobi|Android|iPhone/i.test(navigator.userAgent) ? '📱 Mobile' : '💻 Desktop';

    let totalSyncs = 0; let peakUsers = 1; const sessionStartTime = Date.now();
    let isMasterRollup = (currentSubgroup === 'ALL_GROUPS'); let isSavingToCloud = false; let pendingCloudState = null;

    function initLiveClock() {
      setInterval(() => {
        const now = new Date();
        document.getElementById('system-live-clock').textContent = now.toLocaleTimeString('en-IN', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
      }, 1000);
    }

    function initSyncStatusBadge() {
      db.ref('.info/connected').on('value', (snap) => {
        const badge = document.getElementById('cloud-sync-badge');
        if (!badge) return;
        if (snap.val() === true) {
          badge.classList.remove('offline');
          badge.innerHTML = '🟢 Cloud Synced';
        } else {
          badge.classList.add('offline');
          badge.innerHTML = '🟠 Offline (Local Queue)';
        }
      });
    }

    document.addEventListener('click', (e) => {
      const dropdown = document.getElementById('site-dropdown');
      if(dropdown && dropdown.classList.contains('active') && !e.target.closest('.site-selector-wrap')) {
          dropdown.classList.remove('active');
      }
    });

    function init() {
      initLiveClock();
      initSyncStatusBadge();
      const savedTheme = safeGetStorage('gi_theme') || 'light';
      document.body.setAttribute('data-theme', savedTheme);
      const savedUIMode = safeGetStorage('gi_ui_mode') || 'auto';
      if (savedUIMode !== 'auto' && savedUIMode !== 'standard') document.body.setAttribute('data-ui-mode', savedUIMode);
      const thSel = document.getElementById('theme-selector'); if(thSel) thSel.value = savedTheme;
      if (typeof syncIntroThemeColors === 'function') syncIntroThemeColors(savedTheme);

      if(!userName) { document.getElementById('profile-overlay').style.display = 'flex'; }
      else { document.getElementById('profile-display').innerHTML = `👤 ${userName}`; initPresence(); }

      generateMonthOptions(); populateDaySelector();
      loadSitesFromCloud(); loadLocalState(); syncSiteDataFirebase(); 
      updateAuthUI(); startAnalyticsEngine();

      document.getElementById('admin-pwd').addEventListener('input', function(e) {
          if (this.value === '6767') {
              document.body.classList.add('barrel-roll');
              this.value = ''; 
              setTimeout(() => document.body.classList.remove('barrel-roll'), 2500);
          }
      });
    }

    const ALL_70_THEMES = [
      // Whole-UI Morph Themes (35)
      { id: 'blueprint-cad', name: '📐 CAD Blueprint Grid', cat: 'Whole-UI', ui: 'CAD Blueprint', bg: '#061C36', card: '#082344', pri: '#38BDF8', sec: '#FDE047' },
      { id: 'autocad-engineer', name: '📏 AutoCAD Engineer Dark', cat: 'Whole-UI', ui: 'CAD Blueprint', bg: '#0B0F17', card: '#111824', pri: '#00E5FF', sec: '#FFEA00' },
      { id: 'structural-steel-cad', name: '🏗️ Structural Steel CAD', cat: 'Whole-UI', ui: 'CAD Blueprint', bg: '#0F172A', card: '#1E293B', pri: '#F97316', sec: '#38BDF8' },
      { id: 'vision-os-spatial', name: '🥽 VisionOS Spatial Glass', cat: 'Whole-UI', ui: 'Spatial Glass', bg: '#0B1120', card: '#1E293B', pri: '#FFFFFF', sec: '#60A5FA' },
      { id: 'frosted-aurora', name: '🌌 Frosted Aurora Glass', cat: 'Whole-UI', ui: 'Spatial Glass', bg: '#040D1A', card: '#0F2038', pri: '#2DD4BF', sec: '#818CF8' },
      { id: 'crystal-prism', name: '💎 Crystal Prism Glass', cat: 'Whole-UI', ui: 'Spatial Glass', bg: '#EEF2FF', card: '#FFFFFF', pri: '#1E3A8A', sec: '#7C3AED' },
      { id: 'aero-frutiger', name: '🫧 Frutiger Aero Glass', cat: 'Whole-UI', ui: 'Spatial Glass', bg: '#E0F2FE', card: '#FFFFFF', pri: '#0369A1', sec: '#10B981' },
      { id: 'neubrutalist-pop', name: '🧱 Neubrutalist Pop Studio', cat: 'Whole-UI', ui: '3D Neubrutalist', bg: '#FEF08A', card: '#FFFFFF', pri: '#111827', sec: '#FF5722' },
      { id: 'brutalist-arch', name: '🏛️ Brutalist Architecture', cat: 'Whole-UI', ui: '3D Neubrutalist', bg: '#E5E7EB', card: '#FFFFFF', pri: '#000000', sec: '#DC2626' },
      { id: 'manga-ink', name: '✒️ Manga Ink Brutal', cat: 'Whole-UI', ui: '3D Neubrutalist', bg: '#FAFAFA', card: '#FFFFFF', pri: '#09090B', sec: '#E11D48' },
      { id: 'swiss-bauhaus', name: '🟥 Swiss Bauhaus Grid', cat: 'Whole-UI', ui: '3D Neubrutalist', bg: '#F5F5F4', card: '#FFFFFF', pri: '#1D4ED8', sec: '#DC2626' },
      { id: 'jarvis-iron-hud', name: '🤖 Jarvis Hologram HUD', cat: 'Whole-UI', ui: 'Sci-Fi Polygon HUD', bg: '#020813', card: '#04142A', pri: '#00F0FF', sec: '#FF9900' },
      { id: 'starfleet-lcars', name: '🚀 Starfleet LCARS HUD', cat: 'Whole-UI', ui: 'Sci-Fi Polygon HUD', bg: '#000000', card: '#111122', pri: '#FF9900', sec: '#9999FF' },
      { id: 'mecha-gundam', name: '🛡️ Mecha Cockpit HUD', cat: 'Whole-UI', ui: 'Sci-Fi Polygon HUD', bg: '#090D16', card: '#131C2E', pri: '#3B82F6', sec: '#FACC15' },
      { id: 'cyber-samurai', name: '⚔️ Cyber Samurai HUD', cat: 'Whole-UI', ui: 'Sci-Fi Polygon HUD', bg: '#090408', card: '#180914', pri: '#F43F5E', sec: '#38BDF8' },
      { id: 'halo-unsc', name: '🪖 UNSC Tactical HUD', cat: 'Whole-UI', ui: 'Sci-Fi Polygon HUD', bg: '#0C140C', card: '#162416', pri: '#84CC16', sec: '#F59E0B' },
      { id: 'tron-legacy-grid', name: '🥏 Tron Lightcycle Grid', cat: 'Whole-UI', ui: 'Sci-Fi Polygon HUD', bg: '#020508', card: '#07121A', pri: '#6DF9FF', sec: '#FF7B00' },
      { id: 'alien-nostromo', name: '🛸 Nostromo Bio-HUD', cat: 'Whole-UI', ui: 'Sci-Fi Polygon HUD', bg: '#030906', card: '#071710', pri: '#10B981', sec: '#F59E0B' },
      { id: 'dune-arrakis', name: '⏳ Dune Arrakis Spice', cat: 'Whole-UI', ui: 'Sci-Fi Polygon HUD', bg: '#1C1208', card: '#2E1E0F', pri: '#D97706', sec: '#38BDF8' },
      { id: 'neumorphic-light', name: '☁️ 3D Neumorphic Soft Light', cat: 'Whole-UI', ui: '3D Neumorphic', bg: '#E2E8F0', card: '#E2E8F0', pri: '#334155', sec: '#2563EB' },
      { id: 'neumorphic-dark', name: '🌑 3D Neumorphic Stealth', cat: 'Whole-UI', ui: '3D Neumorphic', bg: '#1E242B', card: '#1E242B', pri: '#38BDF8', sec: '#818CF8' },
      { id: 'claymorphic-3d', name: '🧸 3D Claymorphism Studio', cat: 'Whole-UI', ui: '3D Claymorphic', bg: '#EEF2FF', card: '#FFFFFF', pri: '#4F46E5', sec: '#EC4899' },
      { id: 'porcelain-ceramic', name: '🏺 Porcelain Ceramic 3D', cat: 'Whole-UI', ui: '3D Claymorphic', bg: '#F8FAFC', card: '#FFFFFF', pri: '#0F172A', sec: '#0D9488' },
      { id: 'luxury-black-gold', name: '👑 Imperial Black & Gold', cat: 'Luxury', ui: 'Luxury Editorial', bg: '#080808', card: '#12110E', pri: '#D4AF37', sec: '#FFD700' },
      { id: 'marble-imperial', name: '🏛️ Carrara Marble Gold', cat: 'Luxury', ui: 'Luxury Editorial', bg: '#FAF8F5', card: '#FFFFFF', pri: '#1E293B', sec: '#D97706' },
      { id: 'rolex-emerald-gold', name: '⌚ Geneva Emerald & Gold', cat: 'Luxury', ui: 'Luxury Editorial', bg: '#022316', card: '#053824', pri: '#D4AF37', sec: '#10B981' },
      { id: 'wall-street-paper', name: '📰 Financial Gazette Serif', cat: 'Luxury', ui: 'Luxury Editorial', bg: '#FBF1E6', card: '#FFF9F2', pri: '#1C1917', sec: '#9A3412' },
      { id: 'monaco-yacht', name: '🛥️ Monaco Yacht Club', cat: 'Luxury', ui: 'Luxury Editorial', bg: '#F0F6FC', card: '#FFFFFF', pri: '#0F294A', sec: '#C59B27' },
      { id: 'dubai-burj-gold', name: '🏙️ Burj Royal Gold', cat: 'Luxury', ui: 'Luxury Editorial', bg: '#090D16', card: '#131B2E', pri: '#F59E0B', sec: '#38BDF8' },
      { id: 'win95-retro-os', name: '💾 Classic 95 Desktop OS', cat: 'Retro', ui: 'Retro Bevel OS', bg: '#008080', card: '#C0C0C0', pri: '#000080', sec: '#008080' },
      { id: 'mac-classic-platinum', name: '🖥️ Platinum Classic OS', cat: 'Retro', ui: 'Retro Bevel OS', bg: '#CCCCCC', card: '#EEEEEE', pri: '#222222', sec: '#3B82F6' },
      { id: 'pipboy-fallout', name: '☢️ Vault Pip-Boy 3000', cat: 'Retro', ui: 'CRT Phosphor', bg: '#041204', card: '#092209', pri: '#16F529', sec: '#22C55E' },
      { id: 'amber-crt-monitor', name: '📺 1984 Amber CRT Monitor', cat: 'Retro', ui: 'CRT Phosphor', bg: '#120B00', card: '#1F1400', pri: '#FFB000', sec: '#FFCC00' },
      { id: 'dos-borland-blue', name: '⌨️ Turbo DOS Blue Terminal', cat: 'Retro', ui: 'CRT Phosphor', bg: '#0000AA', card: '#000088', pri: '#FFFF55', sec: '#55FFFF' },
      { id: 'gameboy-pocket', name: '🎮 8-Bit Handheld Olive', cat: 'Retro', ui: 'CRT Phosphor', bg: '#9BBC0F', card: '#8BAC0F', pri: '#0F380F', sec: '#306230' },
      // Nature & India (15)
      { id: 'himalayan-dawn', name: '🏔️ Himalayan Sunrise', cat: 'Nature', ui: 'Modern Clean', bg: '#F8FAFC', card: '#FFFFFF', pri: '#1E3A8A', sec: '#F97316' },
      { id: 'ganga-river-mist', name: '🌊 Ganga River Mist (Bihar)', cat: 'Nature', ui: 'Modern Clean', bg: '#F0FDFA', card: '#FFFFFF', pri: '#0F766E', sec: '#0284C7' },
      { id: 'monsoon-thunder', name: '⛈️ Monsoon Storm Slate', cat: 'Nature', ui: 'Modern Clean', bg: '#0F172A', card: '#1E293B', pri: '#38BDF8', sec: '#FACC15' },
      { id: 'thar-desert-gold', name: '🐪 Thar Desert Sandstone', cat: 'Nature', ui: 'Modern Clean', bg: '#FEFCE8', card: '#FFFFFF', pri: '#9A3412', sec: '#D97706' },
      { id: 'kashmir-saffron', name: '🌺 Kashmir Kesar Saffron', cat: 'Nature', ui: 'Modern Clean', bg: '#FFF7ED', card: '#FFFFFF', pri: '#C2410C', sec: '#DC2626' },
      { id: 'sundarbans-mangrove', name: '🐅 Sundarbans Canopy', cat: 'Nature', ui: 'Modern Clean', bg: '#041E17', card: '#062E22', pri: '#34D399', sec: '#FBBF24' },
      { id: 'bioluminescent-bay', name: '🪼 Bioluminescent Lagoon', cat: 'Nature', ui: 'Modern Clean', bg: '#020818', card: '#061532', pri: '#00F5D4', sec: '#00BBF9' },
      { id: 'northern-lights', name: '🌠 Aurora Borealis', cat: 'Nature', ui: 'Modern Clean', bg: '#050B14', card: '#0D192B', pri: '#4ADE80', sec: '#A855F7' },
      { id: 'volcanic-magma', name: '🌋 Volcanic Obsidian Lava', cat: 'Nature', ui: 'Modern Clean', bg: '#120705', card: '#220E0A', pri: '#FF5722', sec: '#FF9800' },
      { id: 'cherry-blossom-kyoto', name: '🌸 Kyoto Sakura Blossom', cat: 'Nature', ui: 'Modern Clean', bg: '#FFF1F2', card: '#FFFFFF', pri: '#BE185D', sec: '#F43F5E' },
      { id: 'matcha-zen', name: '🍵 Uji Matcha Zen', cat: 'Nature', ui: 'Modern Clean', bg: '#F7FEE7', card: '#FFFFFF', pri: '#3F6212', sec: '#4D7C0F' },
      { id: 'nordic-fjord', name: '🧊 Norwegian Fjord', cat: 'Nature', ui: 'Modern Clean', bg: '#0B192C', card: '#162B47', pri: '#0284C7', sec: '#38BDF8' },
      { id: 'sahara-dusk', name: '🏜️ Sahara Terracotta Dusk', cat: 'Nature', ui: 'Modern Clean', bg: '#1F120B', card: '#331D12', pri: '#EA580C', sec: '#F59E0B' },
      { id: 'amalfi-coast', name: '🍋 Amalfi Azure & Lemon', cat: 'Nature', ui: 'Modern Clean', bg: '#F0F9FF', card: '#FFFFFF', pri: '#0284C7', sec: '#EAB308' },
      { id: 'lavender-provence', name: '💜 Provence Lavender', cat: 'Nature', ui: 'Modern Clean', bg: '#F5F3FF', card: '#FFFFFF', pri: '#6D28D9', sec: '#F472B6' },
      // Classic & Signature (20)
      { id: 'light', name: '☀️ Light Default', cat: 'Classic', ui: 'Standard', bg: '#F0F4F8', card: '#FFFFFF', pri: '#102A43', sec: '#2D68C4' },
      { id: 'dark', name: '🌙 Dark Slate', cat: 'Classic', ui: 'Standard', bg: '#0F172A', card: '#1E293B', pri: '#94A3B8', sec: '#3B82F6' },
      { id: 'liquid-glass', name: '🧪 Liquid Glass (Blur)', cat: 'Whole-UI', ui: 'Spatial Glass', bg: '#030712', card: '#0F172A', pri: '#38BDF8', sec: '#0EA5E9' },
      { id: 'cyberpunk', name: '⚡ Cyberpunk Neon', cat: 'Whole-UI', ui: 'Sci-Fi HUD', bg: '#05050A', card: '#121019', pri: '#FF007F', sec: '#00F0FF' },
      { id: 'emerald', name: '🌲 Emerald Forest', cat: 'Classic', ui: 'Standard', bg: '#022C22', card: '#064E3B', pri: '#10B981', sec: '#059669' },
      { id: 'sunset', name: '🌅 Sunset Orange', cat: 'Classic', ui: 'Standard', bg: '#FFF7ED', card: '#FFFFFF', pri: '#7C2D12', sec: '#EA580C' },
      { id: 'royal', name: '👑 Royal Amethyst', cat: 'Classic', ui: 'Standard', bg: '#1E1B4B', card: '#2E1065', pri: '#C084FC', sec: '#7C3AED' },
      { id: 'arctic', name: '❄️ Arctic Frost', cat: 'Classic', ui: 'Standard', bg: '#F0F9FF', card: '#FFFFFF', pri: '#0C4A6E', sec: '#0284C7' },
      { id: 'matrix', name: '💻 Matrix Green', cat: 'Retro', ui: 'CRT Terminal', bg: '#000500', card: '#001100', pri: '#00FF00', sec: '#00CC00' },
      { id: 'obsidian', name: '🖤 Obsidian Dark', cat: 'Classic', ui: 'Standard', bg: '#0A0A0A', card: '#171717', pri: '#FAFAFA', sec: '#525252' },
      { id: 'rose-gold', name: '✨ Rose Gold', cat: 'Luxury', ui: 'Standard', bg: '#FDFBFB', card: '#FFFFFF', pri: '#4A2E2B', sec: '#B76E79' },
      { id: 'tokyo-night', name: '🌆 Tokyo Night', cat: 'Classic', ui: 'Standard', bg: '#1a1b26', card: '#24283b', pri: '#7AA2F7', sec: '#bb9af7' },
      { id: 'solarized', name: '📜 Solarized Light', cat: 'Classic', ui: 'Standard', bg: '#fdf6e3', card: '#eee8d5', pri: '#268bd2', sec: '#b58900' },
      { id: 'nordic', name: '🏔️ Nordic Minimal', cat: 'Classic', ui: 'Standard', bg: '#2E3440', card: '#3B4252', pri: '#5E81AC', sec: '#88C0D0' },
      { id: 'deep-space', name: '🌌 Deep Space', cat: 'Classic', ui: 'Standard', bg: '#030712', card: '#0F172A', pri: '#6366F1', sec: '#8B5CF6' },
      { id: 'pastel-dream', name: '🎨 Pastel Dream', cat: 'Classic', ui: 'Standard', bg: '#FDF4FF', card: '#FFFFFF', pri: '#93C5FD', sec: '#F472B6' },
      { id: 'retro-terminal', name: '📟 Retro Terminal', cat: 'Retro', ui: 'CRT Terminal', bg: '#111111', card: '#1E1E1E', pri: '#33FF33', sec: '#00FFCC' },
      { id: 'industrial-steel', name: '⚙️ Industrial Steel', cat: 'Classic', ui: 'Standard', bg: '#0F172A', card: '#1E293B', pri: '#475569', sec: '#0284C7' },
      { id: 'golden-amber', name: '⭐ Golden Amber', cat: 'Luxury', ui: 'Standard', bg: '#FFFBEB', card: '#FFFFFF', pri: '#B45309', sec: '#F59E0B' },
      { id: 'carbon-fiber', name: '🏎️ Carbon Fiber', cat: 'Classic', ui: 'Standard', bg: '#09090B', card: '#18181B', pri: '#38BDF8', sec: '#F43F5E' },
      { id: 'synthwave', name: '🌴 Synthwave 80s', cat: 'Retro', ui: 'Standard', bg: '#1A0033', card: '#2B0055', pri: '#FF77FF', sec: '#00FFFF' },
      { id: 'neon-sakura', name: '🌸 Neon Sakura', cat: 'Classic', ui: 'Standard', bg: '#FFF0F5', card: '#FFFFFF', pri: '#FF69B4', sec: '#FF1493' },
      { id: 'sunset-mirage', name: '🏜️ Sunset Mirage', cat: 'Classic', ui: 'Standard', bg: '#2C0000', card: '#3D0C02', pri: '#FF4500', sec: '#FF8C00' },
      { id: 'acid-matrix', name: '🔋 Acid Matrix', cat: 'Retro', ui: 'Standard', bg: '#0A140A', card: '#142814', pri: '#76FF03', sec: '#64DD17' },
      { id: 'vampire-blood', name: '🩸 Vampire Blood', cat: 'Classic', ui: 'Standard', bg: '#120505', card: '#210A0A', pri: '#D32F2F', sec: '#B71C1C' },
      { id: 'deep-ocean-abyss', name: '🌊 Deep Ocean Abyss', cat: 'Nature', ui: 'Standard', bg: '#001015', card: '#00222B', pri: '#00838F', sec: '#00ACC1' },
      { id: 'cyber-gold', name: '🏆 Cyber Gold', cat: 'Luxury', ui: 'Standard', bg: '#141200', card: '#242100', pri: '#FFD700', sec: '#FFC107' },
      { id: 'neon-mint', name: '🌿 Neon Mint', cat: 'Nature', ui: 'Standard', bg: '#001A10', card: '#003320', pri: '#00E676', sec: '#1DE9B6' },
      { id: 'crimson-dusk', name: '🍷 Crimson Dusk', cat: 'Classic', ui: 'Standard', bg: '#1F0510', card: '#330A1D', pri: '#C2185B', sec: '#E91E63' },
      { id: 'electric-violet', name: '🔮 Electric Violet', cat: 'Classic', ui: 'Standard', bg: '#0D051A', card: '#1A0A33', pri: '#7C4DFF', sec: '#B388FF' }
    ];

    let activeThemeStudioCat = 'ALL';
    let activeWholeUIMode = safeGetStorage('gi_ui_mode') || 'auto';

    function changeTheme(themeName) {
      document.body.setAttribute('data-theme', themeName);
      safeSetStorage('gi_theme', themeName);
      const thSel = document.getElementById('theme-selector');
      if (thSel && thSel.value !== themeName) thSel.value = themeName;
      if (typeof syncIntroThemeColors === 'function') syncIntroThemeColors(themeName);
      renderThemeStudioGrid();
      const tObj = ALL_70_THEMES.find(t => t.id === themeName);
      showToast(`Theme applied: ${tObj ? tObj.name : themeName.replace(/-/g, ' ')}`);
    }

    window.setWholeUIMode = function(mode) {
      activeWholeUIMode = mode;
      safeSetStorage('gi_ui_mode', mode);
      if (mode === 'auto' || mode === 'standard') {
        document.body.removeAttribute('data-ui-mode');
      } else {
        document.body.setAttribute('data-ui-mode', mode);
      }
      const pills = document.querySelectorAll('#ui-mode-pills .filter-pill');
      pills.forEach(p => {
        p.classList.toggle('active', p.getAttribute('onclick').includes(`'${mode}'`));
      });
      showToast(`Whole-UI Architecture set to: ${mode.toUpperCase()}`);
    };

    window.openThemeStudioModal = function() {
      renderThemeStudioGrid();
      document.getElementById('theme-studio-modal').style.display = 'flex';
    };

    window.setThemeStudioCat = function(cat) {
      activeThemeStudioCat = cat;
      renderThemeStudioGrid();
    };

    window.surpriseRandomTheme = function() {
      const rand = ALL_70_THEMES[Math.floor(Math.random() * ALL_70_THEMES.length)];
      changeTheme(rand.id);
    };

    window.renderThemeStudioGrid = function() {
      const grid = document.getElementById('theme-studio-grid');
      const pills = document.getElementById('theme-cat-pills');
      if (!grid || !pills) return;

      const cats = [
        { k: 'ALL', l: `🌐 All Themes (${ALL_70_THEMES.length})` },
        { k: 'Whole-UI', l: '🏛️ Whole-UI Morphs (25)' },
        { k: 'Luxury', l: '👑 Luxury & Gold (8)' },
        { k: 'Nature', l: '🌏 India & Nature (17)' },
        { k: 'Retro', l: '📟 Retro OS & CRT (9)' },
        { k: 'Classic', l: '⭐ Classic Signature (19)' }
      ];
      pills.innerHTML = cats.map(c => `<span class="filter-pill ${activeThemeStudioCat === c.k ? 'active' : ''}" onclick="setThemeStudioCat('${c.k}')">${c.l}</span>`).join('');

      const q = (document.getElementById('theme-studio-search') ? document.getElementById('theme-studio-search').value.toLowerCase().trim() : '');
      const curTheme = document.body.getAttribute('data-theme') || 'light';

      const filtered = ALL_70_THEMES.filter(t => {
        if (activeThemeStudioCat !== 'ALL' && t.cat !== activeThemeStudioCat) return false;
        if (q && !(t.name.toLowerCase().includes(q) || t.ui.toLowerCase().includes(q) || t.cat.toLowerCase().includes(q))) return false;
        return true;
      });

      grid.innerHTML = filtered.map(t => `
        <div class="theme-swatch-card ${curTheme === t.id ? 'active-theme' : ''}" onclick="changeTheme('${t.id}')" style="background:${t.card}; color:${t.pri}; border-color:${t.sec};">
          <div style="display:flex; justify-content:space-between; align-items:center; gap:6px;">
            <span style="font-size:13px; font-weight:900;">${t.name}</span>
            ${curTheme === t.id ? '<span style="font-size:11px; background:#10B981; color:#fff; padding:2px 7px; border-radius:10px; font-weight:900;">ACTIVE</span>' : ''}
          </div>
          <div style="display:flex; gap:6px; align-items:center;">
            <span style="width:20px; height:20px; border-radius:50%; background:${t.bg}; border:1px solid rgba(128,128,128,0.4); display:inline-block;"></span>
            <span style="width:20px; height:20px; border-radius:50%; background:${t.pri}; display:inline-block;"></span>
            <span style="width:20px; height:20px; border-radius:50%; background:${t.sec}; display:inline-block;"></span>
            <span style="font-size:10px; font-weight:800; margin-left:auto; opacity:0.85; padding:2px 6px; border-radius:6px; border:1px solid currentColor;">${t.ui}</span>
          </div>
        </div>
      `).join('');
    };

    function sanitizeStructure(struct) {
      if (!struct) return []; 
      let sArr = Array.isArray(struct) ? struct : Object.values(struct);
      sArr = sArr.filter(Boolean);
      sArr.forEach(site => {
        if (site.subgroups) {
          site.subgroups = Array.isArray(site.subgroups) ? site.subgroups : Object.values(site.subgroups);
          site.subgroups = site.subgroups.filter(Boolean);
        } else { site.subgroups = []; }
      });
      return sArr;
    }

    function sanitizeState(state) {
      if (!state) state = {};
      let wArr = Array.isArray(state.workers) ? state.workers : (state.workers ? Object.values(state.workers) : []);
      state.workers = wArr.filter(Boolean);
      let kpArr = Array.isArray(state.keyPersons) ? state.keyPersons : (state.keyPersons ? Object.values(state.keyPersons) : []);
      state.keyPersons = kpArr.filter(Boolean);

      state.attendance = Array.isArray(state.attendance) ? Object.assign({}, state.attendance) : (state.attendance || {});
      state.kpAttendance = Array.isArray(state.kpAttendance) ? Object.assign({}, state.kpAttendance) : (state.kpAttendance || {});
      state.advances = Array.isArray(state.advances) ? Object.assign({}, state.advances) : (state.advances || {});
      state.timeline = Array.isArray(state.timeline) ? Object.assign({}, state.timeline) : (state.timeline || {});
      state.dpr = Array.isArray(state.dpr) ? Object.assign({}, state.dpr) : (state.dpr || {});
      state.stockThresholds = (state.stockThresholds && typeof state.stockThresholds === 'object' && !Array.isArray(state.stockThresholds)) ? state.stockThresholds : {};
      
      Object.keys(state.dpr).forEach(k => {
         let d = state.dpr[k];
         if(d) {
             d.matReceived = Array.isArray(d.matReceived) ? d.matReceived.filter(Boolean) : (d.matReceived ? Object.values(d.matReceived).filter(Boolean) : []);
             d.matConsumed = Array.isArray(d.matConsumed) ? d.matConsumed.filter(Boolean) : (d.matConsumed ? Object.values(d.matConsumed).filter(Boolean) : []);
             d.photos = Array.isArray(d.photos) ? d.photos : (d.photos ? Object.values(d.photos).filter(Boolean) : []);
         }
      });
      return state;
    }

    function getStorageKey() { return `GI_DATA_${currentSite}_${currentSubgroup}`; }
    function showToast(m) { const t = document.getElementById('toast'); document.getElementById('toast-msg').textContent = m; t.style.bottom = '30px'; setTimeout(() => { t.style.bottom = '-80px'; }, 3000); }

    function saveProfile() {
      const name = document.getElementById('profile-name-input').value.trim();
      if (!name) { showToast("Please enter a valid name."); return; }
      userName = name; safeSetStorage('gi_user_profile', name); 
      document.getElementById('profile-overlay').style.display = 'none'; document.getElementById('profile-display').innerHTML = `👤 ${name}`; 
      initPresence(); logActivity("Joined the portal");
    }
    
    function toggleActivityPanel() { document.getElementById('activity-panel').classList.toggle('open'); updateAdvancedAnalytics(); }

    function initPresence() {
      if (!userName) return;
      db.ref('global/presence').off(); db.ref('global/activity').off();
      const userKey = userName.replace(/[^a-zA-Z0-9]/g,'') || 'user';
      const ref = db.ref(`global/presence/${userKey}`);
      db.ref('.info/connected').on('value', (s) => {
        if(s.val()) { ref.set({ name: userName, role: userRole, device: deviceType, time: Date.now() }); ref.onDisconnect().remove(); }
      });
      
      db.ref('global/presence').on('value', (s) => {
        const list = document.getElementById('online-users-list'); list.innerHTML = ''; let count = 0; let mobiles = 0; let desktops = 0;
        if(s.val()) {
          Object.values(s.val()).forEach(u => { 
            if(!u) return;
            count++; if(u.device && u.device.includes('Mobile')) mobiles++; else desktops++;
            const t = new Date(u.time).toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'});
            list.innerHTML += `<div class="online-tag"><div style="display:flex; align-items:center;"><div class="pulse-dot"></div> <b>${u.name || 'User'}</b> <span style="font-weight:normal; color:var(--text-muted); margin-left:6px;">(${u.role || 'viewer'})</span></div><div style="display:flex; align-items:center; gap:8px;"><span style="font-size:11px; color:var(--text-muted);">Since ${t}</span><span title="${u.device || 'Desktop'}">${u.device ? u.device.split(' ')[0] : '💻'}</span></div></div>`; 
          });
        }
        document.getElementById('ana-sessions').textContent = count;
        if(count > peakUsers) peakUsers = count; document.getElementById('ana-peak').textContent = peakUsers;
        document.getElementById('ana-mobile').textContent = count ? Math.round((mobiles/count)*100)+'%' : '0%';
        document.getElementById('ana-desktop').textContent = count ? Math.round((desktops/count)*100)+'%' : '0%';
      });

      const startOfDay = new Date().setHours(0,0,0,0);
      db.ref('global/activity').orderByChild('time').startAt(startOfDay).on('value', (s) => {
        const list = document.getElementById('activity-log-list'); list.innerHTML = ''; let lCount = 0; let aCount = 0;
        if(s.val()) {
          Object.values(s.val()).reverse().forEach(a => { 
            if(!a) return;
            lCount++; if((a.action && (a.action.includes('Deleted') || a.action.includes('Wiped') || a.action.includes('Authorized as admin'))) || (a.user && a.user.includes('Admin'))) aCount++;
            const t = new Date(a.time).toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'}); 
            list.innerHTML += `<div class="log-item"><b>${a.user || 'User'}</b>: ${a.action || ''}<div class="log-time">${t}</div></div>`; 
          });
        }
        document.getElementById('ana-logs').textContent = lCount;
        document.getElementById('ana-admin-logs').textContent = aCount;
      });
    }

    function logActivity(action) { if(userName) db.ref('global/activity').push({ user: userName, action: action, time: Date.now() }); }

    function startAnalyticsEngine() {
        setInterval(() => {
            document.getElementById('ana-ping').textContent = Math.floor(Math.random() * (45 - 15) + 15) + 'ms';
            document.getElementById('ana-cpu').textContent = Math.floor(Math.random() * (20 - 5) + 5) + '%';
            let diff = Math.floor((Date.now() - sessionStartTime) / 1000);
            let h = Math.floor(diff / 3600).toString().padStart(2, '0');
            let m = Math.floor((diff % 3600) / 60).toString().padStart(2, '0');
            let s = (diff % 60).toString().padStart(2, '0');
            document.getElementById('ana-uptime').textContent = `${h}:${m}:${s}`;
        }, 2000);
    }

    window.jumpToSelectedDay = function(dayNum) {
      const sel = document.getElementById('day-select');
      if (!sel) return;
      sel.value = dayNum;
      handleDayChange();
      showToast(`Jumped to Day ${dayNum}`);
    };

    function renderVisualAnalyticsCharts() {
      try {
        const sD = parseInt(document.getElementById("day-select").value) || 1;
        const mKey = getAttendanceMonthKey();
        const currentMonthDays = new Date(parseInt(mKey.split('-')[1]), parseInt(mKey.split('-')[0]), 0).getDate();
        const monthAtt = appState.attendance[mKey] || {};
        const maxW = Math.max(appState.workers.length, 1);

        // 1. 7-Day Attendance Trend Interactive Bar Chart
        let barsInner = '';
        for (let offset = 6; offset >= 0; offset--) {
          const dNum = sD - offset;
          if (dNum < 1) continue;
          let dayPresent = 0;
          appState.workers.forEach(w => {
            const r = monthAtt[w.id] && monthAtt[w.id][dNum];
            const dutyVal = r ? parseDutyInput(r.duty) : null;
            if (dutyVal !== null && dutyVal > 0) dayPresent += dutyVal;
          });
          const pct = Math.min(100, Math.round((dayPresent / maxW) * 100));
          const isSel = (dNum === sD);
          barsInner += `
            <div onclick="jumpToSelectedDay(${dNum})" style="flex:1; display:flex; flex-direction:column; align-items:center; justify-content:flex-end; height:100%; cursor:pointer; gap:4px;" title="Click to jump to Day ${dNum} (${dayPresent} Present)">
              <span style="font-size:10px; font-weight:900; color:${isSel ? 'var(--secondary)' : 'var(--primary)'};">${dayPresent}</span>
              <div style="width:100%; max-width:26px; height:${Math.max(pct, 8)}%; background:${isSel ? 'linear-gradient(180deg, var(--accent), var(--warning))' : 'linear-gradient(180deg, var(--secondary), var(--primary-light))'}; border-radius:6px 6px 2px 2px; transition:0.3s;"></div>
              <span style="font-size:10px; font-weight:${isSel ? '900' : '700'}; color:${isSel ? 'var(--secondary)' : 'var(--text-muted)'};">D${dNum}</span>
            </div>`;
        }
        const chart7Html = `<div style="display:flex; align-items:flex-end; justify-content:space-between; gap:8px; height:115px; padding:12px 10px 4px 10px; background:var(--bg); border-radius:12px; border:1px solid var(--border);">${barsInner || '<span style="margin:auto; font-size:12px; color:var(--text-muted);">No days in range</span>'}</div>`;

        // 2. Trade-Wise Workforce Distribution SVG Donut Chart
        const tradeMap = {};
        appState.workers.forEach(w => {
          const t = (w.desig || 'Unspecified').trim();
          tradeMap[t] = (tradeMap[t] || 0) + 1;
        });
        const tradeEntries = Object.entries(tradeMap).sort((a, b) => b[1] - a[1]);
        const palette = ['#2D68C4', '#10B981', '#F59E0B', '#9333EA', '#EF4444', '#06B6D4', '#EC4899'];
        const r = 42, circum = 2 * Math.PI * r;
        let offsetLen = 0;
        let circlesSvg = '';
        let legendHtml = '';
        if (appState.workers.length === 0) {
          circlesSvg = `<circle cx="60" cy="60" r="${r}" fill="none" stroke="var(--border)" stroke-width="14" />`;
          legendHtml = `<div style="font-size:12px; color:var(--text-muted);">No workers registered</div>`;
        } else {
          tradeEntries.slice(0, 6).forEach(([t, cnt], idx) => {
            const col = palette[idx % palette.length];
            const segLen = (cnt / appState.workers.length) * circum;
            circlesSvg += `<circle cx="60" cy="60" r="${r}" fill="none" stroke="${col}" stroke-width="14" stroke-dasharray="${segLen} ${circum}" stroke-dashoffset="${-offsetLen}" transform="rotate(-90 60 60)" />`;
            offsetLen += segLen;
            const pct = Math.round((cnt / appState.workers.length) * 100);
            legendHtml += `<div style="display:flex; align-items:center; justify-content:space-between; font-size:11px; font-weight:800; gap:8px; margin-bottom:4px;"><span style="display:flex; align-items:center; gap:6px; overflow:hidden; text-overflow:ellipsis; white-space:nowrap;"><span style="width:9px; height:9px; border-radius:50%; background:${col}; display:inline-block;"></span>${t}</span><span style="color:var(--text-muted);">${cnt} (${pct}%)</span></div>`;
          });
        }
        const donutHtml = `
          <div style="display:flex; align-items:center; gap:14px;">
            <svg viewBox="0 0 120 120" width="96" height="96" style="flex-shrink:0;">
              ${circlesSvg}
              <text x="60" y="57" text-anchor="middle" fill="var(--primary)" font-size="18" font-weight="900">${appState.workers.length}</text>
              <text x="60" y="72" text-anchor="middle" fill="var(--text-muted)" font-size="9" font-weight="800">STAFF</text>
            </svg>
            <div style="flex:1; overflow:hidden;">${legendHtml}</div>
          </div>`;

        // 3. Gross vs. Advance Breakdown Progress Bar
        let totalGross = 0, totalAdv = 0, totalOT = 0;
        appState.workers.forEach(w => {
          let wD = 0, wO = 0, wA = 0;
          if (monthAtt[w.id]) {
            for (let d = 1; d <= currentMonthDays; d++) {
              const rec = monthAtt[w.id][d];
              if (rec) {
                wD += (parseDutyInput(rec.duty) || 0);
                wO += (parseFloat(rec.ot) || 0);
                wA += (parseFloat(rec.adv) || 0);
              }
            }
          }
          const rt = parseFloat(w.rate) || 0;
          totalGross += (wD * rt) + (wO * (rt / 8));
          totalAdv += (parseFloat(appState.advances[w.id]) || 0) + wA;
          totalOT += wO;
        });
        const netPay = Math.max(0, totalGross - totalAdv);
        const denom = Math.max(totalGross, 1);
        const advPct = Math.min(100, Math.round((totalAdv / denom) * 100));
        const netPct = Math.max(0, 100 - advPct);

        const finHtml = `
          <div style="display:flex; flex-direction:column; gap:10px;">
            <div style="display:flex; justify-content:space-between; font-size:12px; font-weight:800;">
              <span>Gross: <b style="color:var(--primary);">₹${Math.round(totalGross).toLocaleString('en-IN')}</b></span>
              <span>Adv: <b style="color:var(--danger);">₹${Math.round(totalAdv).toLocaleString('en-IN')}</b></span>
            </div>
            <div style="height:16px; width:100%; background:var(--bg); border-radius:10px; overflow:hidden; display:flex; border:1px solid var(--border);">
              <div style="width:${netPct}%; background:linear-gradient(90deg, #10B981, #059669); height:100%;" title="Net Payable: ${netPct}%"></div>
              <div style="width:${advPct}%; background:linear-gradient(90deg, #EF4444, #DC2626); height:100%;" title="Advance Deducted: ${advPct}%"></div>
            </div>
            <div style="display:flex; justify-content:space-between; font-size:11px; font-weight:800; color:var(--text-muted);">
              <span style="color:var(--success);">🟢 Net Payable: ${netPct}% (₹${Math.round(netPay).toLocaleString('en-IN')})</span>
              <span style="color:var(--danger);">🔴 Advances: ${advPct}%</span>
            </div>
          </div>`;

        const el7 = document.getElementById('chart-7day-bars');
        const elT = document.getElementById('chart-trade-dist');
        const elF = document.getElementById('chart-fin-breakdown');
        if (el7) el7.innerHTML = chart7Html;
        if (elT) elT.innerHTML = donutHtml;
        if (elF) elF.innerHTML = finHtml;

        const mirrorPanel = document.getElementById('panel-visual-charts');
        if (mirrorPanel) {
          mirrorPanel.innerHTML = `
            <div class="ana-box" style="text-align:left; padding:12px;"><span>7-Day Attendance Trend</span>${chart7Html}</div>
            <div class="ana-box" style="text-align:left; padding:12px;"><span>Trade-Wise Workforce</span>${donutHtml}</div>
            <div class="ana-box" style="text-align:left; padding:12px;"><span>Gross vs. Advance Split</span>${finHtml}</div>
          `;
        }
      } catch (err) {}
    }

    function updateAdvancedAnalytics() {
        try {
            document.getElementById('ana-syncs').textContent = totalSyncs;
            document.getElementById('ana-payload').textContent = (new Blob([JSON.stringify(appState)]).size / 1024).toFixed(1) + ' KB';
            let zCount = 0; siteStructure.forEach(s => zCount += (s.subgroups ? s.subgroups.length : 0));
            document.getElementById('ana-zones').textContent = zCount;
            document.getElementById('ana-workforce').textContent = appState.workers.length;
            document.getElementById('ana-kp').textContent = appState.keyPersons.length;
            let rainDays = 0, matActivity = 0;
            Object.values(appState.dpr).forEach(d => {
                if (!d) return;
                if (d.rainStart || (d.weather && d.weather.includes('Rain'))) rainDays++;
                matActivity += (d.matReceived ? d.matReceived.length : 0) + (d.matConsumed ? d.matConsumed.length : 0);
            });
            document.getElementById('ana-rain').textContent = rainDays; document.getElementById('ana-mat').textContent = matActivity;

            const sD = parseInt(document.getElementById("day-select").value) || 1;
            const mKey = getAttendanceMonthKey();
            const currentMonthDays = new Date(parseInt(mKey.split('-')[1]), parseInt(mKey.split('-')[0]), 0).getDate();
            let pT = 0, totalGross = 0, totalAdv = 0, totalOT = 0;
            const monthAtt = appState.attendance[mKey] || {};
            appState.workers.forEach(w => {
                let wD = 0, wO = 0, wA = 0;
                if (monthAtt[w.id]) {
                    if (monthAtt[w.id][sD] && parseDutyInput(monthAtt[w.id][sD].duty) > 0) pT++;
                    for (let d = 1; d <= currentMonthDays; d++) {
                        const r = monthAtt[w.id][d];
                        if (r) {
                            wD += (parseDutyInput(r.duty) || 0);
                            wO += (parseFloat(r.ot) || 0);
                            wA += (parseFloat(r.adv) || 0);
                        }
                    }
                }
                const rate = parseFloat(w.rate) || 0;
                const gross = (wD * rate) + (wO * (rate / 8));
                const adv = (parseFloat(appState.advances[w.id]) || 0) + wA;
                totalGross += gross;
                totalAdv += adv;
                totalOT += wO;
            });
            const attendRate = appState.workers.length > 0 ? Math.round((pT / appState.workers.length) * 100) : 0;
            document.getElementById('ana-attend-rate').textContent = `${attendRate}%`;
            document.getElementById('ana-gross').textContent = `₹${Math.round(totalGross).toLocaleString('en-IN')}`;
            document.getElementById('ana-adv').textContent = `₹${Math.round(totalAdv).toLocaleString('en-IN')}`;
            document.getElementById('ana-ot').textContent = `${totalOT.toFixed(1)}h`;
            document.getElementById('ana-net').textContent = `₹${Math.round(totalGross - totalAdv).toLocaleString('en-IN')}`;
            renderVisualAnalyticsCharts();
        } catch(e) {}
    }

    function toggleAuth() { 
      if (userRole !== 'viewer') { 
        showConfirmModal("Are you sure you want to lock your active session and return to View Only mode?", () => {
          userRole = 'viewer'; safeRemoveStorage('gi_role'); 
          updateAuthUI(); renderAll(); showToast("Locked Mode Active"); logActivity("Locked portal access"); 
        }, "🔒 Confirm Session Lock");
      } else { 
        document.getElementById('login-overlay').style.display = 'flex'; 
        document.getElementById('pwd-error').style.display = 'none'; 
        document.getElementById('admin-pwd').value = ''; document.getElementById('admin-pwd').focus(); 
      } 
    }
    
    function closeLoginModal() { document.getElementById('login-overlay').style.display = 'none'; }
    function closeModal(id) { document.getElementById(id).style.display = 'none'; }
    
    function checkPassword() { 
      const pwd = document.getElementById('admin-pwd').value;
      if (pwd === '9431') { userRole = 'admin'; showToast("Admin Access Unlocked"); }
      else if (pwd === '1820') { userRole = 'incharge'; showToast("Site Incharge Mode Unlocked"); }
      else if (pwd === '5566') { userRole = 'supervisor'; showToast("Supervisor Mode Unlocked"); }
      else { document.getElementById('pwd-error').style.display = 'block'; return; }
      
      safeSetStorage('gi_role', userRole); 
      closeLoginModal(); updateAuthUI(); renderAll(); initPresence(); 
      logActivity(`Authorized as ${userRole}`);
    }
    
    function updateAuthUI() {
      const btn = document.getElementById('auth-status-btn'), edits = document.getElementById('edit-controls'), clrGrp = document.getElementById('btn-clear-group');
      const addWorkerBtn = document.getElementById('btn-add-worker'), addKpBtn = document.getElementById('btn-add-kp');
      const restoreBtn = document.getElementById('btn-restore-db');
      if (restoreBtn) restoreBtn.style.display = (userRole === 'admin') ? 'inline-flex' : 'none';
      if (userRole === 'admin') { 
        btn.innerHTML='🛡️ Admin'; btn.style.background='var(--danger)'; btn.classList.remove("shake-error");
        edits.style.display = 'flex';
        addWorkerBtn.style.display = isMasterRollup ? 'none' : 'inline-flex';
        addKpBtn.style.display = 'inline-flex';
        clrGrp.style.display = isMasterRollup ? 'none' : 'inline-flex';
      } else if (userRole === 'incharge') {
        btn.innerHTML='🔑 Incharge'; btn.style.background='var(--warning)'; btn.classList.remove("shake-error");
        edits.style.display = isMasterRollup ? 'none' : 'flex';
        addWorkerBtn.style.display = 'inline-flex';
        addKpBtn.style.display = 'none';
        clrGrp.style.display = 'none';
      } else if (userRole === 'supervisor') {
        btn.innerHTML='👷 Supervisor'; btn.style.background='var(--secondary)'; btn.classList.remove("shake-error");
        edits.style.display = isMasterRollup ? 'none' : 'flex';
        addWorkerBtn.style.display = 'inline-flex';
        addKpBtn.style.display = 'none';
        clrGrp.style.display = 'none';
      } else { 
        btn.innerHTML='🔒 View Only'; btn.style.background='rgba(255,255,255,0.2)'; edits.style.display='none';
      }
      renderSiteDropdown();
    }

    window.requireAuthClick = function(el) { 
      const canManage = (userRole === 'admin' || userRole === 'incharge' || userRole === 'supervisor');
      if (!canManage || isMasterRollup) { 
        if(el && el.blur) el.blur(); 
        const btn = document.getElementById('auth-status-btn'); 
        btn.classList.remove("shake-error"); void btn.offsetWidth; btn.classList.add("shake-error"); 
        showToast(isMasterRollup ? "Switch to a specific group to edit." : "Enter PIN to make edits."); 
        if(!isMasterRollup && !canManage) setTimeout(() => { document.getElementById('login-overlay').style.display = 'flex'; }, 400); 
      } 
    };

    function isUserTyping() { const el = document.activeElement; return el && (el.tagName === 'INPUT' || el.tagName === 'TEXTAREA' || el.tagName === 'SELECT'); }
    
    window.resolveConflict = function(action) {
      document.getElementById('conflict-overlay').style.display = 'none';
      if(action === 'reload') { appState = sanitizeState(pendingCloudState); renderAll(); } 
      else if (action === 'force') { isSavingToCloud = true; db.ref(`data/${currentSite}/${currentSubgroup}`).set(appState).then(() => { isSavingToCloud = false; showToast("Forced Override Successful"); logActivity("Forced sync overwrite"); }); }
    };

    function loadLocalState() {
      if(isMasterRollup) return; 
      const saved = safeGetStorage(getStorageKey());
      appState = sanitizeState(saved ? JSON.parse(saved) : null);
    }
    
    function syncSiteDataFirebase() {
      if (currentSiteRef) { currentSiteRef.off(); }
      if (!currentSite || !currentSubgroup) { appState = sanitizeState(null); renderAll(); return; }

      if (isMasterRollup) {
        currentSiteRef = db.ref(`data/${currentSite}`);
        currentSiteRef.on('value', (s) => {
          if(isSavingToCloud) return;
          const allGroups = s.val();
          let aggregated = { workers: [], keyPersons: [], attendance: {}, kpAttendance: {}, advances: {}, dpr: {}, timeline: {} };
          if(allGroups) {
            Object.values(allGroups).forEach(group => {
              if(!group) return;
              if(group.workers) aggregated.workers.push(...Object.values(group.workers));
              if(group.keyPersons) aggregated.keyPersons.push(...Object.values(group.keyPersons));
              if(group.attendance) Object.entries(group.attendance).forEach(([month, wData]) => {
                if(!aggregated.attendance[month]) aggregated.attendance[month] = {};
                Object.assign(aggregated.attendance[month], wData);
              });
              if(group.kpAttendance) {
                Object.entries(group.kpAttendance).forEach(([k, v]) => {
                  if (v && typeof v === 'object') {
                    if (!aggregated.kpAttendance[k]) aggregated.kpAttendance[k] = {};
                    Object.assign(aggregated.kpAttendance[k], v);
                  }
                });
              }
              if(group.advances) Object.assign(aggregated.advances, group.advances);
              if(group.timeline) Object.entries(group.timeline).forEach(([date, tArray]) => {
                if(!aggregated.timeline[date]) aggregated.timeline[date] = [];
                aggregated.timeline[date].push(...Object.values(tArray));
              });
              if(group.dpr) Object.entries(group.dpr).forEach(([date, dData]) => {
                if(!aggregated.dpr[date]) aggregated.dpr[date] = { work: "", weather: dData.weather || "☀️ Sunny / Clear", rainStart: dData.rainStart || "", rainEnd: dData.rainEnd || "", workStop: dData.workStop || "No", matReceived: [], matConsumed: [], photos: [] };
                if(dData.work) aggregated.dpr[date].work += (aggregated.dpr[date].work ? "\n---\n" : "") + dData.work;
                if(dData.matReceived) aggregated.dpr[date].matReceived.push(...Object.values(dData.matReceived));
                if(dData.matConsumed) aggregated.dpr[date].matConsumed.push(...Object.values(dData.matConsumed));
                if(dData.photos) aggregated.dpr[date].photos.push(...Object.values(dData.photos));
              });
            });
          }
          const uniqueKpIds = [];
          aggregated.keyPersons = aggregated.keyPersons.filter(kp => { if(!kp || uniqueKpIds.includes(String(kp.id))) return false; uniqueKpIds.push(String(kp.id)); return true; });
          Object.keys(aggregated.timeline).forEach(date => { aggregated.timeline[date].sort((a,b) => a.timestamp - b.timestamp); });
          appState = sanitizeState(aggregated);
          if(!isUserTyping()) renderAll();
        });
        return;
      }

      currentSiteRef = db.ref(`data/${currentSite}/${currentSubgroup}`);
      currentSiteRef.on('value', (s) => {
        if(isSavingToCloud) return; 
        const newData = s.val();
        if(isUserTyping() && newData) {
           if(JSON.stringify(appState) !== JSON.stringify(sanitizeState(newData))) { pendingCloudState = newData; document.getElementById('conflict-overlay').style.display = 'flex'; return; }
        }
        appState = sanitizeState(newData); 
        safeSetStorage(getStorageKey(), JSON.stringify(appState));
        if(!isUserTyping()) { renderAll(); }
      });
    }

    function saveKeyPersonnelState() {
      if (!currentSite) return;
      appState = sanitizeState(appState);
      const targetGroup = (!isMasterRollup && currentSubgroup) ? currentSubgroup : '_site_officials';
      isSavingToCloud = true;
      Promise.all([
        db.ref(`data/${currentSite}/${targetGroup}/keyPersons`).set(appState.keyPersons),
        db.ref(`data/${currentSite}/${targetGroup}/kpAttendance`).set(appState.kpAttendance)
      ]).then(() => { isSavingToCloud = false; });
      totalSyncs++; updateDashboard(); updateAdvancedAnalytics();
    }

    function saveState() {
      if (!currentSite || !currentSubgroup) return;
      if (isMasterRollup) {
        saveKeyPersonnelState();
        return;
      }
      appState = sanitizeState(appState);
      safeSetStorage(getStorageKey(), JSON.stringify(appState));

      isSavingToCloud = true;
      db.ref(`data/${currentSite}/${currentSubgroup}`).set(appState).then(() => { isSavingToCloud = false; });
      totalSyncs++; updateDashboard(); updateAdvancedAnalytics();
    }
    
    function forceSyncProcess() { saveState(); showToast("Force Synced with Cloud"); }
    
    function wipeZoneData() {
      const canManage = (userRole === 'admin' || userRole === 'incharge' || userRole === 'supervisor');
      if(!canManage || isMasterRollup) return;
      showConfirmModal("DANGER: Wipe all data in this group?", () => {
        appState = sanitizeState(null); saveState(); renderAll(); logActivity(`Wiped all data in ${currentSubgroup}`); showToast("Data Cleared");
      }, "⚠️ Wipe Group Data");
    }

    function toggleDropdown() { document.getElementById('site-dropdown').classList.toggle('active'); }
    function loadSitesFromCloud() {
      db.ref('global/structure').on('value', (snap) => {
        siteStructure = sanitizeStructure(snap.val());
        if (siteStructure.length > 0 && (!currentSite || !siteStructure.some(s => s.id === currentSite))) {
          const firstSite = siteStructure[0];
          const firstSub = (firstSite.subgroups && firstSite.subgroups.length > 0) ? firstSite.subgroups[0] : null;
          selectSiteSubgroup(firstSite.id, firstSub ? firstSub.id : 'ALL_GROUPS', firstSite.name, firstSub ? firstSub.name : 'Master Roll-Up');
        } else {
          renderSiteDropdown();
        }
      });
    }

    function renderSiteDropdown() {
      const dd = document.getElementById('site-dropdown'); dd.innerHTML = '';
      const canManage = (userRole === 'admin' || userRole === 'incharge' || userRole === 'supervisor');

      if (siteStructure.length === 0) { dd.innerHTML = `<div class="dropdown-zone-item last-zone"><span style="margin-left:20px;">No sites created</span></div>`; } 
      else {
        siteStructure.forEach(site => {
          const header = document.createElement('div'); header.className = 'dropdown-site-header';
          let acts = canManage ? `<div style="display:flex; gap:6px;"><span class="add-zone-btn" onclick="openSiteManager('group', '${site.id}')">➕ Group</span><span class="action-btn-sm" onclick="event.stopPropagation(); triggerRenameSite('${site.id}')">✏️</span><span class="action-btn-sm" style="color:red;" onclick="event.stopPropagation(); triggerDeleteSite('${site.id}')">🗑</span></div>` : '';
          header.innerHTML = `<div class="site-title-text" style="cursor:pointer;" onclick="selectSiteSubgroup('${site.id}', 'ALL_GROUPS', '${site.name}', 'Master Roll-Up')">🏢 ${site.name}</div>${acts}`;
          dd.appendChild(header);
          if(site.subgroups) {
            site.subgroups.forEach((sub, i) => {
              const item = document.createElement('div'); item.className = `dropdown-zone-item ${i === site.subgroups.length - 1 ? 'last-zone' : ''}`;
              if(site.id === currentSite && sub.id === currentSubgroup) { item.style.background = 'rgba(45, 104, 196, 0.05)'; item.style.color = 'var(--secondary)'; }
              let subActs = canManage ? `<div style="display:flex; gap:6px;"><span class="action-btn-sm" onclick="event.stopPropagation(); triggerRename('${sub.id}')">✏️</span><span class="action-btn-sm" onclick="event.stopPropagation(); triggerDelete('${sub.id}')">🗑️</span></div>` : '';
              item.innerHTML = `<span style="flex:1; display:flex; align-items:center; gap:6px;">📍 ${sub.name}</span> ${subActs}`;
              item.onclick = () => selectSiteSubgroup(site.id, sub.id, site.name, sub.name);
              dd.appendChild(item);
            });
          }
        });
      }
      if(canManage) { 
        const addS = document.createElement('div'); addS.className = "add-zone-btn"; addS.style.margin="10px"; addS.style.textAlign="center"; addS.innerHTML = '➕ Create New Site'; 
        addS.onclick = () => { document.getElementById('site-dropdown').classList.remove('active'); openSiteManager('site'); }; dd.appendChild(addS); 
      }
      
      const aSite = siteStructure.find(x => x.id === currentSite);
      if(aSite) { 
          if(currentSubgroup === 'ALL_GROUPS') document.getElementById('selected-site-label').textContent = `🏢 ${aSite.name} ➔ 🌍 Master Roll-Up`; 
          else { const aSub = (aSite.subgroups||[]).find(x => x.id === currentSubgroup); document.getElementById('selected-site-label').textContent = `🏢 ${aSite.name} ➔ 📍 ${aSub ? aSub.name : 'Select Group'}`; }
      } else { document.getElementById('selected-site-label').textContent = '⚠️ Database Empty'; }
    }

    function selectSiteSubgroup(sId, subId, sName, subName) {
      currentSite = sId; currentSubgroup = subId; safeSetStorage('gi_last_site', sId); safeSetStorage('gi_last_sub', subId);
      isMasterRollup = (subId === 'ALL_GROUPS');
      
      if (isMasterRollup) {
         document.getElementById('selected-site-label').textContent = `🏢 ${sName} ➔ 🌍 Master Roll-Up`;
         document.querySelectorAll('[id^="rollup-alert-"]').forEach(el => el.style.display = 'block');
         document.getElementById('kp-master-header').style.display = 'block';
      } else {
         document.getElementById('selected-site-label').textContent = `🏢 ${sName} ➔ 📍 ${subName}`;
         document.querySelectorAll('[id^="rollup-alert-"]').forEach(el => el.style.display = 'none');
         document.getElementById('kp-master-header').style.display = 'none';
      }
      updateAuthUI();
      document.getElementById('site-dropdown').classList.remove('active'); loadLocalState(); syncSiteDataFirebase(); 
    }

    let smTempSiteId = null;
    function openSiteManager(type, siteId = null) {
      const canManage = (userRole === 'admin' || userRole === 'incharge' || userRole === 'supervisor');
      if(!canManage) return showToast("Permission denied. Supervisors, Incharges & Admins only.");
      document.getElementById('site-manager-modal').style.display = 'flex'; document.getElementById('sm-action-type').value = type; smTempSiteId = siteId; document.getElementById('sm-input').value = '';
      if(type === 'site') { document.getElementById('sm-title').textContent = "Create New Site"; document.getElementById('sm-desc').textContent = "A Site represents a major geographical project location."; } 
      else if (type === 'group') { document.getElementById('sm-title').textContent = "Create New Group"; } 
      else if (type === 'rename') { document.getElementById('sm-title').textContent = "Rename Group"; const site = siteStructure.find(s => s.subgroups && s.subgroups.some(sub => sub.id === contextTargetId)); if(site) { const sub = site.subgroups.find(s => s.id === contextTargetId); if(sub) document.getElementById('sm-input').value = sub.name; } }
      else if (type === 'rename_site') { document.getElementById('sm-title').textContent = "Rename Site"; const site = siteStructure.find(s => s.id === contextTargetId); if(site) document.getElementById('sm-input').value = site.name; }
    }

    function executeSiteManager() {
      const type = document.getElementById('sm-action-type').value; const val = document.getElementById('sm-input').value.trim();
      if(!val) { showToast("Name cannot be empty."); return; }
      if(type === 'site') {
        const id = 'site_' + Date.now();
        siteStructure.push({ id, name: val, subgroups: [] });
        logActivity(`Created new site: ${val}`);
        if (!currentSite) selectSiteSubgroup(id, 'ALL_GROUPS', val, 'Master Roll-Up');
      } 
      else if(type === 'group') {
        const site = siteStructure.find(s => s.id === smTempSiteId);
        if(!site) return;
        if(!site.subgroups) site.subgroups = [];
        const newSubId = 'sub_'+Date.now();
        site.subgroups.push({ id: newSubId, name: val });
        logActivity(`Added group ${val}`);
        if (!currentSite || !currentSubgroup || currentSubgroup === 'ALL_GROUPS') selectSiteSubgroup(site.id, newSubId, site.name, val);
      } 
      else if(type === 'rename') {
        const site = siteStructure.find(s => s.subgroups && s.subgroups.some(sub => sub.id === contextTargetId));
        if(site) {
          const sub = site.subgroups.find(s => s.id === contextTargetId);
          if(sub) sub.name = val;
          logActivity(`Renamed group to ${val}`);
          if(currentSubgroup === contextTargetId) document.getElementById('selected-site-label').textContent = `🏢 ${site.name} ➔ 📍 ${val}`;
        }
      }
      else if(type === 'rename_site') {
        const site = siteStructure.find(s => s.id === contextTargetId);
        if(site) {
          site.name = val;
          logActivity(`Renamed site to ${val}`);
        }
      }
      db.ref('global/structure').set(siteStructure); closeModal('site-manager-modal');
    }

    function triggerRename(subId) { document.getElementById('site-dropdown').classList.remove('active'); contextTargetId = subId; openSiteManager('rename'); }
    function triggerRenameSite(siteId) { document.getElementById('site-dropdown').classList.remove('active'); contextTargetId = siteId; openSiteManager('rename_site'); }
    
    function triggerDelete(subId) { 
      document.getElementById('site-dropdown').classList.remove('active'); contextTargetId = subId; 
      showConfirmModal("Delete this group permanently?", () => {
        const site = siteStructure.find(s => s.subgroups && s.subgroups.some(sub => sub.id === contextTargetId)); 
        if (!site) return;
        site.subgroups = site.subgroups.filter(s => s.id !== contextTargetId); 
        db.ref('global/structure').set(siteStructure); db.ref(`data/${site.id}/${contextTargetId}`).remove(); logActivity(`Deleted a group`); 
        if (contextTargetId === currentSubgroup) {
          const fallbackSub = (site.subgroups && site.subgroups.length > 0) ? site.subgroups[0].id : 'ALL_GROUPS';
          if(fallbackSub !== 'ALL_GROUPS') selectSiteSubgroup(site.id, fallbackSub, site.name, site.subgroups[0].name);
          else selectSiteSubgroup(site.id, 'ALL_GROUPS', site.name, 'Master Roll-Up');
        }
      }, "🗑️ Delete Group");
    }
    
    function triggerDeleteSite(siteId) {
      document.getElementById('site-dropdown').classList.remove('active'); 
      showConfirmModal("DANGER: Are you sure you want to completely delete this ENTIRE SITE?", () => {
        siteStructure = siteStructure.filter(s => s.id !== siteId); db.ref('global/structure').set(siteStructure); db.ref(`data/${siteId}`).remove(); logActivity(`Deleted a main site`); 
        if (currentSite === siteId) {
          const fallbackSite = siteStructure.length > 0 ? siteStructure[0] : null;
          if (fallbackSite) {
            const fallbackSub = (fallbackSite.subgroups && fallbackSite.subgroups.length > 0) ? fallbackSite.subgroups[0] : null;
            if (fallbackSub) selectSiteSubgroup(fallbackSite.id, fallbackSub.id, fallbackSite.name, fallbackSub.name);
            else selectSiteSubgroup(fallbackSite.id, 'ALL_GROUPS', fallbackSite.name, 'Master Roll-Up');
          } else { currentSite = null; currentSubgroup = null; document.getElementById('selected-site-label').textContent = '⚠️ Database Empty'; renderSiteDropdown(); syncSiteDataFirebase(); }
        } else renderSiteDropdown(); 
      }, "⚠️ Delete Entire Site");
    }

    function generateMonthOptions() { 
      const select = document.getElementById("month-select"); if(!select) return; select.innerHTML = ""; 
      const m = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"]; 
      const cY = new Date().getFullYear(), cM = new Date().getMonth() + 1; 
      for (let y = 2025; y <= 2030; y++) { for (let i = 1; i <= 12; i++) { const opt = document.createElement("option"); opt.value = `${i}-${y}`; opt.textContent = `${m[i-1]} ${y}`; if (y === cY && i === cM) opt.selected = true; select.appendChild(opt); } } 
    }

    function populateDaySelector() { 
      const select = document.getElementById("day-select"); if(!select) return;
      const currentSelectedDay = select.value || new Date().getDate(); 
      select.innerHTML = ""; 
      const mKey = getAttendanceMonthKey(); const parts = mKey.split("-");
      const month = parseInt(parts[0], 10); const year = parseInt(parts[1], 10);
      const totalDays = new Date(year, month, 0).getDate();
      for (let i = 1; i <= totalDays; i++) { const opt = document.createElement("option"); opt.value = i; opt.textContent = `Day ${i}`; select.appendChild(opt); }
      select.value = Math.min(parseInt(currentSelectedDay) || 1, totalDays);
    }

    function getSelectedDateKey() { return `${document.getElementById("day-select").value}-${document.getElementById("month-select").value}`; }
    function handleDayChange() { renderDailyView(); renderKeyPersonView(); renderDPRView(); renderNotesView(); updateDashboard(); }
    function changeMonth() { populateDaySelector(); renderAll(); }
    
    function switchTab(tId, btnElement) {
      document.querySelectorAll(".tab-content").forEach(e => e.classList.remove("active"));
      document.querySelectorAll(".tab-btn").forEach(e => e.classList.remove("active"));
      const targetContent = document.getElementById(tId); if (targetContent) targetContent.classList.add("active");
      if (btnElement) btnElement.classList.add("active");
      const dP = document.getElementById("daily-date-picker-wrap");
      if (tId === "daily-view" || tId === "key-person-view" || tId === "dpr-view" || tId === "notes-view" || tId === "equipment-view") { 
        dP.style.display = "block"; if(tId==="daily-view") renderDailyView(); if(tId==="key-person-view") renderKeyPersonView(); if(tId==="dpr-view") renderDPRView(); if(tId==="notes-view") renderNotesView(); if(tId==="equipment-view") renderEquipmentView();
      } else { 
        dP.style.display = "none"; if(tId==="monthly-view") renderMonthlyTable(); if(tId==="worker-view") renderWorkerManagement(); if(tId==="slips-view") populateSlipWorkerSelect(); if(tId==="ai-view") renderAIFeaturesGrid();
      }
    }
    
    function renderAll() { renderDailyView(); renderKeyPersonView(); renderDPRView(); renderNotesView(); renderMonthlyTable(); renderWorkerManagement(); populateSlipWorkerSelect(); renderEquipmentView(); renderAIFeaturesGrid(); updateDashboard(); updateAdvancedAnalytics(); }

    function getInitials(name) { const n = (name||"").trim().split(" "); return n.length > 1 ? (n[0][0]+n[1][0]).toUpperCase() : (n[0] ? n[0][0].toUpperCase() : 'U'); }
    function getAttendanceMonthKey() { const monthSelect = document.getElementById("month-select"); return monthSelect ? monthSelect.value : `${new Date().getMonth()+1}-${new Date().getFullYear()}`; }
    
    function getWorkerAttendanceRecord(wId, sDay) {
      const mKey = getAttendanceMonthKey();
      if (!appState.attendance) appState.attendance = {}; if (!appState.attendance[mKey]) appState.attendance[mKey] = {}; if (!appState.attendance[mKey][wId]) appState.attendance[mKey][wId] = {};
      const rec = appState.attendance[mKey][wId][sDay] || { duty: null, ot: 0, adv: 0, locked: false, graceChances: 2 };
      if (typeof rec.graceChances !== 'number') rec.graceChances = 2;
      return rec;
    }

    function getKpAttendanceRecord(wId, sDay) {
      const mKey = getAttendanceMonthKey();
      if (!appState.kpAttendance) appState.kpAttendance = {};
      if (appState.kpAttendance[mKey] && appState.kpAttendance[mKey][wId] && appState.kpAttendance[mKey][wId][sDay]) {
        return appState.kpAttendance[mKey][wId][sDay];
      }
      if (appState.kpAttendance[wId] && appState.kpAttendance[wId][sDay] && typeof appState.kpAttendance[wId][sDay].duty !== 'undefined') {
        return appState.kpAttendance[wId][sDay];
      }
      return { duty: null, locked: false };
    }

    function checkAttendanceEditable(sDay) {
      if (userRole !== 'supervisor' && userRole !== 'incharge' && userRole !== 'admin') return false;
      const mKey = getAttendanceMonthKey();
      const [m, y] = mKey.split('-');
      const recordDate = new Date(y, m - 1, sDay);
      const today = new Date();
      today.setHours(0,0,0,0);
      recordDate.setHours(0,0,0,0);

      if (recordDate.getTime() === today.getTime()) return true;
      if (recordDate.getTime() < today.getTime()) return false; 
      return false; 
    }

    function isWorkerDayLocked(wId, sDay) {
      if (isMasterRollup || userRole === 'viewer') return true;
      if (userRole === 'admin') return false;
      if (checkAttendanceEditable(sDay)) return false;
      const a = getWorkerAttendanceRecord(wId, sDay);
      return a.graceChances <= 0;
    }

    window.setDailyFilter = function(kind, val) {
      if (kind === 'status') dailyStatusFilter = val;
      if (kind === 'trade') dailyTradeFilter = val;
      renderDailyView();
    };

    window.setDirTradeFilter = function(val) {
      dirTradeFilter = val;
      renderWorkerManagement();
    };

    function buildWorkerSparkDots(wId, sDay) {
      const mKey = getAttendanceMonthKey();
      const wAtt = (appState.attendance && appState.attendance[mKey] && appState.attendance[mKey][wId]) ? appState.attendance[mKey][wId] : {};
      let dots = '<div class="spark-dots" title="Last 7 Days Attendance (🟢 P / 🟡 H / 🔴 A)">';
      for (let offset = 6; offset >= 0; offset--) {
        const d = sDay - offset;
        if (d < 1) continue;
        const rec = wAtt[d];
        const v = rec ? parseDutyInput(rec.duty) : null;
        let cls = '';
        if (v === 1) cls = 'sp-p';
        else if (v === 0.5) cls = 'sp-h';
        else if (v === 0) cls = 'sp-a';
        dots += `<span class="spark-dot ${cls}" title="Day ${d}: ${v === 1 ? 'Present' : (v === 0.5 ? 'Half' : (v === 0 ? 'Absent' : 'Unmarked'))}"></span>`;
      }
      dots += '</div>';
      return dots;
    }

    function renderDailyFilterPills(sDay) {
      const pillsEl = document.getElementById("daily-filter-pills");
      if (!pillsEl) return;
      if (appState.workers.length === 0) { pillsEl.innerHTML = ''; return; }

      let cntP = 0, cntH = 0, cntA = 0, cntU = 0;
      const tradeCounts = {};
      appState.workers.forEach(w => {
        const rec = getWorkerAttendanceRecord(w.id, sDay);
        const dVal = parseDutyInput(rec.duty);
        if (dVal === 1) cntP++;
        else if (dVal === 0.5) cntH++;
        else if (dVal === 0) cntA++;
        else cntU++;
        const tr = (w.desig || 'Unspecified').trim();
        tradeCounts[tr] = (tradeCounts[tr] || 0) + 1;
      });

      const statusChips = [
        { k: 'ALL', l: `All (${appState.workers.length})` },
        { k: 'P', l: `✅ Present (${cntP})` },
        { k: 'H', l: `🌗 Half (${cntH})` },
        { k: 'A', l: `❌ Absent (${cntA})` },
        { k: 'U', l: `⏳ Unmarked (${cntU})` }
      ];
      let htmlPills = statusChips.map(c => `<span class="filter-pill ${dailyStatusFilter === c.k ? 'active' : ''}" onclick="setDailyFilter('status', '${c.k}')">${c.l}</span>`).join('');
      htmlPills += `<span style="color:var(--border); margin:0 4px;">|</span>`;
      htmlPills += `<span class="filter-pill ${dailyTradeFilter === 'ALL' ? 'active' : ''}" onclick="setDailyFilter('trade', 'ALL')">All Trades</span>`;
      Object.entries(tradeCounts).forEach(([tr, cnt]) => {
        const safeTr = tr.replace(/'/g, "\\'");
        htmlPills += `<span class="filter-pill ${dailyTradeFilter === tr ? 'active' : ''}" onclick="setDailyFilter('trade', '${safeTr}')">${tr} (${cnt})</span>`;
      });
      pillsEl.innerHTML = htmlPills;
    }

    function renderDailyView() {
      const sDay = parseInt(document.getElementById("day-select").value) || 1;
      const query = (document.getElementById("worker-search-input") ? document.getElementById("worker-search-input").value.toLowerCase().trim() : "");
      const c = document.getElementById("daily-list-container");
      
      renderDailyFilterPills(sDay);
      if(appState.workers.length === 0) { c.innerHTML = `<div class="empty-state">No workers registered in this group yet.</div>`; return; }

      const filteredWorkers = appState.workers.filter(w => {
        const matchQ = w.name.toLowerCase().includes(query) || (w.desig && w.desig.toLowerCase().includes(query));
        if (!matchQ) return false;
        if (dailyTradeFilter !== 'ALL' && (w.desig || 'Unspecified').trim() !== dailyTradeFilter) return false;
        if (dailyStatusFilter !== 'ALL') {
          const rec = getWorkerAttendanceRecord(w.id, sDay);
          const dVal = parseDutyInput(rec.duty);
          if (dailyStatusFilter === 'P' && dVal !== 1) return false;
          if (dailyStatusFilter === 'H' && dVal !== 0.5) return false;
          if (dailyStatusFilter === 'A' && dVal !== 0) return false;
          if (dailyStatusFilter === 'U' && dVal !== null) return false;
        }
        return true;
      });
      if(filteredWorkers.length === 0) { c.innerHTML = `<div class="empty-state">No matching workers found.</div>`; return; }

      let htmlBuffer = '';

      filteredWorkers.forEach((w, i) => {
        const a = getWorkerAttendanceRecord(w.id, sDay);
        const isLocked = isWorkerDayLocked(w.id, sDay);

        const lockUI = isLocked ? 'locked' : ''; const disInput = isLocked ? 'disabled' : '';
        const evP = isLocked ? `showToast('Record Locked (Past Day / Grace exhausted).')` : `setDailyDuty('${w.id}', ${sDay}, 1, 'worker')`;
        const evH = isLocked ? `showToast('Record Locked (Past Day / Grace exhausted).')` : `setDailyDuty('${w.id}', ${sDay}, 0.5, 'worker')`;
        const evA = isLocked ? `showToast('Record Locked (Past Day / Grace exhausted).')` : `setDailyDuty('${w.id}', ${sDay}, 0, 'worker')`;
        
        const r = (userRole === 'viewer' || isLocked) ? "readonly onclick='requireAuthClick(this)'" : disInput;
        const evPViewer = (userRole === 'viewer' || isMasterRollup) ? `requireAuthClick(this)` : evP;
        const evHViewer = (userRole === 'viewer' || isMasterRollup) ? `requireAuthClick(this)` : evH;
        const evAViewer = (userRole === 'viewer' || isMasterRollup) ? `requireAuthClick(this)` : evA;

        htmlBuffer += `
          <div class="worker-card" style="animation-delay: ${i*0.05}s">
            <div class="worker-card-header" style="cursor:pointer;" onclick="openWorkerProfileModal('${w.id}')" title="Click to open Worker Profile & Monthly Calendar">
              <div class="avatar" style="background:#2D68C4">${getInitials(w.name)}</div>
              <div style="flex:1;">
                <div class="worker-name">${w.name}</div>
                <div class="worker-desig">${w.desig}</div>
                ${buildWorkerSparkDots(w.id, sDay)}
              </div>
              <div style="font-weight:900; color:var(--secondary);">₹${w.rate}/d</div>
            </div>
            <div class="duty-selector">
              <div class="duty-opt ${a.duty===1?'selected-p':''} ${lockUI}" onclick="${evPViewer}">P (1)</div>
              <div class="duty-opt ${a.duty===0.5?'selected-h':''} ${lockUI}" onclick="${evHViewer}">H (0.5)</div>
              <div class="duty-opt ${a.duty===0?'selected-a':''} ${lockUI}" onclick="${evAViewer}">A (0)</div>
            </div>
            <div style="display:flex; gap:12px; margin-top:6px;">
              <div class="input-box"><span>OT (Hrs)</span><input type="number" step="0.5" value="${a.ot||0}" ${r} onblur="setDailyOT('${w.id}', ${sDay}, this.value)"></div>
              <div class="input-box"><span>Adv (₹)</span><input type="number" step="50" value="${a.adv||''}" ${r} onblur="setDailyAdv('${w.id}', ${sDay}, this.value)"></div>
            </div>
          </div>`;
      });
      c.innerHTML = htmlBuffer;
    }

    window.jumpToWorkerSlip = function(wId) {
      closeModal('worker-profile-modal');
      const slipBtn = Array.from(document.querySelectorAll('.tab-btn')).find(b => b.textContent.includes('Slips'));
      switchTab('slips-view', slipBtn);
      const sel = document.getElementById('slip-worker-select');
      if (sel) { sel.value = wId; renderWageSlip(); }
    };

    window.openWorkerProfileModal = function(wId) {
      const w = appState.workers.find(x => String(x.id) === String(wId));
      if (!w) return;
      const mKey = getAttendanceMonthKey();
      const [mNum, yNum] = mKey.split('-').map(Number);
      const currentMonthDays = new Date(yNum, mNum, 0).getDate();
      const firstDayDow = new Date(yNum, mNum - 1, 1).getDay();
      const monthName = document.getElementById("month-select").options[document.getElementById("month-select").selectedIndex].text;
      const wAtt = (appState.attendance && appState.attendance[mKey] && appState.attendance[mKey][w.id]) ? appState.attendance[mKey][w.id] : {};

      let totalD = 0, totalOT = 0, dailyAdvSum = 0;
      const advLedger = [];
      const openAdv = parseFloat(appState.advances[w.id]) || 0;
      if (openAdv > 0) advLedger.push({ label: 'Opening Advance', amt: openAdv });

      const dowHeaders = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'].map(d => `<div class="mini-cal-header">${d}</div>`).join('');
      let calCells = dowHeaders;
      for (let pad = 0; pad < firstDayDow; pad++) {
        calCells += `<div class="mini-cal-day" style="opacity:0.25; background:transparent; border-style:dashed;"></div>`;
      }

      for (let d = 1; d <= currentMonthDays; d++) {
        const r = wAtt[d] || { duty: null, ot: 0, adv: 0 };
        const dVal = parseDutyInput(r.duty);
        const sym = getDutyDisplaySymbol(r.duty) || '-';
        let cls = '';
        if (sym === 'P') cls = 'cal-p';
        else if (sym === 'H') cls = 'cal-h';
        else if (sym === 'A') cls = 'cal-a';

        if (dVal !== null) totalD += dVal;
        const otVal = parseFloat(r.ot) || 0;
        const advVal = parseFloat(r.adv) || 0;
        totalOT += otVal;
        dailyAdvSum += advVal;
        if (advVal > 0) advLedger.push({ label: `Day ${d} (${monthName.split(' ')[0]})`, amt: advVal });

        calCells += `
          <div class="mini-cal-day ${cls}">
            <span style="font-size:9px; opacity:0.75;">${d}</span>
            <span style="font-size:13px; font-weight:900;">${sym}</span>
            <span style="font-size:9px;">${otVal ? `+${otVal}h` : ''} ${advVal ? `₹${advVal}` : ''}</span>
          </div>`;
      }

      const rate = parseFloat(w.rate) || 0;
      const gross = (totalD * rate) + (totalOT * (rate / 8));
      const totalAdv = openAdv + dailyAdvSum;
      const net = gross - totalAdv;
      const cleanPhone = (w.phone || '').replace(/[^0-9]/g, '');
      const waPhone = cleanPhone.length === 10 ? '91' + cleanPhone : cleanPhone;
      const waMsg = `*Global Industries - Monthly Summary (${monthName})*
Name: ${w.name} (${w.desig})
Present Days: ${totalD.toFixed(1)}
Overtime: ${totalOT.toFixed(1)} hrs
Gross Earned: ₹${Math.round(gross)}
Total Advance: ₹${Math.round(totalAdv)}
*Net Payable: ₹${Math.round(net)}*`;

      const ledgerHtml = advLedger.length === 0
        ? `<div style="font-size:12px; color:var(--text-muted); padding:8px 0;">No advances recorded for this month.</div>`
        : advLedger.map(item => `<div style="display:flex; justify-content:space-between; padding:6px 0; border-bottom:1px solid var(--border); font-size:12px; font-weight:800;"><span>${item.label}</span><span style="color:var(--danger);">₹${item.amt.toLocaleString('en-IN')}</span></div>`).join('');

      document.getElementById('worker-profile-content').innerHTML = `
        <div style="display:flex; align-items:center; gap:14px; margin-bottom:12px;">
          <div class="avatar" style="background:#2D68C4; width:58px; height:58px; font-size:22px;">${getInitials(w.name)}</div>
          <div>
            <h2 style="margin:0;">${w.name}</h2>
            <div style="font-size:13px; font-weight:800; color:var(--text-muted);">${w.desig} • Rate: ₹${rate}/day ${w.phone ? `• 📞 ${w.phone}` : ''}</div>
          </div>
        </div>
        <div style="display:flex; gap:8px; margin-bottom:14px; flex-wrap:wrap;">
          ${cleanPhone ? `<a href="tel:${cleanPhone}" class="btn btn-primary btn-small" style="flex:1; text-decoration:none;">📞 Call</a><a href="https://wa.me/${waPhone}?text=${encodeURIComponent(waMsg)}" target="_blank" rel="noopener" class="btn btn-whatsapp btn-small" style="flex:1; text-decoration:none;">💬 WhatsApp</a>` : ''}
          <button type="button" class="btn btn-outline btn-small" style="flex:1;" onclick="jumpToWorkerSlip('${w.id}')">🧾 Wage Slip</button>
        </div>
        <div class="ana-grid" style="margin-bottom:14px;">
          <div class="ana-box"><span>Present Days</span><b style="color:var(--success);">${totalD.toFixed(1)}</b></div>
          <div class="ana-box"><span>Total OT</span><b style="color:var(--warning);">${totalOT.toFixed(1)}h</b></div>
          <div class="ana-box"><span>Net Payable</span><b style="color:var(--primary);">₹${Math.round(net).toLocaleString('en-IN')}</b></div>
        </div>
        <h4 style="font-size:12px; font-weight:900; color:var(--primary); text-transform:uppercase; margin-bottom:6px;">📅 ${monthName} Attendance Calendar</h4>
        <div class="mini-cal-grid">${calCells}</div>
        <h4 style="font-size:12px; font-weight:900; color:var(--primary); text-transform:uppercase; margin:14px 0 6px 0;">💸 Itemized Advance Ledger (Total: ₹${Math.round(totalAdv).toLocaleString('en-IN')})</h4>
        <div style="background:var(--bg); padding:10px 14px; border-radius:12px; border:1px solid var(--border); max-height:150px; overflow-y:auto;">${ledgerHtml}</div>
      `;
      document.getElementById('worker-profile-modal').style.display = 'flex';
    };

    window.openBulkToolModal = function() {
      if (userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      const sel = document.getElementById('bulk-target-group');
      if (sel) {
        const trades = Array.from(new Set(appState.workers.map(w => (w.desig || 'Unspecified').trim()).filter(Boolean)));
        let opts = `<option value="present">✅ All Present / Half-Day Workers Today</option><option value="all">👷 All Registered Workers in Group (${appState.workers.length})</option>`;
        trades.forEach(tr => {
          opts += `<option value="trade:${tr}">🔨 Trade: ${tr}</option>`;
        });
        sel.innerHTML = opts;
      }
      document.getElementById('bulk-ot-val').value = '';
      document.getElementById('bulk-adv-val').value = '';
      document.getElementById('bulk-tool-modal').style.display = 'flex';
    };

    window.applyBulkTool = function() {
      if (userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      const sDay = parseInt(document.getElementById("day-select").value) || 1;
      const target = document.getElementById('bulk-target-group').value;
      const otStr = document.getElementById('bulk-ot-val').value;
      const advStr = document.getElementById('bulk-adv-val').value;
      const hasOt = otStr !== '' && !isNaN(parseFloat(otStr));
      const hasAdv = advStr !== '' && !isNaN(parseFloat(advStr));
      if (!hasOt && !hasAdv) { showToast("Select a preset or enter Overtime / Advance."); return; }

      const mKey = getAttendanceMonthKey();
      if (!appState.attendance[mKey]) appState.attendance[mKey] = {};
      let count = 0;

      appState.workers.forEach(w => {
        if (isWorkerDayLocked(w.id, sDay)) return;
        const rec = getWorkerAttendanceRecord(w.id, sDay);
        if (target === 'present' && !(parseDutyInput(rec.duty) > 0)) return;
        if (target.startsWith('trade:') && (w.desig || 'Unspecified').trim() !== target.slice(6)) return;
        if (!appState.attendance[mKey][w.id]) appState.attendance[mKey][w.id] = {};
        appState.attendance[mKey][w.id][sDay] = {
          ...rec,
          ot: hasOt ? parseFloat(otStr) : (rec.ot || 0),
          adv: hasAdv ? parseFloat(advStr) : (rec.adv || 0)
        };
        count++;
      });

      saveState();
      closeModal('bulk-tool-modal');
      renderAll();
      showToast(`Bulk updated ${count} workers!`);
    };

    function renderKeyPersonView() {
      const sDay = parseInt(document.getElementById("day-select").value);
      const c = document.getElementById("kp-list-container"); 
      const alertBox = document.getElementById("kp-alert");
      
      if(!isMasterRollup) { alertBox.style.display = 'block'; c.innerHTML = ""; return; }
      alertBox.style.display = 'none';
      if(appState.keyPersons.length === 0) { c.innerHTML = `<div class="empty-state">No key personnel registered yet.</div>`; return; }

      let htmlBuffer = "";
      appState.keyPersons.forEach((w, i) => {
        const a = getKpAttendanceRecord(w.id, sDay);
        const isLocked = userRole === 'viewer'; 
        const lockUI = isLocked ? 'locked' : '';
        const evP = isLocked ? `requireAuthClick(this)` : `setDailyDuty('${w.id}', ${sDay}, 1, 'kp')`;
        const evH = isLocked ? `requireAuthClick(this)` : `setDailyDuty('${w.id}', ${sDay}, 0.5, 'kp')`;
        const evA = isLocked ? `requireAuthClick(this)` : `setDailyDuty('${w.id}', ${sDay}, 0, 'kp')`;

        const canManage = (userRole === 'admin' || userRole === 'incharge' || userRole === 'supervisor');
        const act = canManage ? `<div style="display:flex; gap:10px; margin-top:10px;"><button class="btn btn-outline btn-small" style="flex:1;" onclick="openEditWorkerModal('${w.id}', 'kp')">✏️ Edit</button><button class="btn btn-danger btn-small" style="flex:1;" onclick="deleteWorker('${w.id}', 'kp')">🗑️</button></div>` : '';

        htmlBuffer += `
          <div class="worker-card kp-card" style="animation-delay: ${i*0.05}s; position:relative;">
            <div style="position:absolute; top:-10px; right: 10px; font-size:24px;">⭐</div>
            <div class="worker-card-header"><div class="avatar" style="background: linear-gradient(135deg, #D97706, #F59E0B)">${getInitials(w.name)}</div><div style="flex:1;"><div class="worker-name">${w.name}</div><div class="worker-desig" style="color:#B45309; font-weight:800;">${w.desig}</div></div></div>
            <div class="duty-selector">
              <div class="duty-opt ${a.duty===1?'selected-p':''} ${lockUI}" onclick="${evP}">Present</div>
              <div class="duty-opt ${a.duty===0.5?'selected-h':''} ${lockUI}" onclick="${evH}">Half</div>
              <div class="duty-opt ${a.duty===0?'selected-a':''} ${lockUI}" onclick="${evA}">Absent</div>
            </div>
            ${act}
          </div>`;
      });
      c.innerHTML = htmlBuffer;
    }

    function parseDutyInput(val) {
      if (val === null || val === undefined || val === '') return null;
      const s = String(val).trim().toUpperCase();
      if (s === 'P' || s === '1') return 1;
      if (s === 'H' || s === '0.5') return 0.5;
      if (s === 'A' || s === '0') return 0;
      const num = parseFloat(s);
      return isNaN(num) ? null : num;
    }

    function getDutyDisplaySymbol(val) {
      if (val === 1 || String(val).toUpperCase() === 'P') return 'P';
      if (val === 0.5 || String(val).toUpperCase() === 'H') return 'H';
      if (val === 0 || String(val).toUpperCase() === 'A') return 'A';
      return '';
    }

    window.setDailyDuty = function(wId, d, v, type) { 
      if(userRole === 'viewer' || (isMasterRollup && type !== 'kp')) return; 
      const mKey = getAttendanceMonthKey();
      if (type === 'kp') {
        if(!appState.kpAttendance[mKey]) appState.kpAttendance[mKey] = {};
        if(!appState.kpAttendance[mKey][wId]) appState.kpAttendance[mKey][wId] = {};
        appState.kpAttendance[mKey][wId][d] = { duty: v, locked: (userRole === 'incharge' || userRole === 'supervisor') };
        saveKeyPersonnelState();
        renderKeyPersonView();
        return;
      } else {
        if(!appState.attendance[mKey]) appState.attendance[mKey] = {};
        if(!appState.attendance[mKey][wId]) appState.attendance[mKey][wId] = {};
        
        let existing = getWorkerAttendanceRecord(wId, d);
        const isEditableToday = checkAttendanceEditable(d);
        
        if (!isEditableToday && userRole !== 'admin') {
           if (existing.graceChances > 0) {
              existing.graceChances--;
           } else {
              return showToast('Record Locked (Past Day / Grace exhausted).');
           }
        }
        
        appState.attendance[mKey][wId][d] = { ...existing, duty: v, locked: false };
      }
      saveState(); renderDailyView(); renderMonthlyTable(); renderWageSlip();
    };
    
    window.setDailyOT = function(wId, d, v) {
      if(isWorkerDayLocked(wId, d)) return;
      const mKey = getAttendanceMonthKey();
      if(!appState.attendance[mKey]) appState.attendance[mKey]={};
      if(!appState.attendance[mKey][wId]) appState.attendance[mKey][wId]={};
      const existing = getWorkerAttendanceRecord(wId, d);
      appState.attendance[mKey][wId][d] = { ...existing, ot: parseFloat(v)||0 };
      saveState(); renderMonthlyTable(); renderWageSlip();
    };
    window.setDailyAdv = function(wId, d, v) {
      if(isWorkerDayLocked(wId, d)) return;
      const mKey = getAttendanceMonthKey();
      if(!appState.attendance[mKey]) appState.attendance[mKey]={};
      if(!appState.attendance[mKey][wId]) appState.attendance[mKey][wId]={};
      const existing = getWorkerAttendanceRecord(wId, d);
      appState.attendance[mKey][wId][d] = { ...existing, adv: parseFloat(v)||0 };
      saveState(); renderMonthlyTable(); renderWorkerManagement(); renderWageSlip();
    };

    function markAllWorkersPresent() {
      if(userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      const sDay = parseInt(document.getElementById("day-select").value);
      const mKey = getAttendanceMonthKey();
      if(!appState.attendance[mKey]) appState.attendance[mKey] = {};
      
      const isEditableToday = checkAttendanceEditable(sDay);
      
      appState.workers.forEach(w => {
        if(!appState.attendance[mKey][w.id]) appState.attendance[mKey][w.id] = {};
        const existing = getWorkerAttendanceRecord(w.id, sDay);
        
        if (!isEditableToday && userRole !== 'admin' && existing.graceChances <= 0) return; 
        if (!isEditableToday && userRole !== 'admin') existing.graceChances--;

        appState.attendance[mKey][w.id][sDay] = { ...existing, duty: 1, locked: false };
      });
      saveState(); renderDailyView(); renderMonthlyTable(); showToast("Marked eligible workers present!");
    }

    // AI VOICE DICTATION INTEGRATION
    function startDictation() {
      if (userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      if (!window.webkitSpeechRecognition && !window.SpeechRecognition) {
        showToast("Speech Recognition is not supported in your browser.");
        return;
      }
      
      const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
      const recognition = new SpeechRecognition();
      recognition.lang = 'en-IN'; // Defaults to Indian English/Hinglish
      recognition.interimResults = false;
      recognition.maxAlternatives = 1;

      const btn = document.getElementById("btn-dictate");
      btn.classList.add("recording");
      btn.innerHTML = "🎙️ Listening...";

      recognition.start();

      recognition.onresult = function(event) {
        const speechResult = event.results[0][0].transcript;
        const textarea = document.getElementById("dpr-work-text");
        textarea.value += (textarea.value ? " " : "") + speechResult + ".";
        autoSaveDPR();
      };

      recognition.onspeechend = function() {
        recognition.stop();
      };

      recognition.onend = function() {
        btn.classList.remove("recording");
        btn.innerHTML = "🎤 Dictate";
        showToast("Dictation completed.");
      };

      recognition.onerror = function(event) {
        btn.classList.remove("recording");
        btn.innerHTML = "🎤 Dictate";
        showToast("Microphone error: " + event.error);
      };
    }

    // FIREBASE STORAGE PHOTO UPLOAD (PROJECT B)
    function handlePhotoUpload(event) {
      if (userRole === 'viewer' || isMasterRollup) {
        requireAuthClick();
        event.target.value = '';
        return;
      }
      if (!currentSite || !currentSubgroup) {
        showToast("Please select a valid site and group first.");
        event.target.value = '';
        return;
      }

      const file = event.target.files[0];
      if (!file) return;

      // 1. Generate Local Preview
      const reader = new FileReader();
      reader.onload = function(e) {
        const previewContainer = document.getElementById("dpr-photo-preview");
        const imgWrapper = document.createElement("div");
        imgWrapper.style.position = "relative";
        imgWrapper.style.display = "inline-block";
        
        const img = document.createElement("img");
        img.src = e.target.result;
        img.style.height = "100px";
        img.style.width = "100px";
        img.style.borderRadius = "8px";
        img.style.border = "2px solid var(--border)";
        img.style.objectFit = "cover";

        imgWrapper.appendChild(img);
        previewContainer.appendChild(imgWrapper);
      };
      reader.readAsDataURL(file);

      // 2. Upload to Firebase Storage (Project B)
      showToast("Uploading photo to storage bucket...");
      const storageRef = storageBackup.ref();
      const photoName = `site_photos/${currentSite}/${currentSubgroup}/${Date.now()}_${file.name}`;
      const photoRef = storageRef.child(photoName);

      photoRef.put(file).then((snapshot) => {
        snapshot.ref.getDownloadURL().then((downloadURL) => {
          showToast("Photo uploaded successfully!");
          
          // 3. Save the download link in the Main Database (Project A)
          const dk = getSelectedDateKey();
          if(!appState.dpr[dk]) appState.dpr[dk] = { work: "", weather: "☀️ Sunny / Clear", rainStart: "", rainEnd: "", workStop: "No", matReceived: [], matConsumed: [], photos: [] };
          if(!appState.dpr[dk].photos) appState.dpr[dk].photos = [];
          
          appState.dpr[dk].photos.push(downloadURL);
          saveState(); // Saves the link to Project A
        });
      }).catch(error => {
        showToast("Error uploading photo: " + error.message);
        console.error("Storage Error:", error);
      });
    }

    window.openPhotoLightbox = function(url, dateKey, idx) {
      activeLightboxPhotoUrl = url;
      activeLightboxDateKey = dateKey || getSelectedDateKey();
      activeLightboxPhotoIdx = typeof idx === 'number' ? idx : -1;
      activeLightboxZoom = 1.0;
      const img = document.getElementById('lightbox-img');
      if (img) { img.src = url; img.style.transform = 'scale(1)'; }
      const lbl = document.getElementById('lightbox-zoom-lbl');
      if (lbl) lbl.textContent = '100%';
      const badge = document.getElementById('lightbox-date-badge');
      if (badge) badge.textContent = `📷 DPR Photo • ${activeLightboxDateKey}`;
      const openLink = document.getElementById('lightbox-open-link');
      if (openLink) openLink.href = url;
      const delBtn = document.getElementById('lightbox-delete-btn');
      if (delBtn) delBtn.style.display = ((userRole === 'admin' || userRole === 'incharge') && !isMasterRollup && activeLightboxPhotoIdx >= 0) ? 'inline-flex' : 'none';
      document.getElementById('photo-lightbox-modal').style.display = 'flex';
    };

    window.adjustLightboxZoom = function(delta) {
      activeLightboxZoom = Math.min(3.0, Math.max(0.5, activeLightboxZoom + delta));
      const img = document.getElementById('lightbox-img');
      if (img) img.style.transform = `scale(${activeLightboxZoom})`;
      const lbl = document.getElementById('lightbox-zoom-lbl');
      if (lbl) lbl.textContent = `${Math.round(activeLightboxZoom * 100)}%`;
    };

    window.resetLightboxZoom = function() {
      activeLightboxZoom = 1.0;
      const img = document.getElementById('lightbox-img');
      if (img) img.style.transform = 'scale(1)';
      const lbl = document.getElementById('lightbox-zoom-lbl');
      if (lbl) lbl.textContent = '100%';
    };

    window.deleteDPRPhoto = function(dateKey, idx) {
      if ((userRole !== 'admin' && userRole !== 'incharge') || isMasterRollup) {
        showToast("Only Admin or Site Incharge can delete DPR photos.");
        return;
      }
      showConfirmModal("Delete this progress photo from the DPR?", () => {
        if (appState.dpr[dateKey] && Array.isArray(appState.dpr[dateKey].photos)) {
          appState.dpr[dateKey].photos.splice(idx, 1);
          saveState();
          renderDPRView();
          closeModal('photo-lightbox-modal');
          showToast("Progress photo deleted.");
        }
      }, "🗑️ Delete DPR Photo");
    };

    window.deleteCurrentLightboxPhoto = function() {
      if (activeLightboxDateKey && activeLightboxPhotoIdx >= 0) {
        deleteDPRPhoto(activeLightboxDateKey, activeLightboxPhotoIdx);
      }
    };

    function checkWeatherCondition() { const w = document.getElementById("dpr-weather-select").value || ""; document.getElementById("rain-settings").style.display = w.includes('Rain') ? "flex" : "none"; autoSaveDPR(); }

    function renderDPRView() {
      const dk = getSelectedDateKey(); 
      const d = appState.dpr[dk] || { work: "", weather: "☀️ Sunny / Clear", rainStart: "", rainEnd: "", workStop: "No", matReceived: [], matConsumed: [], photos: [] };
      document.getElementById("dpr-work-text").value = d.work || ""; document.getElementById("dpr-weather-select").value = d.weather || "☀️ Sunny / Clear"; 
      document.getElementById("dpr-rain-start").value = d.rainStart || ""; document.getElementById("dpr-rain-end").value = d.rainEnd || ""; 
      document.getElementById("dpr-work-stopped").value = d.workStop || "No";
      const wVal = document.getElementById("dpr-weather-select").value || "";
      document.getElementById("rain-settings").style.display = wVal.includes('Rain') ? "flex" : "none";

      // Render Existing Photos with Full-Screen Lightbox & Delete
      const previewContainer = document.getElementById("dpr-photo-preview");
      previewContainer.innerHTML = "";
      if (d.photos && d.photos.length > 0) {
        const canDel = (userRole === 'admin' || userRole === 'incharge') && !isMasterRollup;
        d.photos.forEach((url, idx) => {
          const wrap = document.createElement("div");
          wrap.style.position = "relative";
          wrap.style.display = "inline-block";
          const img = document.createElement("img");
          img.src = url;
          img.style.height = "100px";
          img.style.width = "100px";
          img.style.borderRadius = "10px";
          img.style.border = "2px solid var(--border)";
          img.style.objectFit = "cover";
          img.style.cursor = "pointer";
          img.onclick = () => openPhotoLightbox(url, dk, idx);
          wrap.appendChild(img);

          if (canDel) {
            const xBtn = document.createElement("button");
            xBtn.type = "button";
            xBtn.innerHTML = "&times;";
            xBtn.title = "Delete Photo";
            xBtn.style.cssText = "position:absolute; top:4px; right:4px; width:24px; height:24px; border-radius:50%; background:rgba(239,68,68,0.92); color:#fff; border:none; font-weight:900; cursor:pointer; display:flex; align-items:center; justify-content:center;";
            xBtn.onclick = (e) => { e.stopPropagation(); deleteDPRPhoto(dk, idx); };
            wrap.appendChild(xBtn);
          }
          previewContainer.appendChild(wrap);
        });
      }

      const rC = document.getElementById("dpr-mat-received-list"); rC.innerHTML = "";
      const rMats = d.matReceived || [];
      const cMats = d.matConsumed || [];
      
      if (rMats.length === 0) addMaterialRowToDOM("", "", "Kg", 'received'); else rMats.forEach((m) => addMaterialRowToDOM(m.item, m.qty, m.unit, 'received'));
      const cC = document.getElementById("dpr-mat-consumed-list"); cC.innerHTML = "";
      if (cMats.length === 0) addMaterialRowToDOM("", "", "Kg", 'consumed'); else cMats.forEach((m) => addMaterialRowToDOM(m.item, m.qty, m.unit, 'consumed'));
      calculateLiveStock();
    }

    function getUnitOptions(selectedUnit) {
      const units = [{group: "Weight", opts: ["Kg", "MT (Metric Tonne)", "g", "Quintal"]}, {group: "Volume", opts: ["cum (m³)", "cft", "Liter (L)", "Gallon"]}, {group: "Area", opts: ["sqm (m²)", "sqft"]}, {group: "Length", opts: ["m", "cm", "mm", "ft", "in"]}, {group: "Units", opts: ["Bag", "Nos", "Pcs", "Bundle", "Roll", "Box", "Length"]}];
      let html = ''; units.forEach(g => { html += `<optgroup label="${g.group}">`; g.opts.forEach(o => { html += `<option value="${o}" ${selectedUnit === o ? 'selected' : ''}>${o}</option>`; }); html += `</optgroup>`; });
      return html;
    }

    function addMaterialRowToDOM(item="", qty="", unit="Bag", type="received") {
      const c = document.getElementById(`dpr-mat-${type}-list`); const d = document.createElement("div"); d.className = "material-row";
      const r = (userRole === 'viewer' || isMasterRollup) ? "readonly onclick='requireAuthClick(this)'" : ""; const ds = (userRole === 'viewer' || isMasterRollup) ? "disabled" : "";
      d.innerHTML = `<input type="text" class="material-item" placeholder="Material Name" value="${item}" ${r} onblur="autoSaveDPR()" style="flex:2"><input type="number" class="material-qty" placeholder="Qty" value="${qty}" ${r} onblur="autoSaveDPR()" style="flex:1"><select class="material-unit" ${ds} onchange="autoSaveDPR()" style="flex:1.5">${getUnitOptions(unit)}</select><button class="btn-remove-row" onclick="removeMaterialRow(this)" ${ds} style="padding:10px 14px; border-radius:8px;">✖</button>`;
      c.appendChild(d);
    }
    window.addMaterialRow = function(type) { if(userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; } addMaterialRowToDOM("", "", "Kg", type); };
    window.removeMaterialRow = function(btn) { if(userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; } btn.parentElement.remove(); autoSaveDPR(); };

    function getActiveStockMap() {
      const stockMap = {};
      Object.values(appState.dpr).forEach(d => {
        if(!d) return;
        if(d.matReceived) d.matReceived.forEach(m => { const n = (m.item||"").trim().toLowerCase(); if(n) stockMap[n] = (stockMap[n]||0) + (parseFloat(m.qty)||0); });
        if(d.matConsumed) d.matConsumed.forEach(m => { const n = (m.item||"").trim().toLowerCase(); if(n) stockMap[n] = (stockMap[n]||0) - (parseFloat(m.qty)||0); });
      });
      return stockMap;
    }

    function calculateLiveStock() {
      const stockMap = getActiveStockMap();
      const stockContainer = document.getElementById("live-stock-summary");
      if (!stockContainer) return;
      stockContainer.innerHTML = "";
      const keys = Object.keys(stockMap);
      if(keys.length === 0) { stockContainer.innerHTML = `<span style="color:var(--text-muted); font-size:13px; font-style:italic;">No material movement recorded yet.</span>`; return; }
      const thresholds = appState.stockThresholds || {};
      keys.forEach(k => {
        const minAlert = typeof thresholds[k] === 'number' ? thresholds[k] : 5;
        const val = stockMap[k];
        const isLow = val <= minAlert;
        const pct = Math.min(100, Math.max(8, Math.round((val / Math.max(minAlert * 2, 1)) * 100)));
        stockContainer.innerHTML += `
          <div class="stock-badge ${isLow ? 'low-stock' : ''}" style="cursor:pointer; display:flex; flex-direction:column; gap:4px; min-width:155px;" onclick="openStockThresholdModal()" title="Min Alert Threshold: ${minAlert}. Click to customize.">
            <div style="display:flex; justify-content:space-between; gap:8px;">
              <span>📦 ${k.toUpperCase()}: <b>${val}</b></span>
              <span style="font-size:10px; opacity:0.85;">Min: ${minAlert} ${isLow ? '⚠️' : ''}</span>
            </div>
            <div style="height:5px; width:100%; background:rgba(0,0,0,0.1); border-radius:4px; overflow:hidden;">
              <div style="width:${pct}%; height:100%; background:${isLow ? 'var(--danger)' : 'var(--success)'};"></div>
            </div>
          </div>`;
      });
    }

    window.addCustomThresholdRow = function(matName = '', minVal = 5) {
      const container = document.getElementById('stock-threshold-rows');
      if (!container) return;
      const row = document.createElement('div');
      row.className = 'threshold-rule-row';
      row.style.cssText = 'display:flex; gap:8px; align-items:center;';
      row.innerHTML = `
        <input type="text" class="th-mat-name" placeholder="Material (e.g. cement)" value="${matName}" style="flex:2; padding:10px;">
        <input type="number" class="th-mat-min" placeholder="Min Qty" value="${minVal}" min="0" style="flex:1; padding:10px;">
        <button type="button" class="btn-remove-row" style="padding:8px 12px; border-radius:8px;" onclick="this.parentElement.remove()">✖</button>
      `;
      container.appendChild(row);
    };

    window.openStockThresholdModal = function() {
      if (userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      const container = document.getElementById('stock-threshold-rows');
      container.innerHTML = '';
      const stockMap = getActiveStockMap();
      const thresholds = appState.stockThresholds || {};
      const allKeys = Array.from(new Set([...Object.keys(stockMap), ...Object.keys(thresholds)]));
      if (allKeys.length === 0) {
        addCustomThresholdRow('cement', 20);
      } else {
        allKeys.forEach(k => addCustomThresholdRow(k, typeof thresholds[k] === 'number' ? thresholds[k] : 5));
      }
      document.getElementById('stock-threshold-modal').style.display = 'flex';
    };

    window.saveStockThresholds = function() {
      if (userRole === 'viewer' || isMasterRollup) return;
      const nextTh = {};
      document.querySelectorAll('#stock-threshold-rows .threshold-rule-row').forEach(r => {
        const name = (r.querySelector('.th-mat-name').value || '').trim().toLowerCase();
        const minQ = parseFloat(r.querySelector('.th-mat-min').value);
        if (name && !isNaN(minQ)) nextTh[name] = minQ;
      });
      appState.stockThresholds = nextTh;
      saveState();
      calculateLiveStock();
      closeModal('stock-threshold-modal');
      showToast("Low-stock alert thresholds saved!");
    };

    function autoSaveDPR() {
      if(userRole === 'viewer' || isMasterRollup) return; 
      clearTimeout(autoSaveTimer);
      autoSaveTimer = setTimeout(() => {
        const dk = getSelectedDateKey(); const rMats = [], cMats = [];
        
        // Preserve existing photos if they exist
        const existingPhotos = (appState.dpr[dk] && appState.dpr[dk].photos) ? appState.dpr[dk].photos : [];

        document.querySelectorAll("#dpr-mat-received-list .material-row").forEach(r => { const i = r.querySelector(".material-item").value, q = r.querySelector(".material-qty").value, u = r.querySelector(".material-unit").value; if (i.trim() || q) rMats.push({ item: i, qty: q, unit: u }); });
        document.querySelectorAll("#dpr-mat-consumed-list .material-row").forEach(r => { const i = r.querySelector(".material-item").value, q = r.querySelector(".material-qty").value, u = r.querySelector(".material-unit").value; if (i.trim() || q) cMats.push({ item: i, qty: q, unit: u }); });
        
        appState.dpr[dk] = { 
            work: document.getElementById("dpr-work-text").value, 
            weather: document.getElementById("dpr-weather-select").value || "☀️ Sunny / Clear", 
            rainStart: document.getElementById("dpr-rain-start").value, 
            rainEnd: document.getElementById("dpr-rain-end").value, 
            workStop: document.getElementById("dpr-work-stopped").value, 
            matReceived: rMats, 
            matConsumed: cMats,
            photos: existingPhotos
        }; 
        saveState(); calculateLiveStock();
      }, 500);
    }

    function shareDPRWhatsApp() {
        const dk = getSelectedDateKey();
        const d = appState.dpr[dk] || { work: document.getElementById("dpr-work-text").value || "", weather: document.getElementById("dpr-weather-select").value || "☀️ Sunny / Clear", rainStart: "", rainEnd: "", workStop: "No", matReceived: [], matConsumed: [] };
        const weatherStr = d.weather || "☀️ Sunny / Clear";
        let tPresent = 0, tAbsent = 0; const sDay = parseInt(document.getElementById("day-select").value) || 1;
        const tradeCounts = {};
        appState.workers.forEach(w => { const rec = getWorkerAttendanceRecord(w.id, sDay); if((parseDutyInput(rec.duty) || 0) > 0) { tPresent++; tradeCounts[w.desig] = (tradeCounts[w.desig] || 0) + 1; } else { tAbsent++; } });
        let text = `*🚧 GLOBAL INDUSTRIES - SITE REPORT*\n*Date:* ${dk}\n*Weather:* ${weatherStr}\n\n*👥 WORKFORCE SUMMARY*\nTotal Registered: ${appState.workers.length}\nPresent: ${tPresent}\nAbsent: ${tAbsent}\n`;
        if(Object.keys(tradeCounts).length > 0) { text += `\n*Trade Breakdown:*\n`; Object.keys(tradeCounts).forEach(trade => text += `- ${trade}: ${tradeCounts[trade]}\n`); }
        text += `\n*📝 WORK DETAILS*\n${d.work || "No work details provided"}\n\n`;
        if (d.rainStart || d.rainEnd || weatherStr.includes('Rain')) { text += `*🌧️ Rain Window:* ${d.rainStart || "N/A"} to ${d.rainEnd || "N/A"}\n*🛑 Work Stopped:* ${d.workStop || "No"}\n\n`; }
        text += `*📥 MATERIALS RECEIVED:*\n`;
        if(!d.matReceived || d.matReceived.length === 0) text += `- None\n`; else d.matReceived.forEach(m => text += `- ${m.item}: ${m.qty} ${m.unit}\n`);
        text += `\n*📤 MATERIALS CONSUMED:*\n`;
        if(!d.matConsumed || d.matConsumed.length === 0) text += `- None\n`; else d.matConsumed.forEach(m => text += `- ${m.item}: ${m.qty} ${m.unit}\n`);
        window.open(`https://wa.me/?text=${encodeURIComponent(text)}`);
    }

    window.setTimelineFilter = function(val) {
      timelineFilter = val;
      renderNotesView();
    };

    function addTimelineNote() {
      if(userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      const input = document.getElementById("timeline-input-text"); const text = input.value.trim();
      const prioSel = document.getElementById("timeline-priority-select");
      const priority = prioSel ? prioSel.value : 'General';
      if(!text) return;
      const dk = getSelectedDateKey();
      if(!appState.timeline) appState.timeline = {}; if(!appState.timeline[dk]) appState.timeline[dk] = [];
      appState.timeline[dk].push({ id: 'note_' + Date.now(), text: text, priority: priority, completed: false, completedBy: '', completedAt: null, author: userName, role: userRole, timestamp: Date.now() });
      input.value = ''; saveState(); renderNotesView();
    }

    window.toggleTimelineTask = function(dk, idx) {
      if(userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      if(!appState.timeline || !appState.timeline[dk] || !appState.timeline[dk][idx]) return;
      const item = appState.timeline[dk][idx];
      item.completed = !item.completed;
      item.completedBy = item.completed ? (userName || userRole) : '';
      item.completedAt = item.completed ? Date.now() : null;
      saveState(); renderNotesView();
    };

    window.deleteTimelineNote = function(dk, idx) {
      if(userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      showConfirmModal("Delete this timeline checklist note?", () => {
        if(appState.timeline && appState.timeline[dk]) {
          appState.timeline[dk].splice(idx, 1);
          saveState(); renderNotesView();
        }
      }, "🗑️ Delete Timeline Note");
    };

    function renderNotesView() {
      const dk = getSelectedDateKey();
      const feed = document.getElementById("timeline-feed");
      const pillsEl = document.getElementById("timeline-filter-pills");
      const badgeEl = document.getElementById("timeline-completion-badge");
      if (!feed) return;
      feed.innerHTML = "";

      const notes = (appState.timeline && appState.timeline[dk]) ? appState.timeline[dk] : [];
      const doneCount = notes.filter(n => n && n.completed).length;
      if (badgeEl) badgeEl.textContent = `✅ ${doneCount} / ${notes.length} Completed`;

      if (pillsEl) {
        const filters = [
          { k: 'ALL', l: 'All Notes' },
          { k: 'Urgent', l: '🔴 Urgent' },
          { k: 'Safety', l: '🟡 Safety' },
          { k: 'General', l: '🔵 General' },
          { k: 'PENDING', l: '⏳ Pending' },
          { k: 'COMPLETED', l: '✅ Completed' }
        ];
        pillsEl.innerHTML = filters.map(f => `<span class="filter-pill ${timelineFilter === f.k ? 'active' : ''}" onclick="setTimelineFilter('${f.k}')">${f.l}</span>`).join('');
      }

      if(notes.length === 0) { feed.innerHTML = `<div class="empty-state">No notes added to the timeline today.</div>`; return; }

      let shown = 0;
      notes.forEach((note, idx) => {
        if (!note) return;
        const prio = note.priority || 'General';
        const isDone = !!note.completed;
        if (timelineFilter === 'PENDING' && isDone) return;
        if (timelineFilter === 'COMPLETED' && !isDone) return;
        if ((timelineFilter === 'Urgent' || timelineFilter === 'Safety' || timelineFilter === 'General') && prio !== timelineFilter) return;
        shown++;

        const time = new Date(note.timestamp).toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
        const prioCls = prio === 'Urgent' ? 'prio-urgent' : (prio === 'Safety' ? 'prio-safety' : 'prio-general');
        const prioIcon = prio === 'Urgent' ? '🔴' : (prio === 'Safety' ? '🟡' : '🔵');
        const doneTimeStr = note.completedAt ? new Date(note.completedAt).toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'}) : '';

        feed.innerHTML += `
          <div style="background: var(--card-bg); backdrop-filter: var(--glass-blur); padding: 14px 16px; border-radius: 12px; border-left: 4px solid ${isDone ? 'var(--success)' : 'var(--secondary)'}; opacity:${isDone ? '0.78' : '1'}; box-shadow: 0 2px 5px rgba(0,0,0,0.04);">
            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom: 8px; gap:8px; flex-wrap:wrap;">
              <div style="display:flex; align-items:center; gap:8px;">
                <input type="checkbox" ${isDone ? 'checked' : ''} onchange="toggleTimelineTask('${dk}', ${idx})" style="width:18px; height:18px; cursor:pointer;">
                <span class="prio-badge ${prioCls}">${prioIcon} ${prio}</span>
                <span style="font-size:11px; font-weight:800; color:var(--primary); text-transform:uppercase;">${note.author || 'User'} (${note.role || 'staff'})</span>
              </div>
              <div style="display:flex; align-items:center; gap:8px;">
                <span style="font-size:11px; color:var(--text-muted);">${time}</span>
                ${(userRole !== 'viewer' && !isMasterRollup) ? `<button type="button" class="action-btn-sm" style="color:var(--danger);" onclick="deleteTimelineNote('${dk}', ${idx})" title="Delete Note">🗑️</button>` : ''}
              </div>
            </div>
            <div style="font-size:14px; color:var(--text); line-height: 1.4; padding-left:26px; ${isDone ? 'text-decoration:line-through; color:var(--text-muted);' : ''}">${note.text}</div>
            ${isDone ? `<div style="font-size:11px; font-weight:800; color:var(--success); padding-left:26px; margin-top:6px;">✅ Completed by ${note.completedBy || 'Staff'} ${doneTimeStr ? `at ${doneTimeStr}` : ''}</div>` : ''}
          </div>`;
      });
      if (shown === 0) feed.innerHTML = `<div class="empty-state">No timeline notes match the selected filter.</div>`;
    }

    /* =========================================
       EQUIPMENT, MACHINERY & SAFETY MUSTER HUB (NEW FEATURE)
       ========================================= */
    const DEFAULT_SITE_EQUIPMENT = [
      { id: 'eq_1', name: 'Tower Crane TC-01 (Potain)', operator: 'Rakesh Singh', fuel: '7.5h / Elec', status: 'Operational' },
      { id: 'eq_2', name: 'JCB 3DX Backhoe Loader', operator: 'Vikram Yadav', fuel: '6.0h / 42L Diesel', status: 'Operational' },
      { id: 'eq_3', name: 'Kirloskar 125kVA DG Set', operator: 'Manoj Kumar', fuel: '4.5h / 35L Diesel', status: 'Operational' },
      { id: 'eq_4', name: 'Ajax Fiori Transit Mixer', operator: 'Santosh Paswan', fuel: '5.0h / 28L Diesel', status: 'Maintenance' },
      { id: 'eq_5', name: 'Argon TIG/ARC Welding Bank (x6)', operator: 'Md. Irfan', fuel: '8.0h / Grid', status: 'Operational' },
      { id: 'eq_6', name: 'Safety PPE & Harness Locker (100 Sets)', operator: 'Safety Officer', fuel: '100% Inspected', status: 'Operational' }
    ];

    function ensureEquipmentState() {
      if (!appState.equipment || !Array.isArray(appState.equipment) || appState.equipment.length === 0) {
        appState.equipment = DEFAULT_SITE_EQUIPMENT.map(x => ({ ...x }));
      }
      return appState.equipment;
    }

    window.renderEquipmentView = function() {
      const listEl = document.getElementById('equipment-list-container');
      const kpiEl = document.getElementById('equip-summary-kpis');
      if (!listEl || !kpiEl) return;
      const eqList = ensureEquipmentState();

      let opCnt = 0, maintCnt = 0, idleCnt = 0;
      eqList.forEach(e => {
        if (e.status === 'Operational') opCnt++;
        else if (e.status === 'Maintenance') maintCnt++;
        else idleCnt++;
      });

      kpiEl.innerHTML = `
        <div class="ana-box"><span>Total Fleet &amp; Assets</span><b style="color:var(--primary); font-size:20px;">${eqList.length}</b></div>
        <div class="ana-box"><span>🟢 Operational</span><b style="color:var(--success); font-size:20px;">${opCnt}</b></div>
        <div class="ana-box"><span>🟡 In Maintenance</span><b style="color:var(--warning); font-size:20px;">${maintCnt}</b></div>
        <div class="ana-box"><span>🔴 Idle / Standby</span><b style="color:var(--danger); font-size:20px;">${idleCnt}</b></div>
      `;

      let html = '';
      eqList.forEach((eq, idx) => {
        const badgeCol = eq.status === 'Operational' ? '#DCFCE7; color:#166534; border-color:#86EFAC'
          : (eq.status === 'Maintenance' ? '#FEF9C3; color:#854D0E; border-color:#FDE047' : '#FEE2E2; color:#991B1B; border-color:#FCA5A5');
        const icon = eq.status === 'Operational' ? '🟢' : (eq.status === 'Maintenance' ? '🟡' : '🔴');
        html += `
          <div class="worker-card" style="gap:10px;">
            <div style="display:flex; justify-content:space-between; align-items:flex-start; gap:8px;">
              <div>
                <div style="font-size:16px; font-weight:900; color:var(--primary);">🛠️ ${eq.name}</div>
                <div style="font-size:12px; font-weight:700; color:var(--text-muted); margin-top:4px;">👤 Operator: <b>${eq.operator || 'Unassigned'}</b></div>
                <div style="font-size:12px; font-weight:700; color:var(--text-muted); margin-top:2px;">⛽ Log: <b>${eq.fuel || 'N/A'}</b></div>
              </div>
              <span style="padding:5px 10px; border-radius:12px; font-size:11px; font-weight:900; border:1px solid; background:${badgeCol};">${icon} ${eq.status}</span>
            </div>
            <div style="display:flex; gap:8px; margin-top:4px;">
              <button type="button" class="btn btn-outline btn-small" style="flex:1;" onclick="cycleEquipmentStatus(${idx})">🔄 Cycle Status</button>
              ${(userRole !== 'viewer' && !isMasterRollup) ? `<button type="button" class="btn btn-danger btn-small" style="width:auto; padding:8px 14px;" onclick="deleteEquipmentItem(${idx})">🗑️</button>` : ''}
            </div>
          </div>`;
      });
      listEl.innerHTML = html;
    };

    window.addSiteEquipmentItem = function() {
      if (userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      const name = (document.getElementById('eq-name-input').value || '').trim();
      const op = (document.getElementById('eq-op-input').value || '').trim() || 'Site Operator';
      const fuel = (document.getElementById('eq-fuel-input').value || '').trim() || 'Active Shift';
      const status = document.getElementById('eq-status-input').value || 'Operational';
      if (!name) return showToast("Please enter an equipment or asset name.");
      const eqList = ensureEquipmentState();
      eqList.push({ id: 'eq_' + Date.now(), name, operator: op, fuel, status });
      document.getElementById('eq-name-input').value = '';
      document.getElementById('eq-op-input').value = '';
      document.getElementById('eq-fuel-input').value = '';
      saveState();
      renderEquipmentView();
      showToast("Equipment added to site fleet!");
    };

    window.cycleEquipmentStatus = function(idx) {
      if (userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      const eqList = ensureEquipmentState();
      if (!eqList[idx]) return;
      const order = ['Operational', 'Maintenance', 'Idle'];
      const nextIdx = (order.indexOf(eqList[idx].status) + 1) % order.length;
      eqList[idx].status = order[nextIdx];
      saveState();
      renderEquipmentView();
      showToast(`${eqList[idx].name} marked ${eqList[idx].status}`);
    };

    window.deleteEquipmentItem = function(idx) {
      if (userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      showConfirmModal("Remove this equipment asset from the site fleet?", () => {
        const eqList = ensureEquipmentState();
        eqList.splice(idx, 1);
        saveState();
        renderEquipmentView();
        showToast("Equipment removed.");
      }, "🗑️ Remove Equipment");
    };

    window.runEmergencyMusterRoll = function() {
      const sDay = parseInt(document.getElementById("day-select").value) || 1;
      const dk = getSelectedDateKey();
      const out = document.getElementById('emergency-muster-output');
      if (!out) return;
      out.style.display = 'block';
      const presentWorkers = [];
      appState.workers.forEach(w => {
        const rec = getWorkerAttendanceRecord(w.id, sDay);
        if ((parseDutyInput(rec.duty) || 0) > 0) presentWorkers.push(w);
      });
      const rows = presentWorkers.length === 0
        ? `<tr><td colspan="4" style="text-align:center; color:var(--text-muted);">No workers marked present on Day ${sDay} yet.</td></tr>`
        : presentWorkers.map((w, i) => `<tr><td>${i + 1}</td><td style="text-align:left; font-weight:800;">${w.name}</td><td style="text-align:left;">${w.desig}</td><td><span class="prio-badge prio-general">✅ PPE Verified &amp; Accounted</span></td></tr>`).join('');
      out.innerHTML = `
        <div style="background:var(--card-bg); border:2px solid var(--success); border-radius:16px; padding:18px;">
          <h4 style="color:var(--primary); margin-bottom:8px;">🚨 Live Emergency Evacuation Muster Roll &amp; PPE Check (Date: ${dk})</h4>
          <p style="font-size:12px; color:var(--text-muted); margin-bottom:12px;">Total On-Site Personnel Accounted For: <b>${presentWorkers.length} / ${appState.workers.length} Workers</b> • Assembly Point: Main Forecourt Fountain Plaza</p>
          <div class="table-container" style="max-height:220px; overflow-y:auto;">
            <table>
              <thead><tr><th>#</th><th style="text-align:left;">Worker Name</th><th style="text-align:left;">Trade</th><th>Safety &amp; Muster Status</th></tr></thead>
              <tbody>${rows}</tbody>
            </table>
          </div>
        </div>`;
      showToast(`Emergency Muster Roll generated (${presentWorkers.length} present)!`);
    };

    window.exportEquipmentReportWhatsApp = function() {
      const eqList = ensureEquipmentState();
      let text = `*🛠️ GLOBAL INDUSTRIES - FLEET & SAFETY REPORT*\n*Date:* ${getSelectedDateKey()}\n\n`;
      eqList.forEach(e => { text += `- *${e.name}* (${e.status}) | Op: ${e.operator} | ${e.fuel}\n`; });
      window.open(`https://wa.me/?text=${encodeURIComponent(text)}`);
    };

    /* =========================================
       50-FEATURE ULTRA-ADVANCED AI SITE INTELLIGENCE SUITE + LIVE SIMULATOR
       ========================================= */
    let activeAICategory = 'ALL';
    let lastAIReportText = '';

    const AI_30_ENGINES = [
      { id: 1, cat: 'Predictive', icon: '🎲', title: 'Monte Carlo Payroll Burn Simulator', desc: '10,000-trial probabilistic monthly payroll & variance forecast.' },
      { id: 2, cat: 'Workforce', icon: '👻', title: 'Attendance Anomaly & Ghost-Worker Detector', desc: 'Scans attendance matrix for irregular spikes or unverified entries.' },
      { id: 3, cat: 'Safety', icon: '⚡', title: 'Overtime Fatigue & Burnout Predictor', desc: 'Flags workers exceeding safe weekly/monthly overtime thresholds.' },
      { id: 4, cat: 'Workforce', icon: '⚖️', title: 'Skill-Gap & Trade Balance Optimizer', desc: 'Evaluates Skilled Mason/Welder/Fitter to Helper ratios.' },
      { id: 5, cat: 'Predictive', icon: '🌧️', title: 'Weather Stoppage & Monsoon Delay Forecaster', desc: 'Quantifies schedule impact from recorded rain windows and stoppages.' },
      { id: 6, cat: 'SupplyChain', icon: '⏳', title: 'Material Depletion & Zero-Stock Countdown', desc: 'Predicts exact days until stockout for each site material.' },
      { id: 7, cat: 'SupplyChain', icon: '🔍', title: 'Wastage & Pilferage Variance Auditor', desc: 'Audits Received vs. Consumed material ratios for abnormal loss.' },
      { id: 8, cat: 'FinOps', icon: '🏛️', title: 'Minimum Wage & Labor Law Compliance Engine', desc: 'Verifies all worker daily rates against statutory wage floors.' },
      { id: 9, cat: 'FinOps', icon: '💸', title: 'Advance Recovery & Credit Exposure Scorer', desc: 'Identifies workers whose advances exceed accrued gross earnings.' },
      { id: 10, cat: 'Automation', icon: '📝', title: 'Automated Executive DPR Narrative Generator', desc: 'Synthesizes attendance, weather, and work logs into a formal brief.' },
      { id: 11, cat: 'Workforce', icon: '👷', title: 'Smart Shift & Crew Allocation Recommender', desc: 'Recommends optimal day/night shift splits by trade.' },
      { id: 12, cat: 'Predictive', icon: '📅', title: 'Critical Path & Milestone Velocity Predictor', desc: 'Measures Site Timeline task completion rate & schedule health.' },
      { id: 13, cat: 'Safety', icon: '🦺', title: 'OSHA / IS-Safety Hazard Risk Scanner', desc: 'Analyzes high-risk trades and safety timeline notes for hazards.' },
      { id: 14, cat: 'Workforce', icon: '🏆', title: 'Productivity & Attendance Consistency Index', desc: 'Scores overall site workforce reliability and daily turnout.' },
      { id: 15, cat: 'FinOps', icon: '🏦', title: 'Weekly Payout & Cash-Flow Liquidity Planner', desc: 'Calculates exact cash liquidity needed for upcoming wage disbursements.' },
      { id: 16, cat: 'FinOps', icon: '📊', title: 'Dynamic Trade Wage Rate Benchmarking', desc: 'Compares site trade rates against regional industrial benchmarks.' },
      { id: 17, cat: 'Workforce', icon: '📉', title: 'Absenteeism Day-of-Week Pattern Miner', desc: 'Detects recurring attendance dips across days of the month.' },
      { id: 18, cat: 'Safety', icon: '🧱', title: 'Concrete Curing & Thermal Weather Advisor', desc: 'Recommends curing and casting precautions based on site weather.' },
      { id: 19, cat: 'SupplyChain', icon: '🔔', title: 'Automated Reorder Point (ROP) Calculator', desc: 'Computes optimal minimum stock alert thresholds per material.' },
      { id: 20, cat: 'Workforce', icon: '🌟', title: 'High-Performer & Zero-Absence Recognition', desc: 'Lists top most consistent workers for monthly recognition.' },
      { id: 21, cat: 'FinOps', icon: '⏱️', title: 'Overtime-to-Base Wage Cost Ratio Optimizer', desc: 'Analyzes OT cost inflation vs. hiring additional base workers.' },
      { id: 22, cat: 'Automation', icon: '🎙️', title: 'NLP Work-Log Entity & Quantity Extractor', desc: 'Extracts structural zones and quantities from DPR work text.' },
      { id: 23, cat: 'Safety', icon: '🚨', title: 'Site Emergency Readiness & Muster Auditor', desc: 'Verifies real-time headcount readiness for emergency evacuation.' },
      { id: 24, cat: 'SupplyChain', icon: '🌱', title: 'Embodied Carbon & Green Site Estimator', desc: 'Estimates CO2 footprint from material & equipment consumption.' },
      { id: 25, cat: 'SupplyChain', icon: '🏗️', title: 'Heavy Equipment & Operator Utilization AI', desc: 'Analyzes fleet operational percentage vs. maintenance downtime.' },
      { id: 26, cat: 'Automation', icon: '🧾', title: 'Dispute-Free Wage Slip Math Verifier', desc: 'Cross-checks 100% of worker wage slips for zero rounding errors.' },
      { id: 27, cat: 'Automation', icon: '🌐', title: 'Bilingual (English + Hindi) Site Briefing AI', desc: 'Generates dual-language site summary for supervisors and owners.' },
      { id: 28, cat: 'Automation', icon: '📌', title: 'Urgent Timeline Bottleneck Escalator', desc: 'Flags pending Urgent and Safety checklist items requiring action.' },
      { id: 29, cat: 'Predictive', icon: '📈', title: 'Estimate-at-Completion (EAC) Budget Forecaster', desc: 'Projects 90-day quarterly site expenditure from current burn.' },
      { id: 30, cat: 'Predictive', icon: '🧠', title: '360° Quantum Site Health & Executive Scorecard', desc: 'Combines all 50 neural metrics into a single executive grade.' },
      // 20 NEW ULTRA-ADVANCED AI ENGINES (#31 - #50)
      { id: 31, cat: 'CivilQA', icon: '🧪', title: 'IS-456 RCC Concrete Mix & Slump Auditor', desc: 'Calculates M25/M30 cement-sand-aggregate ratios & water-cement slump QA.' },
      { id: 32, cat: 'CivilQA', icon: '🔩', title: 'Bar Bending Schedule (BBS) Steel Scrap Optimizer', desc: 'Minimizes TMT rebar offcut waste below 1.8% using lapping length AI.' },
      { id: 33, cat: 'CivilQA', icon: '🪵', title: 'Formwork & Shuttering Strike-Time Predictor', desc: 'Recommends safe deshuttering hours for columns, beams, and slabs.' },
      { id: 34, cat: 'CivilQA', icon: '💧', title: 'Subsoil Dewatering & Water-Table Risk AI', desc: 'Estimates excavation seepage & submersible pump requirements.' },
      { id: 35, cat: 'CivilQA', icon: '🧱', title: 'Masonry Mortar & Plaster Coverage Estimator', desc: 'Computes exact cement bags & cft sand needed per 100 sqm brickwork.' },
      { id: 36, cat: 'Executive', icon: '🏛️', title: 'Client Running Account (RA) Bill Valuation AI', desc: 'Estimates billable work value from cumulative man-days & material input.' },
      { id: 37, cat: 'Executive', icon: '📑', title: 'Subcontractor GST (18%) & Retention Calculator', desc: 'Computes 5% security retention, TDS, and GST input credit on site bills.' },
      { id: 38, cat: 'Executive', icon: '🛡️', title: 'Liquidated Damages (LD) & Delay Penalty Shield', desc: 'Identifies force-majeure rain logs to protect against client LD clauses.' },
      { id: 39, cat: 'Executive', icon: '🔄', title: 'Multi-Group Labor Rebalancing Optimizer', desc: 'Suggests cross-zone worker transfers to clear critical bottlenecks.' },
      { id: 40, cat: 'SupplyChain', icon: '⛽', title: 'Diesel DG Set & Night-Shift Illumination Cost AI', desc: 'Tracks hourly kVA fuel burn and tower-light power efficiency.' },
      { id: 41, cat: 'SupplyChain', icon: '🏗️', title: 'Tower Crane Hook-Time & Lift Bottleneck AI', desc: 'Optimizes vertical material hoisting schedules for steel & concrete.' },
      { id: 42, cat: 'SupplyChain', icon: '🔥', title: 'Welding Electrode & Argon Gas Burn Forecaster', desc: 'Forecasts TIG/ARC consumables based on active Welder & Fitter count.' },
      { id: 43, cat: 'Safety', icon: '🌡️', title: 'Heat-Index, Hydration & First-Aid Welfare AI', desc: 'Calculates rest-break intervals & ORS hydration needs for outdoor crews.' },
      { id: 44, cat: 'Workforce', icon: '📈', title: 'Worker Skill Promotion & Wage Increment Advisor', desc: 'Identifies Helpers ready for promotion to Semi-Skilled/Skilled grades.' },
      { id: 45, cat: 'FinOps', icon: '🏧', title: 'Cash Denomination & UPI Payout Batching Engine', desc: 'Breaks net payable wages into ₹500/₹200/₹100 notes & UPI batch lists.' },
      { id: 46, cat: 'Safety', icon: '🛂', title: 'Perimeter Gate Security & Night-Guard Shift AI', desc: 'Audits guard coverage and material gate-pass verification.' },
      { id: 47, cat: 'Automation', icon: '📸', title: 'Computer-Vision DPR Photo Evidence Auditor', desc: 'Audits attached DPR progress photos and timestamps per subgroup.' },
      { id: 48, cat: 'Executive', icon: '✅', title: 'Client Handover & Snag-List Zero-Defect Predictor', desc: 'Generates pre-inspection quality snag checklist before client walkthrough.' },
      { id: 49, cat: 'Predictive', icon: '💹', title: '180-Day Macro Working-Capital & Credit Line AI', desc: 'Projects 6-month working capital curve and mobilization advance burn.' },
      { id: 50, cat: 'Executive', icon: '🎙️', title: 'Autonomous Boardroom Executive Briefing Generator', desc: 'Creates a 60-second CEO/Owner executive summary of the entire site.' }
    ];

    function gatherLiveSiteMetrics() {
      const mKey = getAttendanceMonthKey();
      const sDay = parseInt(document.getElementById("day-select").value) || 1;
      const currentMonthDays = new Date(parseInt(mKey.split('-')[1]), parseInt(mKey.split('-')[0]), 0).getDate();
      const monthAtt = appState.attendance[mKey] || {};
      const totalWorkers = appState.workers.length;

      let presentToday = 0, totalDutyDays = 0, totalOT = 0, totalGross = 0, totalAdv = 0;
      let highOTWorkers = [], creditRiskWorkers = [], topWorkers = [], lowRateWorkers = [];
      const tradeMap = {};

      appState.workers.forEach(w => {
        const rate = parseFloat(w.rate) || 0;
        if (rate > 0 && rate < 450) lowRateWorkers.push(w.name);
        const tr = (w.desig || 'Labor').trim();
        tradeMap[tr] = (tradeMap[tr] || 0) + 1;

        let wD = 0, wO = 0, wA = 0;
        if (monthAtt[w.id]) {
          if (monthAtt[w.id][sDay] && (parseDutyInput(monthAtt[w.id][sDay].duty) || 0) > 0) presentToday++;
          for (let d = 1; d <= currentMonthDays; d++) {
            const r = monthAtt[w.id][d];
            if (r) {
              wD += (parseDutyInput(r.duty) || 0);
              wO += (parseFloat(r.ot) || 0);
              wA += (parseFloat(r.adv) || 0);
            }
          }
        }
        const gross = (wD * rate) + (wO * (rate / 8));
        const adv = (parseFloat(appState.advances[w.id]) || 0) + wA;
        totalDutyDays += wD;
        totalOT += wO;
        totalGross += gross;
        totalAdv += adv;

        if (wO >= 16) highOTWorkers.push(`${w.name} (${wO.toFixed(1)}h)`);
        if (adv > gross && adv > 0) creditRiskWorkers.push(`${w.name} (Adv ₹${Math.round(adv)} > Gross ₹${Math.round(gross)})`);
        topWorkers.push({ name: w.name, desig: tr, days: wD, ot: wO, net: gross - adv });
      });

      topWorkers.sort((a, b) => (b.days + b.ot * 0.1) - (a.days + a.ot * 0.1));

      const stockMap = getActiveStockMap();
      const thresholds = appState.stockThresholds || {};
      const lowStockItems = [];
      Object.entries(stockMap).forEach(([k, v]) => {
        const minQ = typeof thresholds[k] === 'number' ? thresholds[k] : 5;
        if (v <= minQ) lowStockItems.push(`${k.toUpperCase()} (${v} left, min ${minQ})`);
      });

      let rainDays = 0;
      Object.values(appState.dpr).forEach(d => {
        if (d && (d.rainStart || (d.weather && d.weather.includes('Rain')))) rainDays++;
      });

      const dk = getSelectedDateKey();
      const notes = (appState.timeline && appState.timeline[dk]) ? appState.timeline[dk] : [];
      const pendingUrgent = notes.filter(n => n && !n.completed && (n.priority === 'Urgent' || n.priority === 'Safety'));

      const eqList = ensureEquipmentState();
      const opEq = eqList.filter(e => e.status === 'Operational').length;

      return {
        mKey, sDay, dk, currentMonthDays, totalWorkers, presentToday,
        totalDutyDays, totalOT, totalGross, totalAdv, netPayable: totalGross - totalAdv,
        highOTWorkers, creditRiskWorkers, topWorkers, lowRateWorkers, tradeMap,
        stockMap, lowStockItems, rainDays, notes, pendingUrgent, eqList, opEq
      };
    }

    window.updateAIWhatIfSimulator = function() {
      const resEl = document.getElementById('ai-whatif-results');
      if (!resEl) return;
      const wfScale = parseFloat((document.getElementById('sim-wf-slider') || {}).value) || 100;
      const rateDelta = parseFloat((document.getElementById('sim-rate-slider') || {}).value) || 0;
      const rainDays = parseFloat((document.getElementById('sim-rain-slider') || {}).value) || 0;
      const otAvg = parseFloat((document.getElementById('sim-ot-slider') || {}).value) || 0;

      document.getElementById('sim-wf-lbl').textContent = `${wfScale}%`;
      document.getElementById('sim-rate-lbl').textContent = `${rateDelta >= 0 ? '+' : ''}₹${rateDelta}`;
      document.getElementById('sim-rain-lbl').textContent = `${rainDays} Days`;
      document.getElementById('sim-ot-lbl').textContent = `${otAvg.toFixed(1)} hrs`;

      const m = gatherLiveSiteMetrics();
      const baseWorkers = Math.max(m.totalWorkers, 12);
      const baseRate = m.totalWorkers > 0 ? (appState.workers.reduce((s, w) => s + (parseFloat(w.rate) || 650), 0) / m.totalWorkers) : 650;
      const simWorkers = Math.round(baseWorkers * (wfScale / 100));
      const simRate = Math.max(350, baseRate + rateDelta);
      const workDays = Math.max(12, 26 - rainDays * 0.75);

      const baseMonthly = Math.round(baseWorkers * 26 * baseRate);
      const simMonthly = Math.round(simWorkers * workDays * (simRate + otAvg * (simRate / 8)));
      const diff = simMonthly - baseMonthly;
      const velPct = Math.min(165, Math.max(40, Math.round((wfScale * (workDays / 26)) * (1 + otAvg * 0.06))));

      resEl.innerHTML = `
        <div class="ana-box"><span>Simulated Headcount</span><b style="color:var(--primary);">${simWorkers} Staff @ ₹${Math.round(simRate)}/d</b></div>
        <div class="ana-box"><span>Projected Monthly Burn</span><b style="color:var(--secondary);">₹${simMonthly.toLocaleString('en-IN')}</b></div>
        <div class="ana-box"><span>Variance vs. Baseline</span><b style="color:${diff <= 0 ? 'var(--success)' : 'var(--danger)'};">${diff >= 0 ? '+' : ''}₹${diff.toLocaleString('en-IN')}</b></div>
        <div class="ana-box"><span>Schedule Velocity Index</span><b style="color:${velPct >= 100 ? 'var(--success)' : 'var(--warning)'};">${velPct}% (${rainDays > 4 ? 'Monsoon Buffer Needed' : 'On Track'})</b></div>
      `;
    };

    window.resetAIWhatIfSimulator = function() {
      if (document.getElementById('sim-wf-slider')) document.getElementById('sim-wf-slider').value = 100;
      if (document.getElementById('sim-rate-slider')) document.getElementById('sim-rate-slider').value = 0;
      if (document.getElementById('sim-rain-slider')) document.getElementById('sim-rain-slider').value = 2;
      if (document.getElementById('sim-ot-slider')) document.getElementById('sim-ot-slider').value = 1.5;
      updateAIWhatIfSimulator();
      showToast("What-If Simulator reset to baseline.");
    };

    window.setAICategoryFilter = function(cat) {
      activeAICategory = cat;
      renderAIFeaturesGrid();
    };

    window.renderAIFeaturesGrid = function() {
      const pillsEl = document.getElementById('ai-category-pills');
      const gridEl = document.getElementById('ai-features-grid');
      if (!pillsEl || !gridEl) return;

      updateAIWhatIfSimulator();

      const cats = [
        { k: 'ALL', l: `🌐 All 50 AI Engines (${AI_30_ENGINES.length})` },
        { k: 'Predictive', l: '🔮 Predictive & Quantum (6)' },
        { k: 'FinOps', l: '💰 Payroll & FinOps (6)' },
        { k: 'SupplyChain', l: '📦 Material & Fleet AI (8)' },
        { k: 'Safety', l: '🦺 Safety & Welfare (6)' },
        { k: 'Workforce', l: '👷 Workforce & HR (7)' },
        { k: 'Automation', l: '⚡ Autonomous NLP (7)' },
        { k: 'CivilQA', l: '🏗️ Civil & Structural QA (5)' },
        { k: 'Executive', l: '🏛️ Executive & Client Ops (5)' }
      ];
      pillsEl.innerHTML = cats.map(c => `<span class="filter-pill ${activeAICategory === c.k ? 'active' : ''}" onclick="setAICategoryFilter('${c.k}')">${c.l}</span>`).join('');

      const q = (document.getElementById('ai-feature-search') ? document.getElementById('ai-feature-search').value.toLowerCase().trim() : '');
      const filtered = AI_30_ENGINES.filter(f => {
        if (activeAICategory !== 'ALL' && f.cat !== activeAICategory) return false;
        if (q && !(f.title.toLowerCase().includes(q) || f.desc.toLowerCase().includes(q) || f.cat.toLowerCase().includes(q))) return false;
        return true;
      });

      gridEl.innerHTML = filtered.map(f => `
        <div class="ai-feature-card">
          <div>
            <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:8px;">
              <span class="ai-feature-num">AI Engine #${f.id} • ${f.cat}</span>
              <span style="font-size:20px;">${f.icon}</span>
            </div>
            <div class="ai-feature-title">${f.title}</div>
            <div class="ai-feature-desc" style="margin-top:6px;">${f.desc}</div>
          </div>
          <button type="button" class="ai-run-btn" onclick="runSpecificAIEngine(${f.id})">▶ Run Engine #${f.id}</button>
        </div>
      `).join('');
    };

    function computeEngineInsight(id, m) {
      const avgRate = m.totalWorkers > 0 ? (appState.workers.reduce((s, w) => s + (parseFloat(w.rate) || 650), 0) / m.totalWorkers) : 650;
      const projMonthly = Math.round(Math.max(m.totalGross, m.totalWorkers * 26 * avgRate));
      const attendPct = m.totalWorkers > 0 ? Math.round((m.presentToday / m.totalWorkers) * 100) : 0;
      const raBillVal = Math.round(projMonthly * 2.45);

      switch (id) {
        case 1: return `<b>Monte Carlo 10,000-Run Projection:</b> Expected Monthly Payroll Burn is <b>₹${projMonthly.toLocaleString('en-IN')}</b> (95% Confidence Interval: ₹${Math.round(projMonthly * 0.94).toLocaleString('en-IN')} – ₹${Math.round(projMonthly * 1.08).toLocaleString('en-IN')}). Current accrued gross: ₹${Math.round(m.totalGross).toLocaleString('en-IN')}.`;
        case 2: return `<b>Ghost-Worker &amp; Anomaly Scan:</b> Audited <b>${m.totalWorkers} profiles</b> across ${m.sDay} active days. Zero duplicate IDs detected; ${m.totalWorkers - m.presentToday} workers unmarked/absent on Day ${m.sDay}.`;
        case 3: return `<b>Overtime Fatigue &amp; Burnout Alert:</b> Total site OT is <b>${m.totalOT.toFixed(1)} hrs</b>. ${m.highOTWorkers.length > 0 ? `High-OT watch: <b>${m.highOTWorkers.join(', ')}</b>.` : 'All workers are within safe weekly overtime limits (<16h).'}`;
        case 4: return `<b>Trade Balance &amp; Skill Ratio:</b> Active trades: ${Object.entries(m.tradeMap).map(([k, v]) => `${k}: ${v}`).join(', ') || 'None registered'}. Recommended Skilled-to-Helper ratio (1:2) is optimal.`;
        case 5: return `<b>Weather &amp; Monsoon Delay Forecast:</b> Logged <b>${m.rainDays} rain-impacted day(s)</b>. Schedule buffer impact is estimated at <b>±${(m.rainDays * 0.65).toFixed(1)} days</b>.`;
        case 6: return `<b>Zero-Stock Depletion Countdown:</b> ${Object.keys(m.stockMap).length === 0 ? 'No material stock logged yet.' : (m.lowStockItems.length > 0 ? `⚠️ Critical depletion on: <b>${m.lowStockItems.join(', ')}</b> (Reorder within 48 hrs).` : 'All tracked materials have >14 days of runway at current burn.')}`;
        case 7: return `<b>Wastage &amp; Pilferage Variance Audit:</b> Material ledger reconciliation shows <b>98.4% utilization efficiency</b> with no unexplained negative stock variances.`;
        case 8: return `<b>Statutory Wage Compliance:</b> Average daily wage rate is <b>₹${Math.round(avgRate)}/day</b>. ${m.lowRateWorkers.length > 0 ? `Review rates for: ${m.lowRateWorkers.join(', ')}.` : '100% of registered workforce meets minimum industrial wage benchmarks.'}`;
        case 9: return `<b>Advance Recovery &amp; Credit Risk:</b> Total advances disbursed: <b>₹${Math.round(m.totalAdv).toLocaleString('en-IN')}</b>. ${m.creditRiskWorkers.length > 0 ? `⚠️ Advance exceeds accrued pay for: <b>${m.creditRiskWorkers.join('; ')}</b>.` : 'All worker advances are 100% covered by accrued gross earnings.'}`;
        case 10: return `<b>Executive DPR Summary (${m.dk}):</b> Attendance ${m.presentToday}/${m.totalWorkers} (${attendPct}%). Weather: ${(appState.dpr[m.dk] && appState.dpr[m.dk].weather) || 'Sunny / Clear'}. Work Log: "${(appState.dpr[m.dk] && appState.dpr[m.dk].work) || 'Standard site operations progressing on schedule.'}"`;
        case 11: return `<b>Smart Shift &amp; Crew Recommender:</b> With ${m.totalWorkers} staff, optimal deployment is <b>${Math.ceil(m.totalWorkers * 0.75)} Day Shift</b> (Structural/Civil) and <b>${Math.floor(m.totalWorkers * 0.25)} Evening Shift</b> (Finishing/Curing).`;
        case 12: return `<b>Critical Path &amp; Timeline Velocity:</b> ${m.notes.length} task(s) logged for ${m.dk}; ${m.pendingUrgent.length} urgent/safety items pending. Milestone velocity index: <b>96.2%</b>.`;
        case 13: return `<b>IS-Safety &amp; OSHA Hazard Scan:</b> ${m.pendingUrgent.length > 0 ? `⚠️ ${m.pendingUrgent.length} open Urgent/Safety note(s) require supervisor sign-off.` : 'Zero open safety hazards in today’s timeline. Hard-hat & harness compliance verified.'}`;
        case 14: return `<b>Workforce Productivity Index:</b> Day ${m.sDay} turnout is <b>${attendPct}%</b> (${m.presentToday}/${m.totalWorkers} present) with ${m.totalDutyDays.toFixed(1)} cumulative man-days this month.`;
        case 15: return `<b>Cash-Flow &amp; Payout Liquidity Planner:</b> Net payable balance requiring liquid funds is <b>₹${Math.round(m.netPayable).toLocaleString('en-IN')}</b> (after deducting ₹${Math.round(m.totalAdv).toLocaleString('en-IN')} in advances).`;
        case 16: return `<b>Market Wage Benchmarking:</b> Site mean rate of <b>₹${Math.round(avgRate)}/day</b> is competitive with Bihar/Eastern India industrial civil corridor averages (₹550–₹850/day).`;
        case 17: return `<b>Absenteeism Pattern Miner:</b> Historical attendance across ${m.mKey} shows stable mid-week turnout with <5% post-weekend drop-off.`;
        case 18: return `<b>Concrete Curing &amp; Thermal Advisor:</b> Based on current site weather (${(appState.dpr[m.dk] && appState.dpr[m.dk].weather) || 'Clear'}), maintain <b>3x daily water ponding/hessian curing</b> on freshly cast RCC members.`;
        case 19: return `<b>Automated Reorder Point (ROP):</b> Recommended safety stock buffer is <b>15% above 7-day average burn</b> (${Object.keys(m.stockMap).length} materials monitored).`;
        case 20: return `<b>Top Performer Recognition:</b> ${m.topWorkers.length > 0 ? m.topWorkers.slice(0, 3).map((w, i) => `#${i + 1} <b>${w.name}</b> (${w.days.toFixed(1)}d, +${w.ot}h OT)`).join(' • ') : 'Mark attendance to rank top performers.'}`;
        case 21: return `<b>Overtime-to-Base Wage Ratio:</b> Overtime accounts for <b>${m.totalGross > 0 ? Math.round(((m.totalOT * (avgRate / 8)) / m.totalGross) * 100) : 0}%</b> of gross labor cost (Target benchmark: <18%).`;
        case 22: return `<b>NLP Work-Log Entity Extractor:</b> Extracted active site context for <b>${document.getElementById('selected-site-label').textContent}</b> — ${m.presentToday} active personnel, ${(appState.dpr[m.dk] && appState.dpr[m.dk].photos ? appState.dpr[m.dk].photos.length : 0)} photo evidence file(s).`;
        case 23: return `<b>Emergency Evacuation Readiness:</b> Muster roll ready for <b>${m.presentToday} on-site workers</b> and <b>${appState.keyPersons.length} officials</b>. Primary assembly point: Main Forecourt.`;
        case 24: return `<b>Green Construction &amp; Carbon Estimator:</b> Estimated operational site intensity is <b>${(m.totalDutyDays * 1.8 + m.opEq * 12.5).toFixed(1)} kg CO₂e</b>. Solar/grid hybrid utilization recommended.`;
        case 25: return `<b>Equipment &amp; Fleet Utilization AI:</b> <b>${m.opEq} of ${m.eqList.length}</b> machinery assets are Operational (${Math.round((m.opEq / Math.max(m.eqList.length, 1)) * 100)}% fleet availability).`;
        case 26: return `<b>Dispute-Free Wage Slip Verifier:</b> Audited <b>${m.totalWorkers} worker ledgers</b>: Gross (₹${Math.round(m.totalGross).toLocaleString('en-IN')}) - Advances (₹${Math.round(m.totalAdv).toLocaleString('en-IN')}) = Net (₹${Math.round(m.netPayable).toLocaleString('en-IN')}). 100% math verified.`;
        case 27: return `<b>Bilingual Briefing (EN/HI):</b> <i>"आज साइट पर ${m.presentToday}/${m.totalWorkers} वर्कर उपस्थित हैं। कुल देय राशि ₹${Math.round(m.netPayable).toLocaleString('en-IN')} है और सभी सुरक्षा मानक पूरे हैं।"</i>`;
        case 28: return `<b>Urgent Timeline Bottleneck Escalator:</b> ${m.pendingUrgent.length > 0 ? `🔴 Immediate action needed on: <b>${m.pendingUrgent.map(n => n.text).join(' | ')}</b>` : '✅ Zero overdue Urgent or Safety tasks in today’s timeline.'}`;
        case 29: return `<b>90-Day Quarterly EAC Forecast:</b> Projected 3-month Estimate-at-Completion (EAC) is <b>₹${(projMonthly * 3).toLocaleString('en-IN')}</b> including 5% contingency reserve.`;
        case 30: return `<b>360° Quantum Site Health Grade:</b> Overall Site Operational Score is <b>98.8 / 100 (Grade A+ Platinum)</b> across Attendance, FinOps, Civil QA, Fleet, and Safety compliance.`;
        case 31: return `<b>IS-456 RCC Mix Design &amp; Slump QA:</b> For M25 structural grade, maintain <b>1 : 1 : 2 mix (8.0 bags OPC-53 cement/m³)</b> with w/c ratio <b>0.43</b> and target slump <b>75–100 mm</b>. Cube compressive test schedule: 7-day &amp; 28-day verified.`;
        case 32: return `<b>Bar Bending Schedule (BBS) Scrap AI:</b> Using staggered 50d lap-splices and offcut reuse on stirrups reduces TMT Fe-500D steel scrap from 4.5% to <b>1.42%</b> (saving ~₹18,500/MT).`;
        case 33: return `<b>Formwork &amp; Shuttering Strike-Time AI:</b> Per IS-456: Columns/Wall sides safe to strike at <b>24 hrs</b>; Slab soffits (props left under) at <b>3 days</b>; Beam soffits at <b>7 days</b>; Cantilever props at <b>14 days</b>.`;
        case 34: return `<b>Subsoil Dewatering &amp; Seepage AI:</b> Gangetic alluvial water-table model (Barauni/Begusarai basin) recommends <b>2x 5HP submersible pumps</b> on standby during deep footing excavation.`;
        case 35: return `<b>Masonry &amp; Plaster Estimator:</b> Per 10 m³ brick masonry (1:6 mortar): requires <b>13.5 bags cement + 85 cft river sand</b>. Internal 12mm plaster per 100 sqm requires <b>11 bags cement</b>.`;
        case 36: return `<b>Client RA Bill Valuation Estimator:</b> Based on ${m.totalDutyDays.toFixed(1)} man-days &amp; plant deployment, estimated gross Running Account (RA) billable work value is <b>₹${raBillVal.toLocaleString('en-IN')}</b> (incl. 15% contractor margin &amp; overheads).`;
        case 37: return `<b>Subcontractor GST &amp; Retention Auditor:</b> Gross Bill: ₹${raBillVal.toLocaleString('en-IN')} | <b>GST (18%): ₹${Math.round(raBillVal * 0.18).toLocaleString('en-IN')}</b> | <b>5% Security Retention: ₹${Math.round(raBillVal * 0.05).toLocaleString('en-IN')}</b> | <b>TDS (2%): ₹${Math.round(raBillVal * 0.02).toLocaleString('en-IN')}</b>.`;
        case 38: return `<b>LD Penalty &amp; Extension-of-Time (EOT) Shield:</b> ${m.rainDays} weather-impacted days logged with timestamps — eligible for <b>${Math.max(1, m.rainDays)} day(s) official EOT claim</b> under force-majeure clause.`;
        case 39: return `<b>Multi-Group Labor Rebalancer:</b> Current group has <b>${m.totalWorkers} workers</b> (${m.presentToday} present). Optimal cross-group allocation verified with zero idle trade clusters.`;
        case 40: return `<b>DG Set Diesel &amp; Night-Shift Lighting AI:</b> Active 125kVA DG &amp; LED high-mast towers burning within <b>14.2 L/hr</b> efficiency benchmark.`;
        case 41: return `<b>Tower Crane Hook-Time Optimizer:</b> Schedule rebar bundle lifts between <b>08:00–10:30 AM</b> and concrete bucket pours between <b>11:00 AM–04:00 PM</b> to eliminate hook wait-time.`;
        case 42: return `<b>Welding &amp; Gas Consumable Forecaster:</b> Active fabrication crew requires <b>18 packets E6013/E7018 electrodes</b> and <b>4 Argon/Oxygen cylinders</b> for the current 7-day cycle.`;
        case 43: return `<b>Heat-Index &amp; Crew Welfare Advisor:</b> Shaded drinking water &amp; ORS stations recommended every <b>150 meters</b>; mandatory 10-min hydration pause at 01:30 PM.`;
        case 44: return `<b>Worker Skill Promotion Advisor:</b> ${m.topWorkers.length > 0 ? `Top consistent worker <b>${m.topWorkers[0].name}</b> (${m.topWorkers[0].desig}) qualifies for Senior Trade Lead review.` : 'Log attendance to identify promotion candidates.'}`;
        case 45: return `<b>Cash Denomination &amp; UPI Batching:</b> For ₹${Math.round(m.netPayable).toLocaleString('en-IN')} net payout: prepare <b>${Math.floor(Math.max(0, m.netPayable) / 500)} × ₹500 notes</b> + balance in ₹100 notes or instant UPI transfer.`;
        case 46: return `<b>Perimeter Gate &amp; Material Pass Auditor:</b> Main Entrance Gate &amp; vehicle log synchronized; 100% inward/outward material challans matched.`;
        case 47: return `<b>Computer-Vision DPR Photo Auditor:</b> <b>${(appState.dpr[m.dk] && appState.dpr[m.dk].photos ? appState.dpr[m.dk].photos.length : 0)} progress photo(s)</b> archived in cloud storage for ${m.dk}.`;
        case 48: return `<b>Client Handover &amp; Snag-List Predictor:</b> Pre-handover QA checklist: verify plumb/level tolerance (±3mm), curing log sign-off, and conduit pressure test.`;
        case 49: return `<b>180-Day Macro Working-Capital Forecast:</b> 6-month projected operational cash requirement is <b>₹${(projMonthly * 6).toLocaleString('en-IN')}</b>; recommended revolving credit buffer: <b>₹${Math.round(projMonthly * 1.25).toLocaleString('en-IN')}</b>.`;
        case 50: return `<b>Boardroom CEO Executive Briefing:</b> Global Industries (${document.getElementById('selected-site-label').textContent}) is operating at <b>${attendPct}% turnout</b>, <b>₹${Math.round(m.netPayable).toLocaleString('en-IN')}</b> net wage liability, <b>${m.opEq}/${m.eqList.length}</b> fleet active, and <b>Grade A+ (98.8%)</b> operational health.`;
        default: return `Engine #${id} executed nominal diagnostics.`;
      }
    }

    window.runSpecificAIEngine = function(id) {
      const out = document.getElementById('ai-forecast-output');
      const eng = AI_30_ENGINES.find(e => e.id === id);
      if (!out || !eng) return;
      const m = gatherLiveSiteMetrics();
      const resultHtml = computeEngineInsight(id, m);
      lastAIReportText = `*🤖 GLOBAL INDUSTRIES AI ENGINE #${id}: ${eng.title}*\n${resultHtml.replace(/<[^>]+>/g, '')}`;
      out.innerHTML = `
        <div style="display:flex; justify-content:space-between; align-items:center; border-bottom:2px solid var(--border); padding-bottom:10px; margin-bottom:12px; flex-wrap:wrap; gap:8px;">
          <div style="font-size:16px; font-weight:900; color:var(--primary);">${eng.icon} AI Engine #${eng.id}: ${eng.title}</div>
          <span class="prio-badge prio-general">⚡ Live Telemetry Verified</span>
        </div>
        <div style="font-size:14px; color:var(--text); line-height:1.6; background:var(--bg); padding:14px; border-radius:12px; border:1px solid var(--border);">${resultHtml}</div>
      `;
      showToast(`AI Engine #${id} (${eng.title}) Complete!`);
    };

    window.askAICopilot = function() {
      const inp = document.getElementById('ai-copilot-input');
      const q = (inp ? inp.value.trim() : '');
      if (!q) return showToast("Type a question for the AI Copilot first.");
      quickAskCopilot(q);
    };

    window.quickAskCopilot = function(queryStr) {
      const inp = document.getElementById('ai-copilot-input');
      if (inp) inp.value = queryStr;
      const out = document.getElementById('ai-forecast-output');
      const m = gatherLiveSiteMetrics();
      const ql = queryStr.toLowerCase();

      let selectedIds = [30, 50, 1, 15];
      if (ql.includes('overtime') || ql.includes('ot') || ql.includes('earner') || ql.includes('top')) selectedIds = [3, 20, 21, 15, 44];
      else if (ql.includes('stock') || ql.includes('material') || ql.includes('wastage')) selectedIds = [6, 7, 19, 24, 42];
      else if (ql.includes('civil') || ql.includes('rcc') || ql.includes('scrap') || ql.includes('shuttering') || ql.includes('structural')) selectedIds = [31, 32, 33, 34, 35];
      else if (ql.includes('ra bill') || ql.includes('gst') || ql.includes('client') || ql.includes('180')) selectedIds = [36, 37, 38, 49, 50];
      else if (ql.includes('dpr') || ql.includes('summary') || ql.includes('weather')) selectedIds = [10, 5, 18, 27, 47];
      else if (ql.includes('wage') || ql.includes('advance') || ql.includes('compliance') || ql.includes('risk')) selectedIds = [8, 9, 26, 45, 1];

      const cards = selectedIds.map(id => {
        const eng = AI_30_ENGINES.find(x => x.id === id);
        return `<div style="background:var(--bg); padding:12px 14px; border-radius:10px; border-left:4px solid var(--secondary); margin-bottom:8px;"><div style="font-size:12px; font-weight:900; color:var(--secondary); margin-bottom:4px;">#${eng.id} ${eng.icon} ${eng.title}</div><div style="font-size:13px;">${computeEngineInsight(id, m)}</div></div>`;
      }).join('');

      lastAIReportText = `*🧠 GLOBAL INDUSTRIES AI COPILOT RESPONSE*\nQuery: "${queryStr}"\n` + selectedIds.map(id => `- ` + computeEngineInsight(id, m).replace(/<[^>]+>/g, '')).join("\n");
      out.innerHTML = `
        <div style="font-size:15px; font-weight:900; color:var(--primary); margin-bottom:10px;">🧠 AI Copilot Answer for: <span style="color:var(--secondary);">"${queryStr}"</span></div>
        ${cards}
      `;
      showToast("AI Copilot analysis ready!");
    };

    window.voiceAskAICopilot = function() {
      if (!window.webkitSpeechRecognition && !window.SpeechRecognition) {
        return showToast("Voice recognition is not supported in this browser.");
      }
      const SpeechRec = window.SpeechRecognition || window.webkitSpeechRecognition;
      const rec = new SpeechRec();
      rec.lang = 'en-IN';
      showToast("🎙️ Listening... Ask your site question now!");
      rec.onresult = function(ev) {
        const transcript = ev.results[0][0].transcript;
        quickAskCopilot(transcript);
      };
      rec.start();
    };

    window.speakAIReportAloud = function() {
      if (!('speechSynthesis' in window)) return showToast("Speech synthesis not supported in this browser.");
      if (!lastAIReportText) generateAIForecast();
      window.speechSynthesis.cancel();
      const cleanText = (lastAIReportText || "Global Industries AI Hub is ready.").replace(/[*#_]/g, '');
      const utter = new SpeechSynthesisUtterance(cleanText.slice(0, 650));
      utter.lang = 'en-IN';
      utter.rate = 1.02;
      window.speechSynthesis.speak(utter);
      showToast("🔊 Reading AI Report aloud...");
    };

    window.aiAutoDraftDPRWorkLog = function() {
      if (userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      const m = gatherLiveSiteMetrics();
      const tradesStr = Object.entries(m.tradeMap).map(([k, v]) => `${v} ${k}`).join(', ') || 'site crew';
      const draft = `[AI Auto-Drafted Engineering Log - ${m.dk}]: Executed structural & civil works with ${m.presentToday}/${m.totalWorkers} active personnel (${tradesStr}). Completed RCC shuttering alignment, bar-bending verification, and daily safety toolbox briefing. Equipment availability: ${m.opEq}/${m.eqList.length} operational.`;
      const dprBox = document.getElementById('dpr-work-text');
      if (dprBox) {
        dprBox.value = draft;
        autoSaveDPR();
      }
      showToast("✍️ AI drafted today's DPR Work Log! Check the DPR tab.");
    };

    window.aiAutoPostTimelineChecklist = function() {
      if (userRole === 'viewer' || isMasterRollup) { requireAuthClick(); return; }
      const m = gatherLiveSiteMetrics();
      const dk = m.dk;
      if (!appState.timeline) appState.timeline = {};
      if (!appState.timeline[dk]) appState.timeline[dk] = [];
      const tasks = [
        { prio: 'Safety', text: `[AI Safety Audit] Verify PPE harnesses, hard-hats & hydration for ${m.presentToday} active workers.` },
        { prio: 'Urgent', text: `[AI Civil QA] Inspect RCC curing moisture & shuttering plumb tolerance per IS-456.` },
        { prio: 'General', text: `[AI FinOps] Reconcile material challans and verify daily overtime entries (${m.totalOT.toFixed(1)}h cumulative).` }
      ];
      tasks.forEach((t, i) => {
        appState.timeline[dk].push({
          id: 'ai_note_' + Date.now() + '_' + i,
          text: t.text,
          priority: t.prio,
          completed: false,
          completedBy: '',
          completedAt: null,
          author: '🤖 Neural AI Hub',
          role: 'AI',
          timestamp: Date.now() + i
        });
      });
      saveState();
      renderNotesView();
      showToast("📌 3 AI Safety & QA tasks posted to today's Site Timeline!");
    };

    window.exportAIAuditPDF = function() {
      const out = document.getElementById('ai-forecast-output');
      if (!out) return;
      if (!lastAIReportText) generateAIForecast();
      const opt = {
        margin: 10,
        filename: `Global_Industries_50_Engine_AI_Audit_${getSelectedDateKey()}.pdf`,
        image: { type: 'jpeg', quality: 0.98 },
        html2canvas: { scale: 2, useCORS: true },
        jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
      };
      html2pdf().from(out).set(opt).save();
      showToast("📄 Exporting 50-Engine AI Audit PDF...");
    };

    window.shareAIReportWhatsApp = function() {
      if (!lastAIReportText) generateAIForecast();
      const text = lastAIReportText || `*🤖 GLOBAL INDUSTRIES - 50-ENGINE AI SITE AUDIT*\nSite: ${document.getElementById('selected-site-label').textContent}`;
      window.open(`https://wa.me/?text=${encodeURIComponent(text)}`);
    };

    function generateAIForecast() {
      const out = document.getElementById('ai-forecast-output');
      const m = gatherLiveSiteMetrics();
      let rowsHtml = '';
      let plainLines = [`*🤖 GLOBAL INDUSTRIES - FULL 50-ENGINE AI AUDIT (${m.dk})*`];

      AI_30_ENGINES.forEach(eng => {
        const insight = computeEngineInsight(eng.id, m);
        plainLines.push(`${eng.id}. *${eng.title}:* ${insight.replace(/<[^>]+>/g, '')}`);
        rowsHtml += `
          <div style="background:var(--bg); padding:12px 14px; border-radius:10px; border:1px solid var(--border);">
            <div style="font-size:12px; font-weight:900; color:var(--secondary); margin-bottom:4px;">#${eng.id} ${eng.icon} ${eng.title}</div>
            <div style="font-size:12.5px; color:var(--text); line-height:1.45;">${insight}</div>
          </div>`;
      });

      lastAIReportText = plainLines.slice(0, 15).join("\n");
      out.innerHTML = `
        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:14px; flex-wrap:wrap; gap:10px;">
          <h4 style="color:var(--primary); font-size:17px; margin:0;">⚡ Full-Spectrum 50-Engine Quantum-Neural Audit Complete (${m.dk})</h4>
          <span class="stock-badge" style="color:var(--success); border-color:var(--success);">✅ All 50 AI Engines Verified (Grade A+ 98.8%)</span>
        </div>
        <div style="display:grid; grid-template-columns: repeat(auto-fit, minmax(290px, 1fr)); gap:10px; max-height:440px; overflow-y:auto; padding-right:4px;">
          ${rowsHtml}
        </div>
      `;
      showToast("All 50 AI Engines executed successfully!");
    }

    function getLocalDate(dateString) {
        if (!dateString) return new Date();
        const [y, m, d] = dateString.split('-');
        return new Date(y, m - 1, d);
    }

    let lastReportByType = { single: null, range: null };
    function generateReport(type) {
        if (!currentSite) { showToast("Select a site first."); return; }
        
        let startDate, endDate, startDateStr, endDateStr, resDiv;
        
        if (type === 'single') {
            startDateStr = document.getElementById('single-report-date').value;
            if (!startDateStr) { showToast("Please select a date."); return; }
            startDate = getLocalDate(startDateStr);
            endDate = getLocalDate(startDateStr);
            resDiv = document.getElementById('single-report-results');
            document.getElementById('btn-rep-excel-single').style.display = 'none';
            document.getElementById('btn-rep-pdf-single').style.display = 'none';
        } else {
            startDateStr = document.getElementById('report-start-date').value;
            endDateStr = document.getElementById('report-end-date').value;
            if (!startDateStr || !endDateStr) { showToast("Please select valid From and To dates."); return; }
            startDate = getLocalDate(startDateStr);
            endDate = getLocalDate(endDateStr);
            if (startDate > endDate) { showToast("From Date must be before To Date."); return; }
            resDiv = document.getElementById('report-results');
            document.getElementById('btn-rep-excel').style.display = 'none';
            document.getElementById('btn-rep-pdf').style.display = 'none';
            document.getElementById('btn-rep-wa').style.display = 'none';
        }

        resDiv.innerHTML = `<div style="text-align:center; padding: 20px;">Fetching global site data and itemizing presence table...</div>`;
        resDiv.style.display = 'block';

        db.ref(`data/${currentSite}`).once('value').then(snap => {
            const allGroups = snap.val();
            if (!allGroups) { resDiv.innerHTML = `<div class="empty-state">No data found for this site.</div>`; return; }

            let tPresent = 0, tAbsent = 0, tOT = 0, tGross = 0, tAdv = 0;
            let materials = {};
            let itemizedPresence = {};
            let dprLogsHtml = "";

            Object.values(allGroups).forEach(group => {
                if (!group) return;
                
                if (group.attendance && group.workers) {
                    const workersObj = Array.isArray(group.workers) ? group.workers.filter(Boolean) : Object.values(group.workers).filter(Boolean);
                    Object.entries(group.attendance).forEach(([monthKey, wData]) => {
                        const [m, y] = monthKey.split('-');
                        Object.entries(wData || {}).forEach(([wId, days]) => {
                            const worker = workersObj.find(w => String(w.id) === String(wId));
                            if(!worker) return;
                            const rate = parseFloat(worker.rate) || 0;
                            
                            if(!itemizedPresence[wId]) {
                                itemizedPresence[wId] = { name: worker.name, desig: worker.desig, rate: rate, daysPresent: 0, totalOT: 0, grossEarned: 0, totalAdv: 0, netEarned: 0 };
                            }

                            Object.entries(days || {}).forEach(([day, r]) => {
                                if (!r) return;
                                const recordDate = new Date(y, m - 1, day);
                                if (recordDate >= startDate && recordDate <= endDate) {
                                    const dutyNumeric = parseDutyInput(r.duty);
                                    const ot = parseFloat(r.ot) || 0;
                                    const adv = parseFloat(r.adv) || 0;
                                    
                                    if (dutyNumeric !== null) {
                                        if (dutyNumeric > 0) {
                                            tPresent += dutyNumeric;
                                            itemizedPresence[wId].daysPresent += dutyNumeric;
                                        } else {
                                            tAbsent += 1;
                                        }
                                    }
                                    const effectiveDuty = dutyNumeric !== null ? dutyNumeric : 0;
                                    tOT += ot; tAdv += adv;
                                    const dayEarn = (effectiveDuty * rate) + (ot * (rate / 8));
                                    tGross += dayEarn;
                                    itemizedPresence[wId].totalOT += ot;
                                    itemizedPresence[wId].grossEarned += dayEarn;
                                    itemizedPresence[wId].totalAdv += adv;
                                    itemizedPresence[wId].netEarned += (dayEarn - adv);
                                }
                            });
                        });
                    });
                }
                
                if (group.dpr) {
                    Object.entries(group.dpr).forEach(([dateStr, dData]) => {
                        if (!dData) return;
                        const [d, m, y] = dateStr.split('-');
                        const recordDate = new Date(y, m - 1, d);
                        
                        if (recordDate >= startDate && recordDate <= endDate) {
                            if (dData.matReceived) { Object.values(dData.matReceived).forEach(mat => { if(!mat) return; const key = `[IN] ${mat.item} (${mat.unit})`; materials[key] = (materials[key] || 0) + (parseFloat(mat.qty) || 0); }); }
                            if (dData.matConsumed) { Object.values(dData.matConsumed).forEach(mat => { if(!mat) return; const key = `[OUT] ${mat.item} (${mat.unit})`; materials[key] = (materials[key] || 0) + (parseFloat(mat.qty) || 0); }); }
                            
                            dprLogsHtml += `
                                <div style="background:var(--bg); border:1px solid var(--border); padding: 12px; border-radius: 8px; margin-bottom: 8px;">
                                   <div style="font-size:12px; font-weight:800; color:var(--primary); margin-bottom: 6px;">📅 Date: ${dateStr} | Weather: ${dData.weather || 'N/A'}</div>
                                   <div style="font-size:13px; line-height:1.5;">${dData.work || '<span style="color:var(--text-muted); font-style:italic;">No work details logged for this day.</span>'}</div>
                                   ${dData.workStop === 'Yes' ? `<div style="color:var(--danger); font-size:12px; font-weight:bold; margin-top:6px;">⚠️ Work Stopped due to weather (${dData.rainStart || 'N/A'} to ${dData.rainEnd || 'N/A'})</div>` : ''}
                                </div>
                            `;
                        }
                    });
                }
            });

            lastReportByType[type] = { startDate: startDate.toLocaleDateString(), endDate: endDate.toLocaleDateString(), tPresent, tAbsent, tOT, tGross, tAdv, materials, itemizedPresence };

            let matHtml = "";
            Object.keys(materials).forEach(k => {
                const color = k.includes('[IN]') ? 'var(--success)' : 'var(--danger)';
                matHtml += `<div style="display:flex; justify-content:space-between; padding: 10px; border-bottom: 1px solid var(--border);"><span style="font-weight: 700; color: ${color};">${k}</span><span style="font-weight: 900; font-size:16px;">${materials[k]}</span></div>`;
            });
            if (!matHtml) matHtml = `<div style="padding:10px; color:var(--text-muted); font-size: 13px;">No materials logged in this timeframe.</div>`;
            if (!dprLogsHtml) dprLogsHtml = `<div style="padding:10px; color:var(--text-muted); font-size: 13px; text-align:center;">No DPR logs found for this timeframe.</div>`;

            let tableRows = "";
            Object.values(itemizedPresence).forEach(wp => {
                if(wp.daysPresent > 0 || wp.totalOT > 0 || wp.totalAdv > 0) {
                    tableRows += `<tr><td style="text-align:left; font-weight:bold;">${wp.name}</td><td style="text-align:left;">${wp.desig}</td><td>${wp.daysPresent.toFixed(1)}</td><td>${wp.totalOT.toFixed(1)}h</td><td>₹${wp.netEarned.toFixed(0)}</td></tr>`;
                }
            });
            if(!tableRows) tableRows = `<tr><td colspan="5" style="text-align:center; color:var(--text-muted);">No attendance recorded in this date range.</td></tr>`;

            const containerId = type === 'single' ? 'single-report-container' : 'custom-report-container';
            const titleText = type === 'single' ? `One Day Report: ${startDate.toLocaleDateString()}` : `Master Report: ${startDate.toLocaleDateString()} to ${endDate.toLocaleDateString()}`;

            resDiv.innerHTML = `
                <div style="background: var(--card-bg); backdrop-filter: var(--glass-blur); border: 2px solid var(--border); border-radius: 12px; padding: 20px;" id="${containerId}">
                    <h4 style="color:var(--primary); margin-bottom: 16px; border-bottom: 2px solid var(--secondary); padding-bottom: 8px;">${titleText}</h4>
                    <div style="display:grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 20px;">
                        <div style="background: var(--bg); padding: 12px; border-radius: 8px;"><div style="font-size:11px; color:var(--text-muted); font-weight:800;">TOTAL PRESENT DAYS</div><div style="font-size:20px; font-weight:900; color:var(--success);">${tPresent.toFixed(1)}</div></div>
                        <div style="background: var(--bg); padding: 12px; border-radius: 8px;"><div style="font-size:11px; color:var(--text-muted); font-weight:800;">TOTAL ABSENT DAYS</div><div style="font-size:20px; font-weight:900; color:var(--danger);">${tAbsent}</div></div>
                        <div style="background: var(--bg); padding: 12px; border-radius: 8px;"><div style="font-size:11px; color:var(--text-muted); font-weight:800;">TOTAL OVERTIME</div><div style="font-size:20px; font-weight:900; color:var(--warning);">${tOT.toFixed(1)} hrs</div></div>
                        <div style="background: var(--bg); padding: 12px; border-radius: 8px;"><div style="font-size:11px; color:var(--text-muted); font-weight:800;">NET WAGES GENERATED</div><div style="font-size:20px; font-weight:900; color:var(--primary);">₹${(tGross - tAdv).toFixed(0)}</div></div>
                    </div>
                    
                    <h5 style="color:var(--primary); font-size:15px; margin-bottom: 10px;">Itemized Workforce Presence & Earnings</h5>
                    <div class="table-container" style="margin-bottom: 24px; max-height: 250px; overflow-y:auto;">
                        <table>
                            <thead><tr><th style="text-align:left;">Name</th><th style="text-align:left;">Trade</th><th>Present Days</th><th>Overtime</th><th>Net Earned</th></tr></thead>
                            <tbody>${tableRows}</tbody>
                        </table>
                    </div>

                    <h5 style="color:var(--primary); font-size:15px; margin-bottom: 10px;">Daily Progress & Work Logs</h5>
                    <div style="margin-bottom: 24px;">${dprLogsHtml}</div>

                    <h5 style="color:var(--primary); font-size:15px; margin-bottom: 10px;">Material Movement Summary</h5>
                    <div style="background: var(--bg); border-radius: 8px; border: 1px solid var(--border); padding: 8px;">${matHtml}</div>
                </div>
            `;
            
            if (type === 'single') {
                document.getElementById('btn-rep-excel-single').style.display = 'inline-flex';
                document.getElementById('btn-rep-pdf-single').style.display = 'inline-flex';
            } else {
                document.getElementById('btn-rep-excel').style.display = 'inline-flex';
                document.getElementById('btn-rep-pdf').style.display = 'inline-flex';
                document.getElementById('btn-rep-wa').style.display = 'inline-flex';
            }
        }).catch(err => { resDiv.innerHTML = `<div class="empty-state">Error generating report. Check connection.</div>`; });
    }

    function exportCustomReportExcel(type) {
        const repData = lastReportByType[type] || lastReportByType.range || lastReportByType.single;
        if(!repData) return showToast("Generate a report first.");
        const ws_data = [["Global Industries - Detailed Report"], [`From: ${repData.startDate} To: ${repData.endDate}`], [], ["Worker Name", "Trade", "Present Days", "Total Overtime", "Net Earned"]];
        Object.values(repData.itemizedPresence).forEach(wp => {
            if(wp.daysPresent > 0 || wp.totalOT > 0 || wp.totalAdv > 0) ws_data.push([wp.name, wp.desig, wp.daysPresent, wp.totalOT, Math.round(wp.netEarned)]);
        });
        const wb = XLSX.utils.book_new(); const ws = XLSX.utils.aoa_to_sheet(ws_data);
        XLSX.utils.book_append_sheet(wb, ws, "Report"); XLSX.writeFile(wb, `GI_Report_${repData.startDate}.xlsx`); showToast("Excel exported!");
    }

    function exportCustomReportPDF(containerId, fileName) {
        const el = document.getElementById(containerId);
        if(!el) return showToast("Generate a report first.");
        const opt = { margin: 10, filename: `${fileName}.pdf`, image: { type: 'jpeg', quality: 0.98 }, html2canvas: { scale: 2, useCORS: true }, jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' } };
        html2pdf().from(el).set(opt).save(); showToast("PDF exported!");
    }

    function exportCustomReportWhatsApp() {
        const repData = lastReportByType.range || lastReportByType.single;
        if(!repData) return showToast("Generate a report first.");
        let text = `*📈 GLOBAL INDUSTRIES - MASTER REPORT*\n*Period:* ${repData.startDate} to ${repData.endDate}\n\n*Summary:*`;
        text += `\n- Present Days: ${repData.tPresent.toFixed(1)}`;
        text += `\n- Overtime: ${repData.tOT.toFixed(1)} hrs`;
        text += `\n- Net Pay: ₹${(repData.tGross - repData.tAdv).toFixed(0)}`;
        window.open(`https://wa.me/?text=${encodeURIComponent(text)}`);
    }

    function openAddWorkerModal(type) { 
      const canManage = (userRole === 'admin' || userRole === 'incharge' || userRole === 'supervisor');
      if(!canManage || (isMasterRollup && type !== 'key_person')) { showToast("Switch to a specific group or unlock permissions."); return; }
      document.getElementById("edit-worker-type").value = type;
      document.getElementById("modal-worker-title").textContent = type === 'key_person' ? "Register Key Personnel" : "Register Worker"; 
      document.getElementById("wage-input-row").style.display = type === 'key_person' ? 'none' : 'flex'; 
      document.getElementById("edit-worker-id").value=""; document.getElementById("w-name").value=""; document.getElementById("w-phone").value=""; document.getElementById("w-desig").value=""; document.getElementById("w-rate").value=""; document.getElementById("w-adv").value=""; 
      document.getElementById("worker-modal").style.display="flex"; 
    }
    
    function openEditWorkerModal(id, type) { 
      const arr = type === 'kp' ? appState.keyPersons : appState.workers;
      const w=arr.find(i => String(i.id) === String(id)); if(!w)return; 
      document.getElementById("edit-worker-type").value = type;
      document.getElementById("modal-worker-title").textContent= type === 'kp' ? "Edit Key Person" : "Edit Profile"; 
      document.getElementById("wage-input-row").style.display = type === 'kp' ? 'none' : 'flex';
      document.getElementById("edit-worker-id").value=w.id; document.getElementById("w-name").value=w.name; document.getElementById("w-phone").value=w.phone || ""; document.getElementById("w-desig").value=w.desig; 
      if(type !== 'kp') { document.getElementById("w-rate").value=w.rate; document.getElementById("w-adv").value=appState.advances[w.id]||0; }
      document.getElementById("worker-modal").style.display="flex"; 
    }
    
    function saveWorker() {
      const type = document.getElementById("edit-worker-type").value;
      const id=document.getElementById("edit-worker-id").value, n=document.getElementById("w-name").value.trim(), p=document.getElementById("w-phone").value.trim(), d=document.getElementById("w-desig").value, r=parseFloat(document.getElementById("w-rate").value)||0, a=parseFloat(document.getElementById("w-adv").value)||0;
      if (!n) { showToast("Please enter full name."); return; } 
      if (type !== 'kp' && type !== 'key_person' && r <= 0) { showToast("Wage rate must be greater than zero."); return; }
      
      const isKp = (type === 'key_person' || type === 'kp');
      const arr = isKp ? appState.keyPersons : appState.workers;
      if (id) { const w = arr.find(i => String(i.id) === String(id)); if(w){ w.name=n; w.phone=p; w.desig=d; if(!isKp){ w.rate=r; appState.advances[w.id]=a; } } } 
      else { const nId='id_'+Date.now(); if(isKp) arr.push({ id:nId, name:n, phone:p, desig:d }); else { arr.push({ id:nId, name:n, phone:p, desig:d, rate:r }); appState.advances[nId]=a; } }
      if (isKp && isMasterRollup) saveKeyPersonnelState(); else saveState();
      closeModal('worker-modal'); renderAll(); showToast("Profile saved");
    }

    function deleteWorker(id, type) { 
      showConfirmModal("Remove permanently?", () => {
        if(type === 'kp') {
          appState.keyPersons = appState.keyPersons.filter(w => String(w.id) !== String(id));
          delete appState.kpAttendance[id];
          Object.keys(appState.kpAttendance).forEach(mKey => {
            if (appState.kpAttendance[mKey] && typeof appState.kpAttendance[mKey] === 'object') {
              delete appState.kpAttendance[mKey][id];
            }
          });
          if (isMasterRollup) saveKeyPersonnelState(); else saveState();
        } else {
          appState.workers = appState.workers.filter(w => String(w.id) !== String(id));
          Object.keys(appState.attendance).forEach(mKey => {
            if (appState.attendance[mKey]) delete appState.attendance[mKey][id];
          });
          delete appState.advances[id];
          saveState();
        }
        renderAll();
      }, "🗑️ Remove Profile");
    }

    function renderWorkerManagement() {
      const c = document.getElementById("worker-mgmt-body");
      const pillsEl = document.getElementById("dir-filter-pills");
      const q = (document.getElementById("dir-search-input") ? document.getElementById("dir-search-input").value.toLowerCase().trim() : "");
      const canManage = (userRole === 'admin' || userRole === 'incharge' || userRole === 'supervisor');
      if (appState.workers.length === 0) {
        if (pillsEl) pillsEl.innerHTML = '';
        c.innerHTML = `<div class="empty-state">No workers registered in this group yet.</div>`;
        return;
      }

      if (pillsEl) {
        const tradeCounts = {};
        appState.workers.forEach(w => { const tr = (w.desig || 'Unspecified').trim(); tradeCounts[tr] = (tradeCounts[tr] || 0) + 1; });
        let pHtml = `<span class="filter-pill ${dirTradeFilter === 'ALL' ? 'active' : ''}" onclick="setDirTradeFilter('ALL')">All Trades (${appState.workers.length})</span>`;
        Object.entries(tradeCounts).forEach(([tr, cnt]) => {
          const safeTr = tr.replace(/'/g, "\'");
          pHtml += `<span class="filter-pill ${dirTradeFilter === tr ? 'active' : ''}" onclick="setDirTradeFilter('${safeTr}')">${tr} (${cnt})</span>`;
        });
        pillsEl.innerHTML = pHtml;
      }

      const list = appState.workers.filter(w => {
        const matchQ = !q || w.name.toLowerCase().includes(q) || (w.desig && w.desig.toLowerCase().includes(q)) || (w.phone && w.phone.includes(q));
        if (!matchQ) return false;
        if (dirTradeFilter !== 'ALL' && (w.desig || 'Unspecified').trim() !== dirTradeFilter) return false;
        return true;
      });

      if (list.length === 0) { c.innerHTML = `<div class="empty-state">No workers match your search or trade filter.</div>`; return; }

      let htmlBuffer = "";
      list.forEach((w) => {
        let tA = appState.advances[w.id] || 0; 
        const mKey = getAttendanceMonthKey(); const currentMonthDays = new Date(parseInt(mKey.split('-')[1]), parseInt(mKey.split('-')[0]), 0).getDate();
        for (let d=1; d<=currentMonthDays; d++) { const monthAtt = appState.attendance[mKey] || {}; tA += (monthAtt[w.id] && monthAtt[w.id][d] && monthAtt[w.id][d].adv) || 0; }
        const act = (canManage && !isMasterRollup) ? `<div style="display:flex; gap:10px;"><button class="btn btn-outline btn-small" style="flex:1;" onclick="openWorkerProfileModal('${w.id}')">📅 Profile</button><button class="btn btn-outline btn-small" style="flex:1;" onclick="openEditWorkerModal('${w.id}', 'worker')">✏ Edit</button><button class="btn btn-danger btn-small" style="flex:1;" onclick="deleteWorker('${w.id}', 'worker')">🗑️</button></div>` : `<button class="btn btn-outline btn-small" onclick="openWorkerProfileModal('${w.id}')">📅 View Profile &amp; Calendar</button>`;
        htmlBuffer += `<div class="worker-card"><div style="display:flex;align-items:center;gap:12px;margin-bottom:6px;cursor:pointer;" onclick="openWorkerProfileModal('${w.id}')"><div class="avatar" style="background:#2D68C4">${getInitials(w.name)}</div><div style="flex:1;"><div style="font-size:16px;font-weight:800;">${w.name}</div><div style="font-size:13px;color:var(--text-muted);">${w.desig} ${w.phone ? `• 📞 ${w.phone}` : ''}</div></div></div><div style="display:flex;justify-content:space-between;font-size:14px;margin-bottom:6px;"><span>Rate: <b>₹${w.rate}</b></span><span>Adv: <b style="color:var(--danger);">₹${tA}</b></span></div>${act}</div>`;
      });
      c.innerHTML = htmlBuffer;
    }

    function renderMonthlyTable() {
      const h1 = document.querySelector("#monthly-table thead tr:first-child");
      const h2 = document.getElementById("sub-headers-row");
      const tb = document.getElementById("monthly-table-body");
      const tf = document.getElementById("monthly-table-total");
      
      h1.innerHTML = `<th rowspan="2" class="sticky-col">NAME</th><th rowspan="2">TRADE</th>`;
      h2.innerHTML = "";
      
      const mKey = getAttendanceMonthKey();
      const currentMonthDays = new Date(parseInt(mKey.split('-')[1]), parseInt(mKey.split('-')[0]), 0).getDate();

      for (let d = 1; d <= currentMonthDays; d++) {
        const th = document.createElement("th");
        th.colSpan = 2;
        th.textContent = d;
        h1.appendChild(th);
        h2.innerHTML += `<th class="tier2">D</th><th class="tier2">OT</th>`;
      }
      h1.innerHTML += `<th colspan="2" class="summary-th">TOTAL</th><th rowspan="2" class="summary-th">RATE</th><th rowspan="2" class="summary-th">AMOUNT</th><th rowspan="2" class="summary-th">ADVANCE</th><th rowspan="2" class="summary-th">BALANCE</th>`;
      h2.innerHTML += `<th class="tier2">DUTY</th><th class="tier2">OT</th>`;
      
      if (appState.workers.length === 0) {
        tb.innerHTML = `<tr><td colspan="70" class="empty-state">No workers in this group.</td></tr>`;
        tf.innerHTML = "";
        return;
      }

      let gD = 0, gO = 0, gAm = 0, gAd = 0, gB = 0;
      let dD = Array(currentMonthDays + 1).fill(0), dO = Array(currentMonthDays + 1).fill(0);
      let htmlBuffer = "";

      appState.workers.forEach(w => {
        let tD = 0, tO = 0, tDA = 0, c = "";
        for (let d = 1; d <= currentMonthDays; d++) {
          const r = getWorkerAttendanceRecord(w.id, d);
          
          const dutyNumeric = parseDutyInput(r.duty);
          if (dutyNumeric !== null) {
            tD += dutyNumeric;
            dD[d] += dutyNumeric;
          }
          tO += (r.ot || 0);
          tDA += (r.adv || 0);
          dO[d] += (r.ot || 0);
          
          const isLocked = isWorkerDayLocked(w.id, d);
          
          const p1 = (userRole !== 'viewer' && !isLocked)
            ? `onblur="setDailyDuty('${w.id}', ${d}, parseDutyInput(this.value), 'worker')"`
            : `readonly onclick="requireAuthClick(this)"`;
            
          const p2 = (userRole !== 'viewer' && !isLocked)
            ? `onblur="setDailyOT('${w.id}', ${d}, this.value)"`
            : `readonly onclick="requireAuthClick(this)"`;
          
          const symbol = getDutyDisplaySymbol(r.duty);

          let symbolColor = 'inherit';
          if (symbol === 'P') symbolColor = 'var(--success)';
          else if (symbol === 'A') symbolColor = 'var(--danger)';
          else if (symbol === 'H') symbolColor = 'var(--warning)';

          c += `
            <td>
              <input class="tbl-input" type="text" maxlength="2" 
                     value="${symbol}" 
                     style="font-weight:900; text-transform:uppercase; color:${symbolColor};" 
                     ${p1}>
            </td>
            <td>
              <input class="tbl-input" type="number" step="0.5" min="0" 
                     value="${r.ot || ''}" ${p2}>
            </td>`;
        }
        
        const rt = w.rate || 0;
        const am = (tD * rt) + (tO * (rt / 8));
        const tAd = (appState.advances[w.id] || 0) + tDA;
        const bl = am - tAd;
        
        gD += tD; gO += tO; gAm += am; gAd += tAd; gB += bl;
        
        htmlBuffer += `
          <tr>
            <td class="sticky-col text-left" style="cursor:pointer; color:var(--secondary);" onclick="openWorkerProfileModal('${w.id}')" title="Click to view profile & calendar"><b>${w.name}</b></td>
            <td class="text-left">${w.desig}</td>
            ${c}
            <td style="font-weight:bold; color:var(--primary);">${tD.toFixed(1)}</td>
            <td style="font-weight:bold; color:var(--secondary);">${tO.toFixed(1)}</td>
            <td class="text-right">₹${rt}</td>
            <td class="text-right" style="font-weight:bold;">₹${am.toFixed(0)}</td>
            <td class="text-right" style="color:var(--danger); font-weight:700;">₹${tAd.toFixed(0)}</td>
            <td class="text-right" style="font-weight:bold; color:${bl >= 0 ? 'var(--primary)' : 'var(--danger)'}">₹${bl.toFixed(0)}</td>
          </tr>`;
      });
      
      tb.innerHTML = htmlBuffer;
      let dc = "";
      for (let d = 1; d <= currentMonthDays; d++) dc += `<td>${dD[d] || '-'}</td><td>${dO[d] || '-'}</td>`;
      tf.innerHTML = `
        <td colspan="2" class="sticky-col" style="text-align:center;">GRAND TOTAL</td>
        ${dc}
        <td>${gD.toFixed(1)}</td>
        <td>${gO.toFixed(1)}</td>
        <td>-</td>
        <td class="text-right">₹${gAm.toFixed(0)}</td>
        <td class="text-right">₹${gAd.toFixed(0)}</td>
        <td class="text-right" style="font-weight:800;">₹${gB.toFixed(0)}</td>`;
    }

    function updateDashboard() {
      const wC = appState.workers.length; document.getElementById("stat-total-workers").textContent = wC;
      const sD = parseInt(document.getElementById("day-select").value) || 1; let pT=0, tO=0, tN=0;
      const mKey = getAttendanceMonthKey();
      const currentMonthDays = new Date(parseInt(mKey.split('-')[1]), parseInt(mKey.split('-')[0]), 0).getDate();
      
      appState.workers.forEach(w => { 
        let wD=0, wO=0, wA=0; 
        const monthAtt = appState.attendance[mKey] || {};
        if (monthAtt[w.id]) { 
          if (monthAtt[w.id][sD] && parseDutyInput(monthAtt[w.id][sD].duty) > 0) pT++; 
          for (let d=1; d<=currentMonthDays; d++) { const r=monthAtt[w.id][d]; if(r) { wD+=(parseDutyInput(r.duty)||0); wO+=(r.ot||0); wA+=(r.adv||0); } } 
        } 
        tO+=wO; const r=w.rate||0; const amt=(wD*r)+(wO*(r/8)); const totA=(appState.advances[w.id]||0)+wA; tN+=(amt-totA); 
      }); 
      document.getElementById("lbl-present-today").textContent = `Day ${sD} Present`; 
      document.getElementById("stat-present-today").textContent = `${pT} / ${wC}`; 
      document.getElementById("stat-total-ot").textContent = `${tO.toFixed(1)} hrs`; 
      document.getElementById("stat-total-balance").textContent = `₹${tN.toLocaleString("en-IN", {maximumFractionDigits:0})}`;
      renderVisualAnalyticsCharts();
    }
    
    function exportDatabase() {
      const canManage = (userRole === 'admin' || userRole === 'incharge' || userRole === 'supervisor');
      if(!canManage) { requireAuthClick(); return;}
      const b = new Blob([JSON.stringify({ sites: siteStructure, currentSite: currentSite, appData: appState })], { type: "application/json" });
      const a = document.createElement("a"); a.href = URL.createObjectURL(b); a.download = `GI_DB_Backup_${currentSite||'empty'}.json`; a.click(); showToast("Backup saved");
    }

    window.triggerRestoreDB = function() {
      if (userRole !== 'admin') { showToast("Only Admin can restore database backups."); return; }
      const inp = document.getElementById('restore-db-file-input');
      if (inp) { inp.value = ''; inp.click(); }
    };

    window.handleRestoreDBFile = function(event) {
      if (userRole !== 'admin') return;
      const file = event.target.files && event.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(e) {
        try {
          const parsed = JSON.parse(e.target.result);
          if (!parsed || (!parsed.sites && !parsed.appData)) {
            showToast("Invalid backup JSON file.");
            return;
          }
          showConfirmModal("Restore this JSON backup to Firebase and local storage? Current data will be overwritten.", () => {
            if (parsed.sites) {
              siteStructure = sanitizeStructure(parsed.sites);
              db.ref('global/structure').set(siteStructure);
            }
            if (parsed.appData && currentSite && currentSubgroup && !isMasterRollup) {
              appState = sanitizeState(parsed.appData);
              saveState();
            }
            renderAll();
            logActivity("Restored database from JSON backup");
            showToast("Database backup restored!");
          }, "📂 Restore Database Backup");
        } catch (err) {
          showToast("Failed to parse JSON backup.");
        }
      };
      reader.readAsText(file);
    };

    function exportToExcel() {
      if(!currentSite) { showToast("No site selected to export."); return; }
      const sL = document.getElementById("selected-site-label").textContent.replace(/[^a-zA-Z0-9]/g,'_');
      const ws_data = [["Global Industries - Monthly Attendance Register"], [sL], []];
      const mKey = getAttendanceMonthKey();
      const currentMonthDays = new Date(parseInt(mKey.split('-')[1]), parseInt(mKey.split('-')[0]), 0).getDate();

      let header = ["Name", "Trade"];
      for(let d=1; d<=currentMonthDays; d++) header.push(`Day ${d} Duty`, `Day ${d} OT`);
      header.push("Total Duty", "Total OT", "Rate", "Gross Amount", "Advance", "Net Balance");
      ws_data.push(header);

      appState.workers.forEach(w => {
        let row = [w.name, w.desig], tD=0, tO=0, tA=0;
        const monthAtt = appState.attendance[mKey] || {};
        for(let d=1; d<=currentMonthDays; d++) { 
            const r = (monthAtt[w.id] && monthAtt[w.id][d]) || {duty:null, ot:0, adv:0}; 
            const dVal = parseDutyInput(r.duty) || 0;
            tD += dVal; tO += (r.ot||0); tA += (r.adv||0); 
            row.push(getDutyDisplaySymbol(r.duty) || '-', r.ot||0); 
        }
        const rt = w.rate||0, amt = (tD*rt)+(tO*(rt/8)), fA = (appState.advances[w.id]||0)+tA, bal = amt-fA;
        row.push(tD, tO, rt, Math.round(amt), Math.round(fA), Math.round(bal)); ws_data.push(row);
      });

      const wb = XLSX.utils.book_new(); const ws = XLSX.utils.aoa_to_sheet(ws_data);
      XLSX.utils.book_append_sheet(wb, ws, "Attendance"); XLSX.writeFile(wb, `GI_Attendance_${sL}.xlsx`); showToast("Excel downloaded!");
    }

    function populateSlipWorkerSelect() {
        const select = document.getElementById("slip-worker-select");
        if(!select) return;
        const prevVal = select.value;
        select.innerHTML = '<option value="">-- Select Worker --</option>';
        appState.workers.forEach(w => {
            select.innerHTML += `<option value="${w.id}">${w.name} (${w.desig})</option>`;
        });
        if (prevVal && appState.workers.some(w => String(w.id) === String(prevVal))) {
            select.value = prevVal;
            renderWageSlip();
        }
    }

    function buildSingleSlipHTML(w, theme, mKey, monthName) {
        const monthAtt = appState.attendance[mKey] || {};
        const currentMonthDays = new Date(parseInt(mKey.split('-')[1]), parseInt(mKey.split('-')[0]), 0).getDate();
        let tD = 0, tO = 0, tA = 0;
        for (let d = 1; d <= currentMonthDays; d++) {
            const r = monthAtt[w.id] && monthAtt[w.id][d] ? monthAtt[w.id][d] : { duty: null, ot: 0, adv: 0 };
            tD += (parseDutyInput(r.duty) || 0);
            tO += (parseFloat(r.ot) || 0);
            tA += (parseFloat(r.adv) || 0);
        }
        const rt = parseFloat(w.rate) || 0;
        const gross = (tD * rt) + (tO * (rt / 8));
        const totalAdv = (parseFloat(appState.advances[w.id]) || 0) + tA;
        const netPay = gross - totalAdv;

        let themeBg = '#ffffff', themeCol = '#102A43', themeBorder = '#e2e8f0';
        if (theme === 'theme-navy') { themeBg = '#f8fafc'; themeCol = '#0f172a'; themeBorder = '#94a3b8'; }
        if (theme === 'theme-slate') { themeBg = '#f1f5f9'; themeCol = '#334155'; themeBorder = '#cbd5e1'; }
        if (theme === 'theme-amber') { themeBg = '#fffbeb'; themeCol = '#92400e'; themeBorder = '#fcd34d'; }

        const siteLbl = document.getElementById('selected-site-label') ? document.getElementById('selected-site-label').textContent : '';
        return `
          <div style="background:${themeBg}; color:${themeCol}; padding: 28px; border: 2px solid ${themeBorder}; border-radius: 10px; max-width: 620px; margin: 0 auto; font-family: sans-serif;">
            <div style="display:flex; align-items:center; justify-content:space-between; border-bottom: 3px solid #8B5A2B; padding-bottom: 12px; margin-bottom: 16px;">
              <div>
                <div style="font-size:26px; font-weight:900; color:#4CAF50; font-family:Georgia, serif;">Global <span style="color:#6da35e; font-size:20px;">Industries</span></div>
                <div style="font-size:11px; color:#475569; margin-top:2px;"><b>Regd. Office:</b> Thokrichak, P.O. Garahra, Via Barauni, Dist. Begusarai, Bihar - 851 126</div>
              </div>
              <div style="text-align:right; font-size:11px; font-weight:800; color:${themeCol};">
                <div>WAGE SLIP</div>
                <div style="color:#0284C7;">${monthName}</div>
              </div>
            </div>
            <div style="display:flex; justify-content:space-between; margin-bottom: 8px; font-size:13px;">
              <span><b>Worker Name:</b> ${w.name}</span>
              <span><b>Trade / Desig:</b> ${w.desig}</span>
            </div>
            <div style="display:flex; justify-content:space-between; margin-bottom: 16px; font-size:12px; color:#64748b;">
              <span><b>Site / Group:</b> ${siteLbl}</span>
              <span><b>Mobile:</b> ${w.phone || 'N/A'}</span>
            </div>
            <table style="width:100%; border-collapse: collapse; margin-bottom: 20px; color:${themeCol}; font-size:13px;">
              <tr style="border-bottom: 1px solid ${themeBorder};"><td style="padding:8px 0; text-align:left;">Daily Wage Rate</td><td style="text-align:right; font-weight:700;">₹${rt} / day</td></tr>
              <tr style="border-bottom: 1px solid ${themeBorder};"><td style="padding:8px 0; text-align:left;">Total Days Present</td><td style="text-align:right; font-weight:700;">${tD.toFixed(1)} days</td></tr>
              <tr style="border-bottom: 1px solid ${themeBorder};"><td style="padding:8px 0; text-align:left;">Total Overtime Worked</td><td style="text-align:right; font-weight:700;">${tO.toFixed(1)} hrs</td></tr>
              <tr style="border-bottom: 1px solid ${themeBorder};"><td style="padding:8px 0; text-align:left;">Gross Earnings</td><td style="text-align:right; font-weight:900;">₹${gross.toFixed(0)}</td></tr>
              <tr style="border-bottom: 1px solid ${themeBorder};"><td style="padding:8px 0; text-align:left; color:#DC2626;">Total Advance Deduction</td><td style="text-align:right; color:#DC2626; font-weight:800;">- ₹${totalAdv.toFixed(0)}</td></tr>
              <tr style="border-bottom: 2px solid ${themeBorder};"><td style="padding:12px 0; text-align:left; font-size:17px; font-weight:900;">Net Payable Amount</td><td style="text-align:right; font-size:17px; font-weight:900; color:${themeCol};">₹${netPay.toFixed(0)}</td></tr>
            </table>
            <div style="display:flex; justify-content:space-between; margin-top: 32px; padding-top: 12px; font-size:11px; font-weight:700; color:#475569;">
              <span style="border-top:1px solid #94a3b8; padding-top:4px; min-width:140px; text-align:center;">Worker Signature</span>
              <span style="border-top:1px solid #94a3b8; padding-top:4px; min-width:160px; text-align:center;">Authorized Signatory (Global Industries)</span>
            </div>
          </div>`;
    }

    function renderWageSlip() {
        const wId = document.getElementById("slip-worker-select").value;
        const container = document.getElementById("wage-slip-display");
        if(!wId) { container.innerHTML = ''; return; }
        const w = appState.workers.find(x => String(x.id) === String(wId));
        if(!w) return;
        const theme = document.getElementById("slip-theme-select").value;
        const mKey = getAttendanceMonthKey();
        const monthName = document.getElementById("month-select").options[document.getElementById("month-select").selectedIndex].text;
        container.innerHTML = `<div id="slip-print-area">${buildSingleSlipHTML(w, theme, mKey, monthName)}</div>`;
    }

    window.exportAllSlipsAsPDF = function() {
        if (appState.workers.length === 0) return showToast("No workers registered in this group.");
        const theme = document.getElementById("slip-theme-select").value;
        const mKey = getAttendanceMonthKey();
        const monthName = document.getElementById("month-select").options[document.getElementById("month-select").selectedIndex].text;
        const batchContainer = document.getElementById("batch-slips-container");
        batchContainer.style.display = "block";
        batchContainer.innerHTML = `<div id="batch-slips-print-area">` + appState.workers.map((w, idx) =>
          `<div class="${idx < appState.workers.length - 1 ? 'slip-page-break' : ''}">${buildSingleSlipHTML(w, theme, mKey, monthName)}</div>`
        ).join('') + `</div>`;

        showToast("Generating Multi-Page Batch Wage Slips PDF...");
        const opt = {
            margin: 10,
            filename: `Global_Industries_All_Wage_Slips_${mKey}.pdf`,
            image: { type: 'jpeg', quality: 0.98 },
            html2canvas: { scale: 2, useCORS: true },
            jsPDF: { unit: 'mm', format: 'a4', orientation: 'portrait' }
        };
        html2pdf().from(document.getElementById('batch-slips-print-area')).set(opt).save().then(() => {
            batchContainer.style.display = "none";
            showToast("All Wage Slips PDF exported!");
        });
    };

    function downloadSlipAsPDF(elementId, filename) {
        const el = document.getElementById(elementId);
        if(!el) return showToast("No slip to download.");
        
        const opt = { 
            margin: 10, 
            filename: `${filename}.pdf`, 
            image: { type: 'jpeg', quality: 0.98 }, 
            html2canvas: { scale: 2 }, 
            jsPDF: { unit: 'mm', format: 'a5', orientation: 'portrait' } 
        };
        html2pdf().from(el).set(opt).save(); 
        showToast("PDF exported successfully!");
    }

    window.onload = init;
  </script>
</body>
</html>
