<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rhevan | Portfolio 2026</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        :root {
            --bg-deep: #060b14;
            --bg-navy: #0a0f1e;
            --bg-navy-light: #0d1529;
            --bg-card: rgba(13, 21, 41, 0.65);
            --cyan: #00d4ff;
            --cyan-glow: #00d4ff66;
            --cyan-bright: #00e5ff;
            --cyan-dark: #0088aa;
            --white: #e8edf5;
            --white-soft: #c5cddb;
            --text-muted: #8899b4;
            --gold: #d4a853;
            --gradient-cyan: linear-gradient(135deg, #00d4ff, #0088cc);
            --gradient-dark: linear-gradient(180deg, #060b14 0%, #0a0f1e 40%, #0d1529 100%);
            --font-heading: 'Segoe UI', 'Inter', system-ui, -apple-system, sans-serif;
            --font-body: 'Segoe UI', 'Inter', system-ui, -apple-system, sans-serif;
            --radius-sm: 10px;
            --radius-md: 16px;
            --radius-lg: 24px;
            --radius-xl: 32px;
            --shadow-glow-sm: 0 0 18px rgba(0, 212, 255, 0.25);
            --shadow-glow-md: 0 0 35px rgba(0, 212, 255, 0.35);
            --shadow-glow-lg: 0 0 60px rgba(0, 212, 255, 0.45);
            --shadow-card: 0 8px 40px rgba(0, 0, 0, 0.5);
            --transition-smooth: 0.35s cubic-bezier(0.25, 0.1, 0.25, 1);
            --transition-bounce: 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
            --transition-slow: 0.7s cubic-bezier(0.25, 0.1, 0.25, 1);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html {
            scroll-behavior: smooth;
            scrollbar-width: thin;
            scrollbar-color: var(--cyan) var(--bg-deep);
        }

        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: var(--bg-deep);
        }
        ::-webkit-scrollbar-thumb {
            background: var(--cyan-dark);
            border-radius: 10px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: var(--cyan);
        }

        body {
            font-family: var(--font-body);
            background: var(--bg-deep);
            color: var(--white);
            line-height: 1.7;
            overflow-x: hidden;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
            position: relative;
            min-height: 100vh;
        }

        /* ============ CANVAS BACKGROUND ============ */
        #particleCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            pointer-events: none;
            opacity: 0.8;
        }

        /* ============ LOADING SCREEN ============ */
        #loadingScreen {
            position: fixed;
            inset: 0;
            z-index: 99999;
            background: var(--bg-deep);
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: column;
            transition: opacity 0.6s ease, visibility 0.6s ease;
            pointer-events: all;
        }
        #loadingScreen.hidden {
            opacity: 0;
            visibility: hidden;
            pointer-events: none;
        }
        .loader-ring {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            border: 3px solid transparent;
            border-top-color: var(--cyan);
            border-right-color: var(--cyan);
            animation: loaderSpin 0.9s linear infinite;
            filter: drop-shadow(0 0 14px var(--cyan-glow));
        }
        .loader-text {
            margin-top: 20px;
            font-family: var(--font-heading);
            font-weight: 700;
            font-size: 1.1rem;
            letter-spacing: 4px;
            color: var(--cyan);
            text-transform: uppercase;
            animation: loaderPulse 1.4s ease-in-out infinite;
        }
        @keyframes loaderSpin {
            to {
                transform: rotate(360deg);
            }
        }
        @keyframes loaderPulse {
            0%,
            100% {
                opacity: 0.4;
            }
            50% {
                opacity: 1;
            }
        }

        /* ============ MAIN CONTENT WRAPPER ============ */
        .main-content {
            position: relative;
            z-index: 1;
            pointer-events: all;
        }

        /* ============ NAVIGATION ============ */
        .navbar {
            position: fixed;
            top: 16px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 1000;
            width: 90%;
            max-width: 1100px;
            background: var(--bg-card);
            backdrop-filter: blur(28px);
            -webkit-backdrop-filter: blur(28px);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 50px;
            padding: 12px 28px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            transition: all var(--transition-smooth);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.45), var(--shadow-glow-sm);
        }
        .navbar.scrolled {
            top: 6px;
            border-radius: 40px;
            padding: 10px 24px;
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.55), var(--shadow-glow-md);
            background: rgba(10, 15, 30, 0.85);
            border-color: rgba(0, 212, 255, 0.2);
        }
        .nav-logo {
            font-family: var(--font-heading);
            font-weight: 800;
            font-size: 1.5rem;
            letter-spacing: 4px;
            color: var(--cyan);
            text-decoration: none;
            text-shadow: 0 0 22px var(--cyan-glow);
            transition: all var(--transition-smooth);
            cursor: pointer;
        }
        .nav-logo:hover {
            text-shadow: 0 0 40px var(--cyan-glow), 0 0 70px rgba(0, 212, 255, 0.5);
            color: #fff;
        }
        .nav-menu {
            display: flex;
            list-style: none;
            gap: 6px;
            align-items: center;
        }
        .nav-menu a {
            text-decoration: none;
            color: var(--white-soft);
            font-weight: 500;
            font-size: 0.9rem;
            padding: 9px 18px;
            border-radius: 30px;
            transition: all var(--transition-smooth);
            position: relative;
            letter-spacing: 0.5px;
        }
        .nav-menu a:hover,
        .nav-menu a.active {
            color: #fff;
            background: rgba(0, 212, 255, 0.12);
            box-shadow: 0 0 20px rgba(0, 212, 255, 0.2);
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.6);
        }
        .nav-menu a::after {
            content: '';
            position: absolute;
            bottom: 4px;
            left: 50%;
            transform: translateX(-50%) scaleX(0);
            width: 20px;
            height: 2px;
            background: var(--cyan);
            border-radius: 2px;
            transition: transform var(--transition-smooth);
            box-shadow: 0 0 10px var(--cyan-glow);
        }
        .nav-menu a:hover::after {
            transform: translateX(-50%) scaleX(1);
        }
        .nav-hamburger {
            display: none;
            background: none;
            border: none;
            cursor: pointer;
            padding: 8px;
            flex-direction: column;
            gap: 5px;
            z-index: 1001;
        }
        .nav-hamburger span {
            display: block;
            width: 26px;
            height: 2.5px;
            background: var(--cyan);
            border-radius: 3px;
            transition: all var(--transition-smooth);
            box-shadow: 0 0 8px var(--cyan-glow);
        }
        .nav-hamburger.active span:nth-child(1) {
            transform: rotate(45deg) translate(5px, 5px);
        }
        .nav-hamburger.active span:nth-child(2) {
            opacity: 0;
            transform: scaleX(0);
        }
        .nav-hamburger.active span:nth-child(3) {
            transform: rotate(-45deg) translate(5px, -5px);
        }

        /* ============ SECTIONS ============ */
        .section {
            position: relative;
            z-index: 1;
            padding: 90px 20px;
            max-width: 1100px;
            margin: 0 auto;
        }
        .section-label {
            display: inline-block;
            font-size: 0.75rem;
            text-transform: uppercase;
            letter-spacing: 5px;
            color: var(--cyan);
            margin-bottom: 12px;
            font-weight: 600;
            text-shadow: 0 0 14px var(--cyan-glow);
        }
        .section-title {
            font-family: var(--font-heading);
            font-size: 2.6rem;
            font-weight: 700;
            margin-bottom: 18px;
            color: #fff;
            letter-spacing: -0.5px;
            position: relative;
        }
        .section-title .accent {
            color: var(--cyan);
            text-shadow: 0 0 25px var(--cyan-glow);
        }
        .section-divider {
            width: 60px;
            height: 3px;
            background: var(--gradient-cyan);
            border-radius: 3px;
            margin-bottom: 35px;
            box-shadow: var(--shadow-glow-sm);
        }

        /* ============ HERO SECTION ============ */
        .hero-section {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            padding-top: 80px;
            position: relative;
            z-index: 1;
        }
        .hero-content {
            animation: heroFadeIn 1s ease forwards;
        }
        @keyframes heroFadeIn {
            from {
                opacity: 0;
                transform: translateY(40px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .hero-badge {
            display: inline-block;
            padding: 8px 20px;
            border-radius: 30px;
            background: rgba(0, 212, 255, 0.08);
            border: 1px solid rgba(0, 212, 255, 0.25);
            font-size: 0.8rem;
            letter-spacing: 3px;
            color: var(--cyan);
            margin-bottom: 22px;
            text-shadow: 0 0 10px var(--cyan-glow);
            animation: heroFadeIn 1s ease 0.15s forwards;
            opacity: 0;
        }
        .hero-name {
            font-family: var(--font-heading);
            font-size: clamp(3.2rem, 8vw, 6.5rem);
            font-weight: 900;
            letter-spacing: -2px;
            color: #fff;
            line-height: 1.05;
            margin-bottom: 8px;
            text-shadow: 0 0 60px rgba(0, 212, 255, 0.5), 0 4px 30px rgba(0, 0, 0, 0.6);
            animation: heroFadeIn 1s ease 0.25s forwards;
            opacity: 0;
            position: relative;
        }
        .hero-name .dot {
            color: var(--cyan);
            text-shadow: 0 0 40px var(--cyan-glow);
        }
        .hero-subtitle {
            font-size: 1.2rem;
            color: var(--text-muted);
            letter-spacing: 2px;
            font-weight: 400;
            margin-bottom: 35px;
            animation: heroFadeIn 1s ease 0.4s forwards;
            opacity: 0;
        }
        .hero-buttons {
            display: flex;
            gap: 16px;
            flex-wrap: wrap;
            justify-content: center;
            animation: heroFadeIn 1s ease 0.55s forwards;
            opacity: 0;
        }
        .btn {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 14px 30px;
            border-radius: 50px;
            font-weight: 600;
            font-size: 0.95rem;
            letter-spacing: 0.5px;
            cursor: pointer;
            text-decoration: none;
            transition: all var(--transition-bounce);
            border: none;
            font-family: var(--font-body);
            position: relative;
            overflow: hidden;
        }
        .btn-primary {
            background: var(--gradient-cyan);
            color: #000;
            box-shadow: var(--shadow-glow-md);
            font-weight: 700;
        }
        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow-glow-lg), 0 15px 35px rgba(0, 0, 0, 0.4);
        }
        .btn-outline {
            background: transparent;
            color: #fff;
            border: 2px solid rgba(255, 255, 255, 0.3);
            backdrop-filter: blur(4px);
        }
        .btn-outline:hover {
            border-color: var(--cyan);
            box-shadow: var(--shadow-glow-sm);
            transform: translateY(-3px);
            background: rgba(0, 212, 255, 0.06);
        }
        .btn::after {
            content: '';
            position: absolute;
            inset: 0;
            border-radius: 50px;
            opacity: 0;
            transition: opacity 0.4s;
            background: radial-gradient(circle at center, rgba(255, 255, 255, 0.2) 0%, transparent 70%);
        }
        .btn:active::after {
            opacity: 1;
            transition: opacity 0s;
        }

        /* ============ ABOUT SECTION ============ */
        .about-grid {
            display: grid;
            grid-template-columns: 280px 1fr;
            gap: 45px;
            align-items: start;
        }
        .about-avatar-wrapper {
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 20px;
        }
        .about-avatar {
            width: 220px;
            height: 220px;
            border-radius: 50%;
            background: var(--bg-card);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 3px solid rgba(0, 212, 255, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 5rem;
            font-weight: 900;
            color: var(--cyan);
            text-shadow: 0 0 50px var(--cyan-glow);
            box-shadow: var(--shadow-glow-md), var(--shadow-card);
            position: relative;
            animation: avatarFloat 4s ease-in-out infinite;
            user-select: none;
        }
        @keyframes avatarFloat {
            0%,
            100% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-14px);
            }
        }
        .about-avatar-ring {
            position: absolute;
            inset: -12px;
            border-radius: 50%;
            border: 2px dashed rgba(0, 212, 255, 0.3);
            animation: ringRotate 20s linear infinite;
            pointer-events: none;
        }
        @keyframes ringRotate {
            to {
                transform: rotate(360deg);
            }
        }
        .about-info-cards {
            display: flex;
            flex-direction: column;
            gap: 14px;
        }
        .info-card {
            background: var(--bg-card);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.06);
            border-radius: var(--radius-md);
            padding: 16px 22px;
            display: flex;
            align-items: center;
            gap: 16px;
            transition: all var(--transition-smooth);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
        }
        .info-card:hover {
            border-color: rgba(0, 212, 255, 0.3);
            box-shadow: var(--shadow-glow-sm), 0 6px 28px rgba(0, 0, 0, 0.4);
            transform: translateX(4px);
        }
        .info-icon {
            width: 44px;
            height: 44px;
            border-radius: 12px;
            background: rgba(0, 212, 255, 0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            color: var(--cyan);
            flex-shrink: 0;
            text-shadow: 0 0 10px var(--cyan-glow);
        }
        .info-text .info-label {
            font-size: 0.7rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: var(--text-muted);
            margin-bottom: 2px;
        }
        .info-text .info-value {
            font-weight: 600;
            color: #fff;
            font-size: 1rem;
        }

        /* ============ DESCRIPTION SECTION ============ */
        .description-card {
            background: var(--bg-card);
            backdrop-filter: blur(18px);
            -webkit-backdrop-filter: blur(18px);
            border: 1px solid rgba(255, 255, 255, 0.07);
            border-radius: var(--radius-lg);
            padding: 35px 40px;
            position: relative;
            box-shadow: var(--shadow-card);
            line-height: 1.9;
            font-size: 1.05rem;
            color: var(--white-soft);
            overflow: hidden;
        }
        .description-card::before {
            content: '';
            position: absolute;
            top: -40px;
            left: -40px;
            width: 100px;
            height: 100px;
            background: var(--cyan);
            border-radius: 50%;
            filter: blur(70px);
            opacity: 0.25;
            pointer-events: none;
        }
        .description-card .quote-mark {
            font-size: 4rem;
            color: var(--cyan);
            opacity: 0.5;
            line-height: 0;
            vertical-align: -20px;
            margin-right: 6px;
            text-shadow: 0 0 30px var(--cyan-glow);
        }

        /* ============ HOBBIES SECTION ============ */
        .hobbies-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 28px;
            perspective: 1200px;
        }
        .hobby-card {
            background: var(--bg-card);
            backdrop-filter: blur(18px);
            -webkit-backdrop-filter: blur(18px);
            border: 1px solid rgba(255, 255, 255, 0.07);
            border-radius: var(--radius-lg);
            padding: 35px 30px;
            text-align: center;
            transition: all var(--transition-smooth);
            box-shadow: var(--shadow-card);
            position: relative;
            cursor: default;
            transform-style: preserve-3d;
            will-change: transform;
        }
        .hobby-card:hover {
            border-color: rgba(0, 212, 255, 0.35);
            box-shadow: var(--shadow-glow-md), 0 15px 45px rgba(0, 0, 0, 0.5);
        }
        .hobby-icon-wrap {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            margin: 0 auto 20px;
            background: rgba(0, 212, 255, 0.08);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.2rem;
            color: var(--cyan);
            text-shadow: 0 0 25px var(--cyan-glow);
            transition: all var(--transition-smooth);
            position: relative;
            z-index: 2;
        }
        .hobby-card:hover .hobby-icon-wrap {
            background: rgba(0, 212, 255, 0.16);
            box-shadow: 0 0 40px rgba(0, 212, 255, 0.35);
            transform: translateZ(25px);
        }
        .hobby-card h3 {
            font-family: var(--font-heading);
            font-size: 1.4rem;
            font-weight: 700;
            margin-bottom: 10px;
            color: #fff;
            position: relative;
            z-index: 2;
            transition: all var(--transition-smooth);
        }
        .hobby-card:hover h3 {
            transform: translateZ(20px);
            text-shadow: 0 0 20px rgba(255, 255, 255, 0.5);
        }
        .hobby-card p {
            color: var(--text-muted);
            font-size: 0.9rem;
            position: relative;
            z-index: 2;
            transition: all var(--transition-smooth);
        }
        .hobby-card:hover p {
            transform: translateZ(15px);
            color: #c5cddb;
        }
        .hobby-card .card-glow {
            position: absolute;
            inset: 0;
            border-radius: var(--radius-lg);
            opacity: 0;
            transition: opacity var(--transition-smooth);
            pointer-events: none;
            background: radial-gradient(ellipse at center, rgba(0, 212, 255, 0.08) 0%, transparent 70%);
            z-index: 1;
        }
        .hobby-card:hover .card-glow {
            opacity: 1;
        }

        /* ============ CAREER GOALS SECTION ============ */
        .career-card {
            background: var(--bg-card);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 2px solid rgba(0, 212, 255, 0.35);
            border-radius: var(--radius-xl);
            padding: 45px 40px;
            text-align: center;
            position: relative;
            box-shadow: var(--shadow-glow-lg), var(--shadow-card);
            overflow: hidden;
            transition: all var(--transition-smooth);
        }
        .career-card::before {
            content: '';
            position: absolute;
            inset: -2px;
            border-radius: var(--radius-xl);
            padding: 2px;
            background: var(--gradient-cyan);
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            opacity: 0.5;
            pointer-events: none;
        }
        .career-card .career-glow-bg {
            position: absolute;
            top: -80px;
            right: -60px;
            width: 250px;
            height: 250px;
            background: var(--cyan);
            border-radius: 50%;
            filter: blur(100px);
            opacity: 0.15;
            pointer-events: none;
        }
        .career-icon-large {
            font-size: 4.5rem;
            color: var(--cyan);
            text-shadow: 0 0 50px var(--cyan-glow);
            margin-bottom: 18px;
            position: relative;
            z-index: 2;
            animation: careerIconPulse 3s ease-in-out infinite;
        }
        @keyframes careerIconPulse {
            0%,
            100% {
                transform: scale(1);
                text-shadow: 0 0 50px var(--cyan-glow);
            }
            50% {
                transform: scale(1.08);
                text-shadow: 0 0 80px var(--cyan-glow), 0 0 120px rgba(0, 212, 255, 0.5);
            }
        }
        .career-card h3 {
            font-family: var(--font-heading);
            font-size: 2rem;
            font-weight: 800;
            color: #fff;
            position: relative;
            z-index: 2;
            margin-bottom: 12px;
        }
        .career-card .career-reason {
            color: var(--white-soft);
            font-size: 1rem;
            max-width: 600px;
            margin: 0 auto;
            position: relative;
            z-index: 2;
            line-height: 1.8;
        }

        /* ============ SKILLS SECTION ============ */
        .skills-container {
            display: flex;
            flex-direction: column;
            gap: 22px;
            max-width: 700px;
        }
        .skill-item {
            display: flex;
            flex-direction: column;
            gap: 8px;
        }
        .skill-header {
            display: flex;
            justify-content: space-between;
            font-weight: 600;
            font-size: 0.9rem;
            color: #fff;
            letter-spacing: 0.5px;
        }
        .skill-header .skill-pct {
            color: var(--cyan);
            text-shadow: 0 0 10px var(--cyan-glow);
        }
        .skill-bar-bg {
            width: 100%;
            height: 10px;
            border-radius: 10px;
            background: rgba(255, 255, 255, 0.06);
            overflow: hidden;
            box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.4);
        }
        .skill-bar-fill {
            height: 100%;
            border-radius: 10px;
            background: var(--gradient-cyan);
            width: 0%;
            transition: width 1.6s cubic-bezier(0.25, 0.1, 0.25, 1);
            box-shadow: 0 0 16px var(--cyan-glow);
            position: relative;
        }
        .skill-bar-fill::after {
            content: '';
            position: absolute;
            right: 0;
            top: 50%;
            transform: translateY(-50%);
            width: 16px;
            height: 16px;
            border-radius: 50%;
            background: #fff;
            box-shadow: 0 0 20px var(--cyan-glow), 0 0 40px rgba(0, 212, 255, 0.6);
        }

        /* ============ STATISTICS SECTION ============ */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
        }
        .stat-card {
            background: var(--bg-card);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.06);
            border-radius: var(--radius-lg);
            padding: 28px 22px;
            text-align: center;
            transition: all var(--transition-smooth);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
            cursor: default;
        }
        .stat-card:hover {
            border-color: rgba(0, 212, 255, 0.3);
            box-shadow: var(--shadow-glow-sm), 0 10px 35px rgba(0, 0, 0, 0.45);
            transform: translateY(-6px);
        }
        .stat-number {
            font-family: var(--font-heading);
            font-size: 2.8rem;
            font-weight: 900;
            color: var(--cyan);
            text-shadow: 0 0 25px var(--cyan-glow);
            line-height: 1;
            margin-bottom: 6px;
        }
        .stat-label {
            font-size: 0.8rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: var(--text-muted);
        }

        /* ============ CONTACT SECTION ============ */
        .contact-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 18px;
            justify-content: center;
        }
        .contact-btn {
            display: inline-flex;
            align-items: center;
            gap: 10px;
            padding: 16px 28px;
            border-radius: 50px;
            font-weight: 600;
            font-size: 1rem;
            text-decoration: none;
            background: var(--bg-card);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            color: #fff;
            transition: all var(--transition-bounce);
            box-shadow: 0 4px 16px rgba(0, 0, 0, 0.3);
            cursor: pointer;
        }
        .contact-btn:hover {
            border-color: var(--cyan);
            box-shadow: var(--shadow-glow-md);
            transform: translateY(-4px);
            color: var(--cyan);
        }
        .contact-btn i {
            font-size: 1.3rem;
            text-shadow: 0 0 10px var(--cyan-glow);
        }

        /* ============ FOOTER ============ */
        .footer {
            text-align: center;
            padding: 35px 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.06);
            position: relative;
            z-index: 1;
            background: rgba(6, 11, 20, 0.7);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
        }
        .footer-copy {
            font-weight: 600;
            color: #fff;
            letter-spacing: 1px;
            margin-bottom: 6px;
            font-size: 0.9rem;
        }
        .footer-tagline {
            color: var(--text-muted);
            font-size: 0.8rem;
            letter-spacing: 2px;
            font-style: italic;
        }

        /* ============ SCROLL REVEAL ============ */
        .reveal {
            opacity: 0;
            transform: translateY(35px);
            transition: opacity 0.8s ease, transform 0.8s cubic-bezier(0.25, 0.1, 0.25, 1);
        }
        .reveal.revealed {
            opacity: 1;
            transform: translateY(0);
        }

        /* ============ RESPONSIVE ============ */
        @media (max-width: 900px) {
            .about-grid {
                grid-template-columns: 1fr;
                text-align: center;
            }
            .about-avatar-wrapper {
                margin: 0 auto;
            }
            .info-card {
                flex-direction: column;
                text-align: center;
                gap: 8px;
            }
            .info-card:hover {
                transform: translateX(0) translateY(-3px);
            }
            .nav-menu {
                position: fixed;
                top: 0;
                right: -100%;
                width: 75%;
                max-width: 340px;
                height: 100vh;
                background: rgba(10, 15, 30, 0.95);
                backdrop-filter: blur(30px);
                -webkit-backdrop-filter: blur(30px);
                flex-direction: column;
                padding: 90px 30px 30px;
                gap: 8px;
                transition: right 0.4s cubic-bezier(0.25, 0.1, 0.25, 1);
                border-left: 1px solid rgba(255, 255, 255, 0.08);
                box-shadow: -10px 0 50px rgba(0, 0, 0, 0.6);
            }
            .nav-menu.open {
                right: 0;
            }
            .nav-menu a {
                font-size: 1.1rem;
                padding: 14px 20px;
                width: 100%;
                text-align: center;
            }
            .nav-hamburger {
                display: flex;
            }
            .section-title {
                font-size: 2rem;
            }
            .hero-name {
                font-size: clamp(2.4rem, 6vw, 4rem);
            }
            .description-card {
                padding: 25px 20px;
                font-size: 0.95rem;
            }
            .career-card {
                padding: 30px 22px;
            }
            .career-card h3 {
                font-size: 1.5rem;
            }
        }
        @media (max-width: 500px) {
            .navbar {
                width: 94%;
                padding: 10px 18px;
                top: 10px;
            }
            .nav-logo {
                font-size: 1.2rem;
                letter-spacing: 2px;
            }
            .section {
                padding: 60px 14px;
            }
            .hero-buttons {
                flex-direction: column;
                align-items: center;
            }
            .btn {
                width: 100%;
                justify-content: center;
                padding: 13px 20px;
            }
            .hobbies-grid {
                grid-template-columns: 1fr;
            }
            .stats-grid {
                grid-template-columns: 1fr 1fr;
                gap: 12px;
            }
            .stat-number {
                font-size: 2rem;
            }
            .contact-grid {
                flex-direction: column;
                align-items: center;
            }
            .contact-btn {
                width: 100%;
                justify-content: center;
            }
            .about-avatar {
                width: 160px;
                height: 160px;
                font-size: 3.5rem;
            }
        }
    </style>
