<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Dubai Mall - Interactive Sales Deck</title>
    <meta name="description" content="Experience the world's largest shopping mall. Explore retail, luxury, dining, attractions, and events.">
    
    <!-- Preconnect to external resources -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Sora:wght@400;500;600;700&family=Playfair+Display:wght@400;700&display=swap" rel="stylesheet">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-color: #000;
            --secondary-color: #fff;
            --accent-gold: #d4af37;
            --accent-dark-gray: #1a1a1a;
            --accent-light-gray: #f5f5f5;
            --text-primary: #000;
            --text-secondary: #666;
            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }

        html {
            scroll-behavior: smooth;
            overflow-x: hidden;
        }

        body {
            font-family: 'Sora', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            color: var(--text-primary);
            background: var(--secondary-color);
            line-height: 1.6;
        }

        /* ========== NAVIGATION ========== */
        nav {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            z-index: 1000;
            background: rgba(0, 0, 0, 0.95);
            backdrop-filter: blur(10px);
            padding: 1.5rem 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: var(--transition);
        }

        nav.scrolled {
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
        }

        .logo {
            font-family: 'Playfair Display', serif;
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--accent-gold);
            letter-spacing: 2px;
        }

        .nav-links {
            display: flex;
            gap: 2rem;
            list-style: none;
        }

        .nav-links a {
            color: var(--secondary-color);
            text-decoration: none;
            font-size: 0.9rem;
            font-weight: 500;
            letter-spacing: 1px;
            text-transform: uppercase;
            position: relative;
            transition: var(--transition);
        }

        .nav-links a:hover {
            color: var(--accent-gold);
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--accent-gold);
            transition: var(--transition);
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            color: var(--secondary-color);
            font-size: 1.5rem;
            cursor: pointer;
        }

        /* ========== HERO SECTION ========== */
        .hero {
            position: relative;
            height: 100vh;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-top: 60px;
        }

        .hero-video {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            z-index: 0;
        }

        .hero-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.2) 100%);
            z-index: 1;
        }

        .hero-content {
            position: relative;
            z-index: 2;
            text-align: center;
            color: var(--secondary-color);
            animation: fadeInUp 1s ease-out;
        }

        .hero-content h1 {
            font-family: 'Playfair Display', serif;
            font-size: clamp(2rem, 8vw, 5rem);
            font-weight: 700;
            margin-bottom: 1rem;
            letter-spacing: -1px;
            line-height: 1.1;
        }

        .hero-content p {
            font-size: clamp(0.95rem, 2vw, 1.25rem);
            max-width: 600px;
            margin: 0 auto 2rem;
            letter-spacing: 0.5px;
            opacity: 0.9;
        }

        .cta-primary {
            display: inline-block;
            padding: 1rem 3rem;
            background: var(--accent-gold);
            color: var(--primary-color);
            text-decoration: none;
            font-weight: 600;
            letter-spacing: 1px;
            text-transform: uppercase;
            border: 2px solid var(--accent-gold);
            transition: var(--transition);
            cursor: pointer;
            border-radius: 0;
            font-size: 0.85rem;
        }

        .cta-primary:hover {
            background: transparent;
            color: var(--accent-gold);
        }

        /* ========== SCROLL INDICATOR ========== */
        .scroll-indicator {
            position: absolute;
            bottom: 2rem;
            left: 50%;
            transform: translateX(-50%);
            z-index: 2;
            animation: bounce 2s infinite;
        }

        .scroll-indicator svg {
            width: 24px;
            height: 24px;
            stroke: var(--secondary-color);
            stroke-width: 2;
        }

        @keyframes bounce {
            0%, 100% { transform: translateX(-50%) translateY(0); }
            50% { transform: translateX(-50%) translateY(10px); }
        }

        /* ========== SECTIONS ========== */
        section {
            padding: 6rem 2rem;
        }

        section.dark {
            background: var(--accent-dark-gray);
            color: var(--secondary-color);
        }

        section.light {
            background: var(--secondary-color);
            color: var(--text-primary);
        }

        section.light-gray {
            background: var(--accent-light-gray);
            color: var(--text-primary);
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        .section-title {
            font-family: 'Playfair Display', serif;
            font-size: clamp(2rem, 5vw, 3.5rem);
            font-weight: 700;
            margin-bottom: 3rem;
            text-align: center;
            position: relative;
            letter-spacing: -0.5px;
        }

        .section-title::after {
            content: '';
            display: block;
            width: 60px;
            height: 3px;
            background: var(--accent-gold);
            margin: 1rem auto 0;
        }

        /* ========== OVERVIEW SECTION ========== */
        .overview-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 2rem;
            margin-top: 3rem;
        }

        .stat-card {
            padding: 2rem;
            background: var(--accent-dark-gray);
            color: var(--secondary-color);
            border-left: 4px solid var(--accent-gold);
            transition: var(--transition);
        }

        .stat-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }

        .stat-number {
            font-family: 'Playfair Display', serif;
            font-size: 2.5rem;
            font-weight: 700;
            color: var(--accent-gold);
            margin-bottom: 0.5rem;
        }

        .stat-label {
            font-size: 0.9rem;
            letter-spacing: 1px;
            text-transform: uppercase;
            opacity: 0.8;
        }

        /* ========== IMAGE GRID ========== */
        .image-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
            margin-top: 3rem;
        }

        .image-item {
            position: relative;
            overflow: hidden;
            aspect-ratio: 16/9;
            background: var(--accent-light-gray);
        }

        .image-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: var(--transition);
        }

        .image-item:hover img {
            transform: scale(1.05);
        }

        /* ========== VIDEO SECTION ========== */
        .video-container {
            position: relative;
            width: 100%;
            aspect-ratio: 16/9;
            background: #000;
            border-radius: 8px;
            overflow: hidden;
            margin: 2rem 0;
        }

        .video-container iframe,
        .video-container video {
            width: 100%;
            height: 100%;
        }

        /* ========== LUXURY SECTION ========== */
        .luxury-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 3rem;
            align-items: center;
            margin-top: 3rem;
        }

        .luxury-text h3 {
            font-family: 'Playfair Display', serif;
            font-size: 2rem;
            margin-bottom: 1.5rem;
            color: var(--accent-gold);
        }

        .luxury-text p {
            margin-bottom: 1rem;
            line-height: 1.8;
            color: var(--text-secondary);
        }

        /* ========== ATTRACTIONS CAROUSEL ========== */
        .attractions-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            margin-top: 3rem;
        }

        .attraction-card {
            background: var(--secondary-color);
            overflow: hidden;
            border-radius: 4px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            transition: var(--transition);
        }

        .attraction-card:hover {
            transform: translateY(-12px);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
        }

        .attraction-image {
            width: 100%;
            height: 200px;
            background: var(--accent-light-gray);
            overflow: hidden;
        }

        .attraction-image img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .attraction-content {
            padding: 2rem;
        }

        .attraction-content h4 {
            font-family: 'Playfair Display', serif;
            font-size: 1.3rem;
            margin-bottom: 0.5rem;
        }

        .attraction-content p {
            font-size: 0.9rem;
            color: var(--text-secondary);
            line-height: 1.6;
        }

        /* ========== EVENTS SECTION ========== */
        .events-timeline {
            position: relative;
            padding: 2rem 0;
            margin-top: 3rem;
        }

        .event-item {
            display: grid;
            grid-template-columns: 200px 1fr;
            gap: 2rem;
            margin-bottom: 3rem;
            align-items: center;
        }

        .event-date {
            font-family: 'Playfair Display', serif;
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--accent-gold);
        }

        .event-details h4 {
            font-size: 1.2rem;
            margin-bottom: 0.5rem;
        }

        .event-details p {
            color: var(--text-secondary);
        }

        /* ========== CTA SECTION ========== */
        .cta-section {
            text-align: center;
            padding: 4rem 2rem;
        }

        .cta-section h2 {
            font-family: 'Playfair Display', serif;
            font-size: 2.5rem;
            margin-bottom: 1.5rem;
        }

        .cta-buttons {
            display: flex;
            gap: 1rem;
            justify-content: center;
            flex-wrap: wrap;
            margin-top: 2rem;
        }

        .cta-secondary {
            display: inline-block;
            padding: 1rem 2rem;
            background: transparent;
            color: var(--secondary-color);
            border: 2px solid var(--secondary-color);
            text-decoration: none;
            font-weight: 600;
            letter-spacing: 1px;
            text-transform: uppercase;
            transition: var(--transition);
            cursor: pointer;
            border-radius: 0;
            font-size: 0.85rem;
        }

        .cta-secondary:hover {
            background: var(--secondary-color);
            color: var(--primary-color);
        }

        /* ========== FOOTER ========== */
        footer {
            background: var(--primary-color);
            color: var(--secondary-color);
            padding: 3rem 2rem;
            text-align: center;
            border-top: 1px solid rgba(212, 175, 55, 0.2);
        }

        .footer-content {
            max-width: 1400px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            text-align: left;
            margin-bottom: 2rem;
        }

        .footer-section h4 {
            font-family: 'Playfair Display', serif;
            color: var(--accent-gold);
            margin-bottom: 1rem;
        }

        .footer-section a {
            display: block;
            color: var(--secondary-color);
            text-decoration: none;
            font-size: 0.9rem;
            margin-bottom: 0.5rem;
            transition: var(--transition);
        }

        .footer-section a:hover {
            color: var(--accent-gold);
        }

        .footer-bottom {
            text-align: center;
            padding-top: 2rem;
            border-top: 1px solid rgba(212, 175, 55, 0.2);
            font-size: 0.85rem;
        }

        /* ========== ANIMATIONS ========== */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        .fade-in {
            animation: fadeIn 0.8s ease-out forwards;
        }

        /* ========== RESPONSIVE ========== */
        @media (max-width: 768px) {
            nav {
                padding: 1rem 1.5rem;
            }

            .logo {
                font-size: 1.2rem;
            }

            .nav-links {
                display: none;
                position: absolute;
                top: 100%;
                left: 0;
                right: 0;
                flex-direction: column;
                gap: 0;
                background: rgba(0, 0, 0, 0.98);
                padding: 2rem;
            }

            .nav-links.active {
                display: flex;
            }

            .mobile-menu-btn {
                display: block;
            }

            .hero {
                margin-top: 60px;
            }

            section {
                padding: 3rem 1rem;
            }

            .luxury-grid {
                grid-template-columns: 1fr;
            }

            .event-item {
                grid-template-columns: 1fr;
            }

            .cta-buttons {
                flex-direction: column;
            }

            .cta-primary,
            .cta-secondary {
                width: 100%;
            }

            .overview-grid {
                grid-template-columns: 1fr;
            }
        }

        /* ========== LOADING STATE ========== */
        .loading {
            display: inline-block;
            width: 20px;
            height: 20px;
            border: 3px solid var(--accent-light-gray);
            border-radius: 50%;
            border-top-color: var(--accent-gold);
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* ========== UTILITIES ========== */
        .text-gold {
            color: var(--accent-gold);
        }

        .text-center {
            text-align: center;
        }

        .mt-4 {
            margin-top: 2rem;
        }

        .mb-4 {
            margin-bottom: 2rem;
        }

        .opacity-75 {
            opacity: 0.75;
        }

        /* ========== SCROLLING STYLES ========== */
        ::-webkit-scrollbar {
            width: 10px;
        }

        ::-webkit-scrollbar-track {
            background: var(--accent-light-gray);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--accent-gold);
            border-radius: 5px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #c59b1f;
        }
    </style>
