<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Assignment 9.3 - Combine Flexbox and Grid Responsively</title>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        /* ==========================================================================
           1. GLOBAL STYLES & CSS VARIABLES
           ========================================================================== */
        :root {
            --primary-color: #4f46e5;
            --primary-hover: #4338ca;
            --secondary-color: #06b6d4;
            --accent-color: #f59e0b;
            --text-dark: #0f172a;
            --text-muted: #64748b;
            --bg-light: #f8fafc;
            --bg-white: #ffffff;
            --border-color: #e2e8f0;
            --card-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.05), 0 4px 6px -2px rgba(0, 0, 0, 0.025);
            --card-shadow-hover: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
            --radius-sm: 8px;
            --radius-md: 12px;
            --radius-lg: 20px;
            --transition: all 0.3s ease;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', sans-serif;
            color: var(--text-dark);
            background-color: var(--bg-light);
            line-height: 1.6;
            overflow-x: hidden;
        }

        a {
            text-decoration: none;
            color: inherit;
        }

        ul {
            list-style: none;
        }

        /* Container utility for consistent padding & maximum width */
        .container {
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 1.5rem;
        }

        /* ==========================================================================
           2. HEADER & NAVBAR (FLEXBOX IMPLEMENTATION)
           ========================================================================== */
        /* FLEXBOX USED HERE: Main header container aligns logo, menu links, and call-to-action button horizontally */
        .header {
            position: sticky;
            top: 0;
            z-index: 1000;
            background-color: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--border-color);
            box-shadow: 0 2px 4px rgba(0,0,0,0.02);
        }

        .navbar {
            display: flex; /* [FLEXBOX] Enable flex layout for header elements */
            justify-content: space-between; /* Spread brand logo and nav items to opposite ends */
            align-items: center; /* Vertically center all header items */
            height: 80px;
        }

        .logo {
            display: flex; /* [FLEXBOX] Align icon and text logo */
            align-items: center;
            gap: 0.75rem;
            font-size: 1.5rem;
            font-weight: 800;
            color: var(--primary-color);
        }

        .logo-icon {
            width: 40px;
            height: 40px;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            color: white;
            border-radius: var(--radius-sm);
            display: flex; /* [FLEXBOX] Center icon inside logo box */
            align-items: center;
            justify-content: center;
            font-size: 1.25rem;
        }

        .nav-links {
            display: flex; /* [FLEXBOX] Lay out navbar links in a horizontal row */
            align-items: center;
            gap: 2rem;
        }

        .nav-link {
            font-weight: 500;
            color: var(--text-dark);
            transition: var(--transition);
        }

        .nav-link:hover {
            color: var(--primary-color);
        }

        .nav-actions {
            display: flex; /* [FLEXBOX] Group action buttons together */
            align-items: center;
            gap: 1rem;
        }

        .btn {
            display: inline-flex; /* [FLEXBOX] Center icon/text inside button */
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            padding: 0.75rem 1.5rem;
            font-size: 0.95rem;
            font-weight: 600;
            border-radius: var(--radius-sm);
            transition: var(--transition);
            cursor: pointer;
            border: none;
        }

        .btn-primary {
            background-color: var(--primary-color);
            color: white;
            box-shadow: 0 4px 6px -1px rgba(79, 70, 229, 0.3);
        }

        .btn-primary:hover {
            background-color: var(--primary-hover);
            transform: translateY(-2px);
            box-shadow: 0 6px 12px -2px rgba(79, 70, 229, 0.4);
        }

        .btn-outline {
            background-color: transparent;
            color: var(--text-dark);
            border: 1px solid var(--border-color);
        }

        .btn-outline:hover {
            border-color: var(--primary-color);
            color: var(--primary-color);
        }

        /* Mobile Hamburger Toggle */
        .mobile-toggle {
            display: none;
            background: none;
            border: none;
            font-size: 1.5rem;
            color: var(--text-dark);
            cursor: pointer;
        }

        /* ==========================================================================
           3. HERO SECTION (FLEXBOX / GRID COMBINATION)
           ========================================================================== */
        /* FLEXBOX USED HERE: Main split container for Text Column vs Visual Graphic Column */
        .hero-section {
            padding: 5rem 0;
            background: radial-gradient(circle at 10% 20%, rgba(238, 242, 255, 0.8) 0%, rgba(255, 255, 255, 1) 90%);
        }

        .hero-container {
            display: flex; /* [FLEXBOX] Two-column side-by-side layout for Desktop */
            align-items: center;
            justify-content: space-between;
            gap: 4rem;
        }

        .hero-content {
            flex: 1; /* Take up equal 50% width space on desktop */
        }

        .hero-badge {
            display: inline-flex; /* [FLEXBOX] Inline badge styling */
            align-items: center;
            gap: 0.5rem;
            padding: 0.35rem 0.85rem;
            background-color: rgba(79, 70, 229, 0.1);
            color: var(--primary-color);
            font-size: 0.85rem;
            font-weight: 600;
            border-radius: 50px;
            margin-bottom: 1.5rem;
        }

        .hero-title {
            font-size: 3.25rem;
            line-height: 1.15;
            font-weight: 800;
            color: var(--text-dark);
            margin-bottom: 1.25rem;
            letter-spacing: -0.02em;
        }

        .hero-title span {
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .hero-description {
            font-size: 1.125rem;
            color: var(--text-muted);
            margin-bottom: 2rem;
            max-width: 540px;
        }

        .hero-buttons {
            display: flex; /* [FLEXBOX] Align Hero CTA buttons in a horizontal row */
            gap: 1rem;
            margin-bottom: 2.5rem;
        }

        .hero-stats {
            display: flex; /* [FLEXBOX] Align numerical stat badges */
            gap: 2.5rem;
            padding-top: 1.5rem;
            border-top: 1px solid var(--border-color);
        }

        .stat-item h3 {
            font-size: 1.75rem;
            font-weight: 700;
            color: var(--text-dark);
        }

        .stat-item p {
            font-size: 0.875rem;
            color: var(--text-muted);
        }

        .hero-visual {
            flex: 1; /* Take up equal 50% width space on desktop */
            display: flex; /* [FLEXBOX] Center the hero card image inside container */
            justify-content: center;
        }

        .hero-card-preview {
            width: 100%;
            max-width: 480px;
            background-color: var(--bg-white);
            border-radius: var(--radius-lg);
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.15);
            padding: 2rem;
            border: 1px solid var(--border-color);
            position: relative;
        }

        /* Mock App Interface Graphic */
        .mock-ui-header {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 1.5rem;
        }
        .dot { width: 12px; height: 12px; border-radius: 50%; }
        .dot-red { background-color: #ef4444; }
        .dot-yellow { background-color: #f59e0b; }
        .dot-green { background-color: #10b981; }

        .mock-ui-body {
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }
        .mock-bar {
            height: 12px;
            background-color: #f1f5f9;
            border-radius: 6px;
        }
        .mock-bar-long { width: 85%; }
        .mock-bar-medium { width: 60%; }
        .mock-bar-accent { background: linear-gradient(90deg, var(--primary-color), var(--secondary-color)); height: 40px; border-radius: 8px; }

        /* Floating Badge Accent */
        .floating-badge {
            position: absolute;
            bottom: -20px;
            left: -20px;
            background-color: var(--bg-white);
            padding: 1rem;
            border-radius: var(--radius-md);
            box-shadow: var(--card-shadow-hover);
            display: flex;
            align-items: center;
            gap: 0.75rem;
            border: 1px solid var(--border-color);
        }
        .badge-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background-color: #dcfce7;
            color: #16a34a;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* ==========================================================================
           4. FEATURES SECTION (CSS GRID + FLEXBOX COMBINATION)
           ========================================================================== */
        .features-section {
            padding: 6rem 0;
            background-color: var(--bg-white);
        }

        .section-header {
            text-align: center;
            max-width: 650px;
            margin: 0 auto 4rem auto;
        }

        .section-tag {
            color: var(--primary-color);
            font-weight: 700;
            text-transform: uppercase;
            font-size: 0.85rem;
            letter-spacing: 0.05em;
            margin-bottom: 0.5rem;
            display: block;
        }

        .section-title {
            font-size: 2.25rem;
            font-weight: 800;
            color: var(--text-dark);
            margin-bottom: 1rem;
            letter-spacing: -0.01em;
        }

        .section-subtitle {
            font-size: 1.05rem;
            color: var(--text-muted);
        }

        /* 
           GRID USED HERE: Main layout of the 6 feature cards using CSS Grid.
           Grid automatically handles 3 equal columns across desktop screens.
        */
        .features-grid {
            display: grid; /* [CSS GRID] Main multi-column layout engine */
            grid-template-columns: repeat(3, 1fr); /* 3 Equal width columns on desktop */
            gap: 2rem; /* Uniform row and column spacing */
        }

        /* 
           FLEXBOX USED HERE: Internal layout of each Card. 
           Flexbox flex-direction: column allows content to stretch smoothly and 
           align action buttons to the exact bottom of cards regardless of text length.
        */
        .card {
            background-color: var(--bg-white);
            border: 1px solid var(--border-color);
            border-radius: var(--radius-md);
            padding: 2rem;
            box-shadow: var(--card-shadow);
            transition: var(--transition);
            
            display: flex; /* [FLEXBOX] Card internal layout */
            flex-direction: column; /* Stack contents vertically */
            align-items: flex-start; /* Align content left */
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: var(--card-shadow-hover);
            border-color: rgba(79, 70, 229, 0.3);
        }

        .card-icon {
            width: 54px;
            height: 54px;
            border-radius: var(--radius-sm);
            background-color: rgba(79, 70, 229, 0.08);
            color: var(--primary-color);
            display: flex; /* [FLEXBOX] Center icon in container box */
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            margin-bottom: 1.5rem;
            transition: var(--transition);
        }

        .card:hover .card-icon {
            background-color: var(--primary-color);
            color: white;
        }

        .card-title {
            font-size: 1.25rem;
            font-weight: 700;
            color: var(--text-dark);
            margin-bottom: 0.75rem;
        }

        .card-description {
            color: var(--text-muted);
            font-size: 0.95rem;
            margin-bottom: 1.5rem;
            flex-grow: 1; /* [FLEXBOX MAGICA] Forces text to expand so action links align at card bottom */
        }

        .card-link {
            display: inline-flex; /* [FLEXBOX] Align arrow icon with link text */
            align-items: center;
            gap: 0.5rem;
            color: var(--primary-color);
            font-weight: 600;
            font-size: 0.9rem;
            transition: var(--transition);
        }

        .card-link i {
            transition: transform 0.2s ease;
        }

        .card-link:hover i {
            transform: translateX(4px);
        }

        /* ==========================================================================
           5. FOOTER SECTION (FLEXBOX & GRID MIX)
           ========================================================================== */
        .footer {
            background-color: #0f172a;
            color: white;
            padding: 4rem 0 2rem 0;
        }

        .footer-grid {
            display: grid; /* [CSS GRID] Footer multi-column layout */
            grid-template-columns: 2fr repeat(3, 1fr);
            gap: 3rem;
            margin-bottom: 3rem;
        }

        .footer-brand p {
            color: #94a3b8;
            margin-top: 1rem;
            max-width: 300px;
        }

        .footer-column h4 {
            font-size: 1rem;
            font-weight: 700;
            margin-bottom: 1.25rem;
            color: #f8fafc;
        }

        .footer-links {
            display: flex; /* [FLEXBOX] Vertical list layout */
            flex-direction: column;
            gap: 0.75rem;
        }

        .footer-links a {
            color: #94a3b8;
            transition: var(--transition);
        }

        .footer-links a:hover {
            color: white;
        }

        .footer-bottom {
            display: flex; /* [FLEXBOX] Align copyright & social icons horizontally */
            justify-content: space-between;
            align-items: center;
            padding-top: 2rem;
            border-top: 1px solid #1e293b;
            color: #64748b;
            font-size: 0.9rem;
        }

        .social-links {
            display: flex; /* [FLEXBOX] Lay out social media icons */
            gap: 1rem;
        }

        .social-icon {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background-color: #1e293b;
            color: #94a3b8;
            display: flex; /* [FLEXBOX] Center icon inside circular box */
            align-items: center;
            justify-content: center;
            transition: var(--transition);
        }

        .social-icon:hover {
            background-color: var(--primary-color);
            color: white;
        }

        /* ==========================================================================
           6. RESPONSIVE MEDIA QUERIES (MOBILE RESPONSIVENESS)
           ========================================================================== */
        /* Tablet Breakpoint (< 1024px) */
        @media screen and (max-width: 1024px) {
            .features-grid {
                grid-template-columns: repeat(2, 1fr); /* [GRID RESPONSIVE] Switch to 2 columns on tablet */
            }
            .footer-grid {
                grid-template-columns: 1fr 1fr;
                gap: 2rem;
            }
        }

        /* Mobile Breakpoint (< 768px) - MANDATORY ASSIGNMENT REQUIREMENT */
        @media screen and (max-width: 768px) {
            /* 1. Navbar adjustments for Mobile */
            .nav-links, .nav-actions {
                display: none; /* Hide standard navigation links on mobile */
            }
            .nav-links.active {
                display: flex; /* Toggle display when hamburger button is clicked */
                flex-direction: column;
                position: absolute;
                top: 80px;
                left: 0;
                width: 100%;
                background-color: white;
                padding: 1.5rem;
                box-shadow: 0 10px 15px rgba(0,0,0,0.1);
                border-bottom: 1px solid var(--border-color);
            }
            .mobile-toggle {
                display: block; /* Show hamburger button on mobile screens */
            }

            /* 2. Hero Section adjustments for Mobile */
            .hero-container {
                flex-direction: column; /* [FLEXBOX RESPONSIVE] Stack text & image vertically */
                gap: 3rem;
                text-align: center;
            }

            .hero-description {
                margin-left: auto;
                margin-right: auto;
            }

            .hero-title {
                font-size: 2.25rem;
            }

            .hero-buttons {
                justify-content: center; /* Center CTA buttons on mobile screens */
                flex-direction: column;
                width: 100%;
            }

            .hero-buttons .btn {
                width: 100%; /* Full-width buttons on mobile */
            }

            .hero-stats {
                justify-content: center; /* Center stats row on mobile screens */
            }

            /* 3. Features Grid adjustments for Mobile */
            .features-grid {
                grid-template-columns: 1fr; /* [GRID RESPONSIVE] Single-column stacked layout on mobile */
            }

            /* 4. Footer adjustments for Mobile */
            .footer-grid {
                grid-template-columns: 1fr; /* Single column for footer navigation */
            }

            .footer-bottom {
                flex-direction: column;
                gap: 1rem;
                text-align: center;
            }
        }
    </style>
</head>
<body>

    <!-- ==========================================================================
         HEADER & NAVIGATION BAR (FLEXBOX)
         ========================================================================== -->
    <header class="header">
        <div class="container">
            <!-- Navbar uses Flexbox for main horizontal distribution -->
            <nav class="navbar">
                <!-- Flexbox element: Logo -->
                <a href="#" class="logo">
                    <div class="logo-icon">
                        <i class="fa-solid fa-layer-group"></i>
                    </div>
                    <span>FlexGrid</span>
                </a>

                <!-- Flexbox element: Nav Links -->
                <ul class="nav-links" id="navLinks">
                    <li><a href="#hero" class="nav-link">Home</a></li>
                    <li><a href="#features" class="nav-link">Features</a></li>
                    <li><a href="#about" class="nav-link">About</a></li>
                    <li><a href="#pricing" class="nav-link">Pricing</a></li>
                </ul>

                <!-- Flexbox element: CTA Action Buttons -->
                <div class="nav-actions">
                    <a href="#" class="btn btn-outline">Log In</a>
                    <a href="#" class="btn btn-primary">Get Started</a>
                </div>

                <!-- Mobile Navigation Toggle Button -->
                <button class="mobile-toggle" id="mobileToggle" aria-label="Toggle Navigation Menu">
                    <i class="fa-solid fa-bars"></i>
                </button>
            </nav>
        </div>
    </header>

    <!-- ==========================================================================
         HERO SECTION (FLEXBOX DETAILED ALIGNMENT)
         ========================================================================== -->
    <section class="hero-section" id="hero">
        <!-- Hero Container uses Flexbox row on desktop, flex-direction column on mobile -->
        <div class="container hero-container">
            
            <!-- Flex Column 1: Hero Text & Call-To-Action Content -->
            <div class="hero-content">
                <div class="hero-badge">
                    <i class="fa-solid fa-wand-magic-sparkles"></i>
                    Assignment 9.3 Demo
                </div>
                <h1 class="hero-title">Master Layouts with <span>Flexbox & Grid</span></h1>
                <p class="hero-description">
                    Build perfectly responsive web applications by pairing CSS Grid's powerful 2D layout capabilities with Flexbox's precise 1D item positioning.
                </p>
                <div class="hero-buttons">
                    <a href="#features" class="btn btn-primary">
                        Explore Features <i class="fa-solid fa-arrow-right"></i>
                    </a>
                    <a href="#" class="btn btn-outline">
                        <i class="fa-solid fa-circle-play"></i> Watch Video
                    </a>
                </div>

                <!-- Flex items for Statistics -->
                <div class="hero-stats">
                    <div class="stat-item">
                        <h3>100%</h3>
                        <p>Responsive</p>
                    </div>
                    <div class="stat-item">
                        <h3>CSS Grid</h3>
                        <p>Main Layout</p>
                    </div>
                    <div class="stat-item">
                        <h3>Flexbox</h3>
                        <p>Components</p>
                    </div>
                </div>
            </div>

            <!-- Flex Column 2: Graphic / UI Visual Preview -->
            <div class="hero-visual">
                <div class="hero-card-preview">
                    <div class="mock-ui-header">
                        <div class="dot dot-red"></div>
                        <div class="dot dot-yellow"></div>
                        <div class="dot dot-green"></div>
                    </div>
                    <div class="mock-ui-body">
                        <div class="mock-bar mock-bar-accent"></div>
                        <div class="mock-bar mock-bar-long"></div>
                        <div class="mock-bar mock-bar-medium"></div>
                        <div class="mock-bar mock-bar-long"></div>
                    </div>
                    <div class="floating-badge">
                        <div class="badge-icon">
                            <i class="fa-solid fa-check"></i>
                        </div>
                        <div>
                            <strong style="display: block; font-size: 0.9rem;">Clean Code Structure</strong>
                            <span style="font-size: 0.75rem; color: var(--text-muted);">Fully Responsive</span>
                        </div>
                    </div>
                </div>
            </div>

        </div>
    </section>

    <!-- ==========================================================================
         MAIN FEATURES SECTION (CSS GRID + FLEXBOX FOR CARDS)
         ========================================================================== -->
    <section class="features-section" id="features">
        <div class="container">
            
            <!-- Section Title Header -->
            <div class="section-header">
                <span class="section-tag">Core Capabilities</span>
                <h2 class="section-title">Designed for Modern Web Standards</h2>
                <p class="section-subtitle">Demonstrating CSS Grid layout structure with internal Flexbox alignment for UI card components.</p>
            </div>

            <!-- 
               CSS GRID CONTAINER:
               Serves as the main multi-column wrapper for feature cards (3 Columns Desktop, 1 Column Mobile)
            -->
            <div class="features-grid">

                <!-- Feature Card 1 (Flexbox applied internally) -->
                <article class="card">
                    <div class="card-icon">
                        <i class="fa-solid fa-table-cells-large"></i>
                    </div>
                    <h3 class="card-title">CSS Grid Architecture</h3>
                    <p class="card-description">Utilized for two-dimensional main page structures, governing major columns, rows, and page-wide component distribution.</p>
                    <a href="#" class="card-link">Learn Grid System <i class="fa-solid fa-chevron-right"></i></a>
                </article>

                <!-- Feature Card 2 -->
                <article class="card">
                    <div class="card-icon">
                        <i class="fa-solid fa-arrows-left-right-to-line"></i>
                    </div>
                    <h3 class="card-title">Flexbox Alignment</h3>
                    <p class="card-description">Applied for linear one-dimensional item alignment inside components like headers, navigation bars, and card interiors.</p>
                    <a href="#" class="card-link">Explore Flexbox <i class="fa-solid fa-chevron-right"></i></a>
                </article>

                <!-- Feature Card 3 -->
                <article class="card">
                    <div class="card-icon">
                        <i class="fa-solid fa-mobile-screen-button"></i>
                    </div>
                    <h3 class="card-title">Mobile First Breakpoints</h3>
                    <p class="card-description">Converts multi-column desktop arrangements into vertical single-column layouts for small screen sizes below 768px.</p>
                    <a href="#" class="card-link">View Media Queries <i class="fa-solid fa-chevron-right"></i></a>
                </article>

                <!-- Feature Card 4 -->
                <article class="card">
                    <div class="card-icon">
                        <i class="fa-solid fa-paint-brush"></i>
                    </div>
                    <h3 class="card-title">Modern Design Tokens</h3>
                    <p class="card-description">Incorporates subtle shadows, soft border radiuses, curated modern color palettes, and smooth interactive hover states.</p>
                    <a href="#" class="card-link">Check Typography <i class="fa-solid fa-chevron-right"></i></a>
                </article>

                <!-- Feature Card 5 -->
                <article class="card">
                    <div class="card-icon">
                        <i class="fa-solid fa-bolt"></i>
                    </div>
                    <h3 class="card-title">Equal Height Cards</h3>
                    <p class="card-description">Flexbox flex-grow ensures button actions align perfectly to the bottom edge of cards regardless of variable content length.</p>
                    <a href="#" class="card-link">Read Case Study <i class="fa-solid fa-chevron-right"></i></a>
                </article>

                <!-- Feature Card 6 -->
                <article class="card">
                    <div class="card-icon">
                        <i class="fa-solid fa-code"></i>
                    </div>
                    <h3 class="card-title">Semantic & Clean HTML</h3>
                    <p class="card-description">Structured using standards-compliant HTML5 sectioning elements for enhanced code accessibility and readability.</p>
                    <a href="#" class="card-link">Inspect Code <i class="fa-solid fa-chevron-right"></i></a>
                </article>

            </div>
        </div>
    </section>

    <!-- ==========================================================================
         FOOTER SECTION (HYBRID LAYOUT)
         ========================================================================== -->
    <footer class="footer">
        <div class="container">
            <!-- Footer Multi-column layout using CSS Grid -->
            <div class="footer-grid">
                <div class="footer-brand">
                    <div class="logo">
                        <div class="logo-icon">
                            <i class="fa-solid fa-layer-group"></i>
                        </div>
                        <span style="color: white;">FlexGrid</span>
                    </div>
                    <p>Building scalable modern user interfaces combining CSS Grid and Flexbox layouts efficiently.</p>
                </div>

                <div class="footer-column">
                    <h4>Product</h4>
                    <ul class="footer-links">
                        <li><a href="#">Overview</a></li>
                        <li><a href="#">Features</a></li>
                        <li><a href="#">Solutions</a></li>
                        <li><a href="#">Tutorials</a></li>
                    </ul>
                </div>

                <div class="footer-column">
                    <h4>Resources</h4>
                    <ul class="footer-links">
                        <li><a href="#">Documentation</a></li>
                        <li><a href="#">CSS Guidelines</a></li>
                        <li><a href="#">Community</a></li>
                        <li><a href="#">API Reference</a></li>
                    </ul>
                </div>

                <div class="footer-column">
                    <h4>Company</h4>
                    <ul class="footer-links">
                        <li><a href="#">About Us</a></li>
                        <li><a href="#">Careers</a></li>
                        <li><a href="#">Privacy Policy</a></li>
                        <li><a href="#">Contact</a></li>
                    </ul>
                </div>
            </div>

            <!-- Footer bottom bar using Flexbox horizontal alignment -->
            <div class="footer-bottom">
                <p>&copy; 2026 FlexGrid Assignment 9.3 Demo. All rights reserved.</p>
                <div class="social-links">
                    <a href="#" class="social-icon" aria-label="Twitter"><i class="fa-brands fa-twitter"></i></a>
                    <a href="#" class="social-icon" aria-label="GitHub"><i class="fa-brands fa-github"></i></a>
                    <a href="#" class="social-icon" aria-label="LinkedIn"><i class="fa-brands fa-linkedin-in"></i></a>
                </div>
            </div>
        </div>
    </footer>

    <!-- Simple JavaScript snippet for Mobile Menu Toggle -->
    <script>
        const mobileToggle = document.getElementById('mobileToggle');
        const navLinks = document.getElementById('navLinks');

        mobileToggle.addEventListener('click', () => {
            navLinks.classList.toggle('active');
            const icon = mobileToggle.querySelector('i');
            if (navLinks.classList.contains('active')) {
                icon.classList.remove('fa-bars');
                icon.classList.add('fa-xmark');
            } else {
                icon.classList.remove('fa-xmark');
                icon.classList.add('fa-bars');
            }
        });
    </script>
</body>
</html>