</head>
<body>

    <!-- ==================== LOADING SCREEN ==================== -->
    <div id="loadingScreen">
        <div class="loader-ring"></div>
        <p class="loader-text">Rhevan</p>
    </div>

    <!-- ==================== PARTICLE CANVAS ==================== -->
    <canvas id="particleCanvas"></canvas>

    <!-- ==================== MAIN CONTENT ==================== -->
    <div class="main-content">

        <!-- ========== NAVIGATION ========== -->
        <nav class="navbar" id="navbar">
            <a href="#hero" class="nav-logo">RHEVAN</a>
            <ul class="nav-menu" id="navMenu">
                <li><a href="#hero" class="active">Home</a></li>
                <li><a href="#about">About</a></li>
                <li><a href="#hobbies">Hobbies</a></li>
                <li><a href="#goals">Goals</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
            <button class="nav-hamburger" id="navHamburger" aria-label="Menu">
                <span></span>
                <span></span>
                <span></span>
            </button>
        </nav>

        <!-- ========== HERO SECTION ========== -->
        <section class="hero-section section" id="hero">
            <div class="hero-content">
                <div class="hero-badge">✦ PORTFOLIO 2026 ✦</div>
                <h1 class="hero-name">RHEVAN<span class="dot">.</span></h1>
                <p class="hero-subtitle">Student &nbsp;|&nbsp; Future Civil Engineer</p>
                <div class="hero-buttons">
                    <a href="#about" class="btn btn-primary">
                        <i class="fa-solid fa-compass"></i> Explore Profile
                    </a>
                    <a href="#contact" class="btn btn-outline">
                        <i class="fa-solid fa-paper-plane"></i> Contact Me
                    </a>
                </div>
            </div>
        </section>

        <!-- ========== ABOUT SECTION ========== -->
        <section class="section" id="about">
            <span class="section-label reveal">● About Me</span>
            <h2 class="section-title reveal">Biodata <span class="accent">Pribadi</span></h2>
            <div class="section-divider reveal"></div>
            <div class="about-grid reveal">
                <div class="about-avatar-wrapper">
                    <div class="about-avatar">
                        R
                        <div class="about-avatar-ring"></div>
                    </div>
                </div>
                <div class="about-info-cards">
                    <div class="info-card reveal">
                        <div class="info-icon"><i class="fa-solid fa-user"></i></div>
                        <div class="info-text">
                            <div class="info-label">Nama Lengkap</div>
                            <div class="info-value">Rhevan</div>
                        </div>
                    </div>
                    <div class="info-card reveal">
                        <div class="info-icon"><i class="fa-solid fa-cake-candles"></i></div>
                        <div class="info-text">
                            <div class="info-label">Tanggal Lahir</div>
                            <div class="info-value">06 Januari 2009</div>
                        </div>
                    </div>
                    <div class="info-card reveal">
                        <div class="info-icon"><i class="fa-solid fa-school"></i></div>
                        <div class="info-text">
                            <div class="info-label">Sekolah</div>
                            <div class="info-value">SMA Al Muslim</div>
                        </div>
                    </div>
                    <div class="info-card reveal">
                        <div class="info-icon"><i class="fa-solid fa-heart"></i></div>
                        <div class="info-text">
                            <div class="info-label">Hobi</div>
                            <div class="info-value">Memasak & Boxing</div>
                        </div>
                    </div>
                    <div class="info-card reveal">
                        <div class="info-icon"><i class="fa-solid fa-star"></i></div>
                        <div class="info-text">
                            <div class="info-label">Cita-cita</div>
                            <div class="info-value">Civil Engineer</div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- ========== DESCRIPTION SECTION ========== -->
        <section class="section" id="description">
            <span class="section-label reveal">● Introduction</span>
            <h2 class="section-title reveal">Tentang <span class="accent">Saya</span></h2>
            <div class="section-divider reveal"></div>
            <div class="description-card reveal">
                <span class="quote-mark">"</span>
                Saya adalah siswa SMA Al Muslim yang memiliki minat besar dalam dunia teknik sipil. Saya bercita-cita menjadi seorang <strong>Civil Engineer</strong> yang mampu merancang dan membangun infrastruktur yang bermanfaat bagi masyarakat. Selain memiliki ketertarikan pada bidang teknik, saya juga menikmati kegiatan memasak untuk melatih kreativitas dan <strong>boxing</strong> untuk membangun disiplin, fokus, serta kebugaran fisik.
            </div>
        </section>

        <!-- ========== HOBBIES SECTION ========== -->
        <section class="section" id="hobbies">
            <span class="section-label reveal">● My Passions</span>
            <h2 class="section-title reveal">Hobi <span class="accent">Saya</span></h2>
            <div class="section-divider reveal"></div>
            <div class="hobbies-grid">
                <div class="hobby-card reveal" data-tilt>
                    <div class="card-glow"></div>
                    <div class="hobby-icon-wrap"><i class="fa-solid fa-utensils"></i></div>
                    <h3>Memasak</h3>
                    <p>Melatih kreativitas, ketelitian, dan seni dalam meracik cita rasa. Setiap hidangan adalah karya yang memuaskan hati.</p>
                </div>
                <div class="hobby-card reveal" data-tilt>
                    <div class="card-glow"></div>
                    <div class="hobby-icon-wrap"><i class="fa-solid fa-hand-fist"></i></div>
                    <h3>Boxing</h3>
                    <p>Membangun disiplin tinggi, fokus mental, kekuatan fisik, dan ketahanan diri melalui latihan yang intens dan terstruktur.</p>
                </div>
            </div>
        </section>

        <!-- ========== CAREER GOALS SECTION ========== -->
        <section class="section" id="goals">
            <span class="section-label reveal">● Future Vision</span>
            <h2 class="section-title reveal">Cita-cita <span class="accent">Saya</span></h2>
            <div class="section-divider reveal"></div>
            <div class="career-card reveal">
                <div class="career-glow-bg"></div>
                <div class="career-icon-large"><i class="fa-solid fa-building-columns"></i> <i class="fa-solid fa-ruler-combined"></i></div>
                <h3>Civil Engineer</h3>
                <p class="career-reason">
                    Saya memilih profesi <strong>Civil Engineer</strong> karena saya percaya bahwa infrastruktur yang kokoh adalah fondasi kemajuan sebuah bangsa. Saya ingin merancang jembatan, gedung, dan fasilitas publik yang tidak hanya fungsional tetapi juga estetis dan berkelanjutan. Teknik sipil menggabungkan logika, kreativitas, dan dampak sosial yang nyata &mdash; inilah panggilan hidup saya.
                </p>
            </div>
        </section>

        <!-- ========== SKILLS SECTION ========== -->
        <section class="section" id="skills">
            <span class="section-label reveal">● Competencies</span>
            <h2 class="section-title reveal">Progress <span class="accent">Kemampuan</span></h2>
            <div class="section-divider reveal"></div>
            <div class="skills-container reveal">
                <div class="skill-item">
                    <div class="skill-header"><span>Cooking</span><span class="skill-pct">85%</span></div>
                    <div class="skill-bar-bg"><div class="skill-bar-fill" data-width="85"></div></div>
                </div>
                <div class="skill-item">
                    <div class="skill-header"><span>Boxing</span><span class="skill-pct">90%</span></div>
                    <div class="skill-bar-bg"><div class="skill-bar-fill" data-width="90"></div></div>
                </div>
                <div class="skill-item">
                    <div class="skill-header"><span>Civil Engineering Interest</span><span class="skill-pct">95%</span></div>
                    <div class="skill-bar-bg"><div class="skill-bar-fill" data-width="95"></div></div>
                </div>
            </div>
        </section>

        <!-- ========== STATISTICS SECTION ========== -->
        <section class="section" id="stats">
            <span class="section-label reveal">● Quick Facts</span>
            <h2 class="section-title reveal">Statistik <span class="accent">Singkat</span></h2>
            <div class="section-divider reveal"></div>
            <div class="stats-grid reveal">
                <div class="stat-card">
                    <div class="stat-number">2009</div>
                    <div class="stat-label">Tahun Lahir</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">2</div>
                    <div class="stat-label">Hobi Utama</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number"><i class="fa-solid fa-hard-hat" style="font-size:2.2rem;"></i></div>
                    <div class="stat-label">Civil Engineer</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number"><i class="fa-solid fa-graduation-cap" style="font-size:2.2rem;"></i></div>
                    <div class="stat-label">SMA Al Muslim</div>
                </div>
            </div>
        </section>

        <!-- ========== CONTACT SECTION ========== -->
        <section class="section" id="contact">
            <span class="section-label reveal">● Get In Touch</span>
            <h2 class="section-title reveal">Hubungi <span class="accent">Saya</span></h2>
            <div class="section-divider reveal"></div>
            <div class="contact-grid reveal">
                <a href="mailto:rhevan@example.com" class="contact-btn">
                    <i class="fa-solid fa-envelope"></i> Email
                </a>
                <a href="https://wa.me/6280000000000" target="_blank" rel="noopener" class="contact-btn">
                    <i class="fa-brands fa-whatsapp"></i> WhatsApp
                </a>
                <a href="https://instagram.com/rhevan" target="_blank" rel="noopener" class="contact-btn">
                    <i class="fa-brands fa-instagram"></i> Instagram
                </a>
            </div>
        </section>

        <!-- ========== FOOTER ========== -->
        <footer class="footer">
            <p class="footer-copy">&copy; 2026 Rhevan Portfolio</p>
            <p class="footer-tagline">"Building the Future, One Dream at a Time."</p>
        </footer>
    </div>

    <script>
        (function() {
            // ============ LOADING SCREEN ============
            const loadingScreen = document.getElementById('loadingScreen');
            window.addEventListener('load', () => {
                setTimeout(() => {
                    loadingScreen.classList.add('hidden');
                }, 1200);
            });
            // Fallback: hide loading screen after 3 seconds max
            setTimeout(() => {
                if (!loadingScreen.classList.contains('hidden')) {
                    loadingScreen.classList.add('hidden');
                }
            }, 3000);

            // ============ PARTICLE CANVAS ============
            const canvas = document.getElementById('particleCanvas');
            const ctx = canvas.getContext('2d');
            let particles = [];
            const maxParticles = 90;
            let canvasW, canvasH;

            function resizeCanvas() {
                canvasW = canvas.width = window.innerWidth;
                canvasH = canvas.height = window.innerHeight;
            }
            resizeCanvas();
            window.addEventListener('resize', () => {
                resizeCanvas();
                initParticles();
            });

            class Particle {
                constructor() {
                    this.reset();
                    this.y = Math.random() * canvasH;
                }
                reset() {
                    this.x = Math.random() * canvasW;
                    this.y = -10;
                    this.size = Math.random() * 2.2 + 0.8;
                    this.speedY = Math.random() * 0.45 + 0.15;
                    this.speedX = (Math.random() - 0.5) * 0.35;
                    this.opacity = Math.random() * 0.55 + 0.2;
                    this.flickerSpeed = Math.random() * 0.015 + 0.005;
                }
                update() {
                    this.y += this.speedY;
                    this.x += this.speedX + Math.sin(this.y * 0.005) * 0.2;
                    this.opacity += Math.sin(Date.now() * this.flickerSpeed) * 0.003;
                    this.opacity = Math.max(0.1, Math.min(0.7, this.opacity));
                    if (this.y > canvasH + 10 || this.x < -20 || this.x > canvasW + 20) {
                        this.reset();
                        this.y = -10;
                    }
                }
                draw(ctx) {
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                    ctx.fillStyle = `rgba(0,212,255,${this.opacity})`;
                    ctx.fill();
                    // mini glow
                    ctx.beginPath();
                    ctx.arc(this.x, this.y, this.size * 2.5, 0, Math.PI * 2);
                    ctx.fillStyle = `rgba(0,212,255,${this.opacity * 0.2})`;
                    ctx.fill();
                }
            }

            function initParticles() {
                particles = [];
                for (let i = 0; i < maxParticles; i++) {
                    particles.push(new Particle());
                }
            }
            initParticles();

            function drawConnections() {
                for (let i = 0; i < particles.length; i++) {
                    for (let j = i + 1; j < particles.length; j++) {
                        const dx = particles[i].x - particles[j].x;
                        const dy = particles[i].y - particles[j].y;
                        const dist = Math.sqrt(dx * dx + dy * dy);
                        if (dist < 110) {
                            const alpha = (1 - dist / 110) * 0.22;
                            ctx.beginPath();
                            ctx.moveTo(particles[i].x, particles[i].y);
                            ctx.lineTo(particles[j].x, particles[j].y);
                            ctx.strokeStyle = `rgba(0,212,255,${alpha})`;
                            ctx.lineWidth = 0.6;
                            ctx.stroke();
                        }
                    }
                }
            }

            function animateParticles() {
                ctx.clearRect(0, 0, canvasW, canvasH);
                particles.forEach(p => {
                    p.update();
                    p.draw(ctx);
                });
                drawConnections();
                requestAnimationFrame(animateParticles);
            }
            animateParticles();

            // ============ NAVBAR SCROLL EFFECT ============
            const navbar = document.getElementById('navbar');
            const navMenu = document.getElementById('navMenu');
            const navHamburger = document.getElementById('navHamburger');
            const navLinks = navMenu.querySelectorAll('a');

            window.addEventListener('scroll', () => {
                if (window.scrollY > 50) {
                    navbar.classList.add('scrolled');
                } else {
                    navbar.classList.remove('scrolled');
                }
            });

            // Active nav link on scroll
            const sections = document.querySelectorAll('section[id]');
            window.addEventListener('scroll', () => {
                let current = '';
                sections.forEach(sec => {
                    const top = sec.offsetTop - 200;
                    if (window.scrollY >= top) {
                        current = sec.getAttribute('id');
                    }
                });
                navLinks.forEach(link => {
                    link.classList.remove('active');
                    if (link.getAttribute('href') === '#' + current) {
                        link.classList.add('active');
                    }
                });
            });

            // Hamburger menu
            navHamburger.addEventListener('click', () => {
                navMenu.classList.toggle('open');
                navHamburger.classList.toggle('active');
            });
            navLinks.forEach(link => {
                link.addEventListener('click', () => {
                    navMenu.classList.remove('open');
                    navHamburger.classList.remove('active');
                });
            });
            // Close menu on outside click
            document.addEventListener('click', (e) => {
                if (!navbar.contains(e.target) && navMenu.classList.contains('open')) {
                    navMenu.classList.remove('open');
                    navHamburger.classList.remove('active');
                }
            });

            // ============ SCROLL REVEAL ============
            const revealElements = document.querySelectorAll('.reveal');
            const revealObserver = new IntersectionObserver((entries) => {
                entries.forEach((entry, index) => {
                    if (entry.isIntersecting) {
                        // Stagger effect
                        const delay = Array.from(revealElements).indexOf(entry.target) * 60;
                        setTimeout(() => {
                            entry.target.classList.add('revealed');
                        }, Math.min(delay, 400));
                        revealObserver.unobserve(entry.target);
                    }
                });
            }, {
                threshold: 0.15,
                rootMargin: '0px 0px -40px 0px'
            });
            revealElements.forEach(el => revealObserver.observe(el));

            // ============ SKILL BARS ANIMATION ============
            const skillBars = document.querySelectorAll('.skill-bar-fill');
            const skillsObserver = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const bar = entry.target;
                        const width = bar.getAttribute('data-width');
                        setTimeout(() => {
                            bar.style.width = width + '%';
                        }, 200);
                        skillsObserver.unobserve(bar);
                    }
                });
            }, { threshold: 0.5 });
            skillBars.forEach(bar => skillsObserver.observe(bar));

            // ============ 3D TILT EFFECT ON CARDS ============
            const tiltCards = document.querySelectorAll('[data-tilt]');
            tiltCards.forEach(card => {
                card.addEventListener('mousemove', (e) => {
                    const rect = card.getBoundingClientRect();
                    const x = e.clientX - rect.left;
                    const y = e.clientY - rect.top;
                    const centerX = rect.width / 2;
                    const centerY = rect.height / 2;
                    const rotateX = ((y - centerY) / centerY) * -8;
                    const rotateY = ((x - centerX) / centerX) * 8;
                    card.style.transform =
                        `perspective(900px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale3d(1.03,1.03,1.03)`;
                });
                card.addEventListener('mouseleave', () => {
                    card.style.transform =
                        'perspective(900px) rotateX(0deg) rotateY(0deg) scale3d(1,1,1)';
                });
                card.addEventListener('mouseenter', () => {
                    card.style.transition = 'transform 0.15s ease-out, box-shadow 0.35s ease, border-color 0.35s ease';
                });
                card.addEventListener('mouseleave', () => {
                    card.style.transition =
                        'transform 0.6s cubic-bezier(0.25, 0.1, 0.25, 1), box-shadow 0.35s ease, border-color 0.35s ease';
                });
            });

            // ============ PARALLAX LIGHT ON MOUSE MOVE (HERO) ============
            const heroSection = document.querySelector('.hero-section');
            if (heroSection) {
                heroSection.addEventListener('mousemove', (e) => {
                    const rect = heroSection.getBoundingClientRect();
                    const x = e.clientX - rect.left;
                    const y = e.clientY - rect.top;
                    const pctX = x / rect.width;
                    const pctY = y / rect.height;
                    const moveX = (pctX - 0.5) * 25;
                    const moveY = (pctY - 0.5) * 25;
                    const heroContent = heroSection.querySelector('.hero-content');
                    if (heroContent) {
                        heroContent.style.transform = `translate(${moveX}px, ${moveY}px)`;
                        heroContent.style.transition = 'transform 0.2s ease-out';
                    }
                });
                heroSection.addEventListener('mouseleave', () => {
                    const heroContent = heroSection.querySelector('.hero-content');
                    if (heroContent) {
                        heroContent.style.transform = 'translate(0px, 0px)';
                        heroContent.style.transition = 'transform 0.7s cubic-bezier(0.25, 0.1, 0.25, 1)';
                    }
                });
            }

            // ============ SMOOTH SCROLL FOR ALL ANCHOR LINKS ============
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function(e) {
                    const targetId = this.getAttribute('href');
                    if (targetId === '#') return;
                    const target = document.querySelector(targetId);
                    if (target) {
                        e.preventDefault();
                        const navHeight = navbar.offsetHeight + 30;
                        const top = target.getBoundingClientRect().top + window.pageYOffset -
                            navHeight;
                        window.scrollTo({ top, behavior: 'smooth' });
                    }
                });
            });

            console.log('%c✨ Rhevan Portfolio 2026 %cReady %c🚀',
                'color:#00d4ff;font-size:1.2rem;font-weight:bold;',
                'color:#fff;',
                'color:#00d4ff;');
        })();
    </script>
</body>
</html>