</head>
<body>
    <!-- ========== NAVIGATION ========== -->
    <nav id="navbar">
        <div class="logo">THE DUBAI MALL</div>
        <ul class="nav-links" id="navLinks">
            <li><a href="#hero">Home</a></li>
            <li><a href="#overview">Overview</a></li>
            <li><a href="#retail">Retail</a></li>
            <li><a href="#luxury">Luxury</a></li>
            <li><a href="#dining">Dining</a></li>
            <li><a href="#attractions">Attractions</a></li>
            <li><a href="#events">Events</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
        <button class="mobile-menu-btn" id="mobileMenuBtn">☰</button>
    </nav>

    <!-- ========== HERO SECTION ========== -->
    <section id="hero" class="hero">
        <video class="hero-video" autoplay muted playsinline>
            <source src="https://videos.pexels.com/video-files/6234484/6234484-sd_640_360_25fps.mp4" type="video/mp4">
            Your browser doesn't support HTML5 video.
        </video>
        <div class="hero-overlay"></div>
        <div class="hero-content">
            <h1>The World's Largest Shopping Destination</h1>
            <p>More than 14 million visitors annually. A global platform for retail, luxury, dining, and unforgettable experiences.</p>
            <a href="#overview" class="cta-primary">Explore Now</a>
        </div>
        <div class="scroll-indicator">
            <svg viewBox="0 0 24 24" fill="none">
                <path d="M12 5v14M5 12l7 7 7-7" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
        </div>
    </section>

    <!-- ========== OVERVIEW SECTION ========== -->
    <section id="overview" class="light">
        <div class="container">
            <h2 class="section-title">Why The Dubai Mall</h2>
            <div class="overview-grid">
                <div class="stat-card">
                    <div class="stat-number">14M+</div>
                    <div class="stat-label">Annual Visitors</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">1.2M</div>
                    <div class="stat-label">Sq. Meters of Space</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">1,200+</div>
                    <div class="stat-label">Retail Outlets</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">200+</div>
                    <div class="stat-label">Food & Beverage</div>
                </div>
            </div>
            <div class="image-grid">
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1555041469-a586c61ea9bc?w=600&h=400&fit=crop" alt="Mall Exterior">
                </div>
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1560707303-4e980ce876ad?w=600&h=400&fit=crop" alt="Shopping Area">
                </div>
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1552820728-8ac41f1ce891?w=600&h=400&fit=crop" alt="Dining Area">
                </div>
            </div>
        </div>
    </section>

    <!-- ========== RETAIL SECTION ========== -->
    <section id="retail" class="dark">
        <div class="container">
            <h2 class="section-title">Retail Excellence</h2>
            <p style="max-width: 800px; margin: 0 auto 3rem; text-align: center; font-size: 1.1rem;">
                Home to the world's most iconic brands. From luxury flagships to emerging designers, every tenant finds their audience here.
            </p>
            <div class="image-grid">
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1540932424986-7c899166e7c0?w=600&h=400&fit=crop" alt="Luxury Brands">
                </div>
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1541961017774-22349e4a1262?w=600&h=400&fit=crop" alt="Fashion District">
                </div>
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1488459716781-6918f33427d7?w=600&h=400&fit=crop" alt="Retail Space">
                </div>
            </div>
        </div>
    </section>

    <!-- ========== LUXURY SECTION ========== -->
    <section id="luxury" class="light-gray">
        <div class="container">
            <h2 class="section-title">Luxury Experience</h2>
            <div class="luxury-grid">
                <div class="luxury-text">
                    <h3>The Gold Souk</h3>
                    <p>Experience unparalleled luxury in our exclusive Gold Souk, where over 300 jewelry retailers showcase the finest craftsmanship. A destination within a destination, attracting connoisseurs from around the world.</p>
                    <p>Premium positioning, curated clientele, and world-class customer experience make this a beacon for high-value transactions.</p>
                </div>
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1599643478518-a784e5dc4c8f?w=600&h=400&fit=crop" alt="Luxury Shopping">
                </div>
            </div>
        </div>
    </section>

    <!-- ========== DINING & LIFESTYLE ========== -->
    <section id="dining" class="dark">
        <div class="container">
            <h2 class="section-title">Dining & Lifestyle</h2>
            <p style="max-width: 800px; margin: 0 auto 3rem; text-align: center; font-size: 1.1rem; color: var(--secondary-color);">
                200+ restaurants and cafés. From Michelin-starred fine dining to casual global cuisine. A culinary destination that drives traffic and extends dwell time.
            </p>
            <div class="image-grid">
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1553632332-f34513eac054?w=600&h=400&fit=crop" alt="Fine Dining">
                </div>
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1544025162-d76694265947?w=600&h=400&fit=crop" alt="Café Culture">
                </div>
                <div class="image-item">
                    <img src="https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=600&h=400&fit=crop" alt="Restaurant">
                </div>
            </div>
        </div>
    </section>

    <!-- ========== ATTRACTIONS & ENTERTAINMENT ========== -->
    <section id="attractions" class="light">
        <div class="container">
            <h2 class="section-title">Attractions & Entertainment</h2>
            <div class="attractions-container">
                <div class="attraction-card">
                    <div class="attraction-image">
                        <img src="https://images.unsplash.com/photo-1566073771259-6a8506099945?w=400&h=250&fit=crop" alt="Aquarium">
                    </div>
                    <div class="attraction-content">
                        <h4>Dubai Aquarium</h4>
                        <p>World's largest single acrylic panel. Home to 33,000 animals. A draw that brings 2M+ visitors annually and extends property dwell.</p>
                    </div>
                </div>
                <div class="attraction-card">
                    <div class="attraction-image">
                        <img src="https://images.unsplash.com/photo-1464207687429-7505649dae38?w=400&h=250&fit=crop" alt="Cinema">
                    </div>
                    <div class="attraction-content">
                        <h4>Entertainment Complex</h4>
                        <p>Premium cinema, live entertainment venues, and immersive experiences. Year-round programming that drives consistent foot traffic.</p>
                    </div>
                </div>
                <div class="attraction-card">
                    <div class="attraction-image">
                        <img src="https://images.unsplash.com/photo-1533622599810-5c68f61ba5b8?w=400&h=250&fit=crop" alt="Skating Rink">
                    </div>
                    <div class="attraction-content">
                        <h4>Olympic Ice Rink</h4>
                        <p>Full-size ice skating facility. Sports programming, family entertainment, and community events. A lifestyle amenity that differentiates the property.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ========== EVENTS & PLATFORM ========== -->
    <section id="events" class="dark">
        <div class="container">
            <h2 class="section-title">Events & Brand Activation</h2>
            <p style="max-width: 800px; margin: 0 auto 3rem; text-align: center; font-size: 1.1rem; color: var(--secondary-color);">
                A global platform for product launches, concerts, celebrity appearances, and corporate events. The mall hosts over 800 events annually.
            </p>
            <div class="events-timeline">
                <div class="event-item">
                    <div class="event-date">2024</div>
                    <div class="event-details">
                        <h4>Fashion Week 2024</h4>
                        <p>Global fashion brands showcase new collections. 500K+ visitors, 100+ brands, 2-week immersive experience.</p>
                    </div>
                </div>
                <div class="event-item">
                    <div class="event-date">2024</div>
                    <div class="event-details">
                        <h4>Celebrity Concert Series</h4>
                        <p>Premium entertainment programming with world-renowned artists. Enhanced brand visibility and audience engagement.</p>
                    </div>
                </div>
                <div class="event-item">
                    <div class="event-date">2024</div>
                    <div class="event-details">
                        <h4>Corporate Activations</h4>
                        <p>Dedicated event spaces for product launches, trade shows, and brand experiences. From 100-person boardrooms to 10K+ capacity venues.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- ========== CONTACT / CTA SECTION ========== -->
    <section id="contact" class="light-gray">
        <div class="container">
            <div class="cta-section">
                <h2>Ready to Be Part of the Story?</h2>
                <p style="max-width: 700px; margin: 1.5rem auto; color: var(--text-secondary); font-size: 1.1rem;">
                    Join 14 million visitors annually. Partner with the world's leading mixed-use destination.
                </p>
                <div class="cta-buttons">
                    <a href="mailto:leasing@thedubaimall.com" class="cta-primary">Leasing Inquiry</a>
                    <a href="mailto:partnerships@thedubaimall.com" class="cta-primary">Sponsorship</a>
                    <a href="mailto:events@thedubaimall.com" class="cta-primary">Book an Event</a>
                </div>
            </div>
        </div>
    </section>

    <!-- ========== FOOTER ========== -->
    <footer>
        <div class="footer-content">
            <div class="footer-section">
                <h4>The Dubai Mall</h4>
                <p style="font-size: 0.9rem; margin-bottom: 1rem;">The world's largest shopping destination.</p>
            </div>
            <div class="footer-section">
                <h4>Quick Links</h4>
                <a href="#retail">Retail</a>
                <a href="#luxury">Luxury</a>
                <a href="#dining">Dining</a>
                <a href="#attractions">Attractions</a>
                <a href="#events">Events</a>
            </div>
            <div class="footer-section">
                <h4>Contact</h4>
                <a href="mailto:info@thedubaimall.com">info@thedubaimall.com</a>
                <a href="tel:+971123456789">+971 1 234 56789</a>
                <a href="#">Commercial Inquiries</a>
            </div>
            <div class="footer-section">
                <h4>Follow Us</h4>
                <a href="https://instagram.com" target="_blank">Instagram</a>
                <a href="https://twitter.com" target="_blank">Twitter</a>
                <a href="https://facebook.com" target="_blank">Facebook</a>
                <a href="https://linkedin.com" target="_blank">LinkedIn</a>
            </div>
        </div>
        <div class="footer-bottom">
            <p>&copy; 2024 The Dubai Mall. All rights reserved.</p>
        </div>
    </footer>

    <script>
        // ========== NAVIGATION FUNCTIONALITY ==========
        const navbar = document.getElementById('navbar');
        const navLinks = document.getElementById('navLinks');
        const mobileMenuBtn = document.getElementById('mobileMenuBtn');

        // Scroll detection
        window.addEventListener('scroll', () => {
            if (window.scrollY > 100) {
                navbar.classList.add('scrolled');
            } else {
                navbar.classList.remove('scrolled');
            }
        });

        // Mobile menu toggle
        mobileMenuBtn.addEventListener('click', () => {
            navLinks.classList.toggle('active');
        });

        // Close mobile menu when clicking a link
        document.querySelectorAll('.nav-links a').forEach(link => {
            link.addEventListener('click', () => {
                navLinks.classList.remove('active');
            });
        });

        // ========== LAZY LOADING IMAGES ==========
        if ('IntersectionObserver' in window) {
            const imageObserver = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        const img = entry.target;
                        if (img.dataset.src) {
                            img.src = img.dataset.src;
                            img.removeAttribute('data-src');
                        }
                        imageObserver.unobserve(img);
                    }
                });
            });

            document.querySelectorAll('img[data-src]').forEach(img => {
                imageObserver.observe(img);
            });
        }

        // ========== FADE-IN ANIMATION ON SCROLL ==========
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -100px 0px'
        };

        const fadeInObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('fade-in');
                }
            });
        }, observerOptions);

        // Add fade-in class to sections
        document.querySelectorAll('section').forEach(section => {
            section.style.opacity = '0';
            fadeInObserver.observe(section);
        });

        // ========== SMOOTH ANCHOR SCROLL ==========
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                const href = this.getAttribute('href');
                if (href !== '#' && document.querySelector(href)) {
                    e.preventDefault();
                    const target = document.querySelector(href);
                    const offsetTop = target.offsetTop - 60;
                    window.scrollTo({
                        top: offsetTop,
                        behavior: 'smooth'
                    });
                }
            });
        });

        // ========== PERFORMANCE OPTIMIZATION ==========
        // Pause videos when out of view
        const videos = document.querySelectorAll('video');
        const videoObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.play();
                } else {
                    entry.target.pause();
                }
            });
        }, { threshold: 0.5 });

        videos.forEach(video => videoObserver.observe(video));

        // ========== ANALYTICS PLACEHOLDER ==========
        function trackEvent(eventName, eventData) {
            console.log(`Event: ${eventName}`, eventData);
            // Connect to Google Analytics or similar
        }

        // Track CTA clicks
        document.querySelectorAll('.cta-primary, .cta-secondary').forEach(btn => {
            btn.addEventListener('click', () => {
                trackEvent('CTA_Clicked', {
                    text: btn.textContent,
                    href: btn.href
                });
            });
        });

        console.log('Sales Deck loaded successfully');
    </script>
</body>
</html>
