<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Padma Massage & Spa - Premium Lively UI</title>
    
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600&family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

    <style>
        /* --- 1. DESIGN SYSTEM (LIVELY GOLD & WHITE) --- */
        :root {
            --gold: #c5a059;
            --gold-hover: #d4af37;
            --light-bg: #fdfbf7;
            --glass-bg: rgba(255, 255, 255, 0.8);
            --glass-border: rgba(197, 160, 89, 0.2);
            --text-main: #333333;
            --text-muted: #666666;
            --transition-smooth: 0.5s cubic-bezier(0.25, 0.8, 0.25, 1);
            --shadow-soft: 0 10px 40px rgba(0, 0, 0, 0.08);
        }

        /* --- 2. BASE RESET --- */
        * { margin: 0; padding: 0; box-sizing: border-box; }

        body, html {
            height: 100%;
            font-family: 'Montserrat', sans-serif;
            background-color: var(--light-bg);
            color: var(--text-main);
            overflow-x: hidden;
            scroll-behavior: smooth;
        }

        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--light-bg); }
        ::-webkit-scrollbar-thumb { background: var(--gold); border-radius: 10px; }

        /* --- 3. BACKGROUND ENGINE --- */
        .app-container {
            position: relative;
            min-height: 100vh;
            width: 100%;
            display: flex;
            flex-direction: column;
        }

        .app-container::before {
            content: '';
            position: fixed;
            top: 0; left: 0;
            width: 100vw; height: 100vh;
            background-image: linear-gradient(to bottom, rgba(255,255,255,0.4), var(--light-bg)), 
                              url('zien.jpg');
            background-size: cover;
            background-position: center;
            z-index: -1;
            transform: translateZ(0); 
            will-change: transform;
        }

        /* --- 4. NAVIGATION ENGINE --- */
        input[type="radio"].nav-radio { display: none; }

        .views-wrapper {
            display: grid;
            grid-template-columns: 1fr;
            width: 100%;
            flex-grow: 1;
        }

        .view-section {
            grid-row: 1; grid-column: 1;
            display: flex; flex-direction: column; align-items: center;
            width: 100%; opacity: 0; visibility: hidden;
            pointer-events: none; transform: translateY(15px) scale(0.98);
            height: 0; overflow: hidden; padding: 0 5%;
            transition: opacity 0.3s ease-out, transform 0.3s ease-out, height 0s 0.3s, visibility 0s 0.3s, padding 0s 0.3s;
            z-index: 1;
        }

        #tab-home:checked ~ .app-container .views-wrapper #home-view,
        #tab-products:checked ~ .app-container .views-wrapper #products-view,
        #tab-booking:checked ~ .app-container .views-wrapper #booking-view,
        #tab-contact:checked ~ .app-container .views-wrapper #contact-view,
        #tab-faqs:checked ~ .app-container .views-wrapper #faqs-view,
        #tab-login:checked ~ .app-container .views-wrapper #login-view,
        #tab-admin:checked ~ .app-container .views-wrapper #admin-view {
            opacity: 1; visibility: visible; pointer-events: auto;
            transform: translateY(0) scale(1); height: auto; overflow: visible;
            padding: 120px 5% 60px 5%; z-index: 2;
            transition: height 0s, padding 0s, visibility 0s, opacity 0.5s ease-out 0.1s, transform 0.5s ease-out 0.1s;
        }

        /* --- 5. NAVBAR --- */
        .navbar {
            display: flex; justify-content: space-between; align-items: center;
            padding: 25px 5%; width: 100%; position: fixed; top: 0; left: 0; z-index: 100;
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--glass-border);
        }

        .logo-text { font-family: 'Playfair Display', serif; font-size: 24px; color: var(--gold); font-weight: 700; letter-spacing: 2px; cursor: pointer; }
        .nav-links { display: flex; list-style: none; gap: 40px; }
        .nav-links label { color: var(--text-main); font-size: 13px; text-transform: uppercase; letter-spacing: 1px; cursor: pointer; position: relative; transition: color 0.3s ease; }
        
        #tab-home:checked ~ .app-container .nav-home, 
        #tab-products:checked ~ .app-container .nav-products, 
        #tab-contact:checked ~ .app-container .nav-contact, 
        #tab-faqs:checked ~ .app-container .nav-faqs,
        #tab-login:checked ~ .app-container .nav-login { color: var(--gold); font-weight: 600; border-bottom: 2px solid var(--gold); }

        /* --- 6. UI ELEMENTS --- */
        .btn-gold {
            background-color: var(--gold); color: #fff;
            padding: 14px 35px; font-size: 12px; font-weight: 600; text-transform: uppercase;
            letter-spacing: 1px; border-radius: 30px; border: 1px solid var(--gold);
            cursor: pointer; transition: all 0.3s ease; display: inline-flex; align-items: center; justify-content: center; gap: 10px; text-decoration: none;
        }

        .btn-gold:hover { background-color: #fff; color: var(--gold); transform: translateY(-3px); box-shadow: var(--shadow-soft); }

        .glass-card {
            background: var(--glass-bg); border: 1px solid var(--glass-border);
            border-radius: 12px; padding: 40px 30px; text-align: center;
            backdrop-filter: blur(12px); transition: all 0.4s ease; display: flex; flex-direction: column; justify-content: space-between;
            height: 100%;
        }

        .glass-card:hover { transform: translateY(-10px); background: #fff; box-shadow: var(--shadow-soft); }
        .glass-card i { font-size: 32px; color: var(--gold); margin-bottom: 15px; }
        .glass-card h3 { font-size: 16px; margin-bottom: 10px; text-transform: uppercase; }
        .glass-card p { font-size: 12px; color: var(--text-muted); margin-bottom: 15px; line-height: 1.5; flex-grow: 1; }
        .glass-card .price { font-size: 20px; font-weight: 700; color: var(--gold); margin-bottom: 25px; }

        .form-container {
            background: #ffffff; border: 1px solid var(--glass-border);
            padding: 50px; border-radius: 12px; width: 100%; max-width: 500px; box-shadow: var(--shadow-soft);
        }

        .input-group { margin-bottom: 20px; text-align: left; }
        .input-group label { display: block; font-size: 11px; text-transform: uppercase; margin-bottom: 8px; color: var(--gold); font-weight: 600; }
        .input-group input, .input-group select { width: 100%; padding: 15px; background: #f9f9f9; border: 1px solid #eee; border-radius: 6px; font-family: inherit; }

        .category-title { color: var(--gold); border-bottom: 1px solid var(--glass-border); padding-bottom: 10px; text-align: left; width: 100%; max-width: 1200px; text-transform: uppercase; letter-spacing: 2px; margin-bottom: 25px; margin-top: 40px;}

        @media (max-width: 768px) { .nav-links { display: none; } }
    </style>
</head>
<body>

    <input type="radio" name="tabs" id="tab-home" class="nav-radio" checked>
    <input type="radio" name="tabs" id="tab-products" class="nav-radio">
    <input type="radio" name="tabs" id="tab-booking" class="nav-radio"> 
    <input type="radio" name="tabs" id="tab-contact" class="nav-radio">
    <input type="radio" name="tabs" id="tab-faqs" class="nav-radio">
    <input type="radio" name="tabs" id="tab-login" class="nav-radio">
    <input type="radio" name="tabs" id="tab-admin" class="nav-radio">

    <div class="app-container">
        
        <nav class="navbar">
            <label for="tab-home" class="logo-text">PADMA</label>
            <ul class="nav-links">
                <li><label for="tab-home" class="nav-home">Home</label></li>
                <li><label for="tab-products" class="nav-products">Services</label></li>
                <li><label for="tab-contact" class="nav-contact">Contact</label></li>
                <li><label for="tab-faqs" class="nav-faqs">FAQs</label></li>
                <li><label for="tab-login" class="nav-login"><i class="far fa-user"></i> Admin</label></li>
            </ul>
        </nav>

        <div class="views-wrapper">
            
            <div id="home-view" class="view-section">
                <img src="image-removebg-preview.png" alt="Padma Logo" style="width: 100%; max-width: 280px; margin-bottom: 20px;">
                <h1 style="font-family: 'Playfair Display'; font-size: clamp(45px, 8vw, 75px);">PADMA</h1>
                <div style="letter-spacing: 4px; color: var(--gold); font-size: 11px; margin-bottom: 10px;">ESTABLISHED 2010</div>
                <h2 style="font-family: 'Playfair Display'; letter-spacing: 6px; color: var(--text-muted); margin-bottom: 40px;">MASSAGE & SPA</h2>
                <label for="tab-products" class="btn-gold">Explore Services <i class="fas fa-chevron-right"></i></label>
            </div>

            <div id="products-view" class="view-section">
                <div class="section-header"><h2 style="font-size: 40px; font-family: 'Playfair Display';">Our Treatments</h2><p style="color: var(--text-muted); margin-top: 10px;">Elevate your well-being with our premium selection.</p></div>
                
                <h3 class="category-title">Signature (1 Hour)</h3>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 30px; width: 100%; max-width: 1200px;">
                    <div class="glass-card"><i class="fas fa-spa"></i><h3>Padma Signature</h3><p>A combination of relaxing Swedish massage and focused Shiatsu deep tissue.</p><div class="price">₱480.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                    <div class="glass-card"><i class="fas fa-child"></i><h3>Back Massage</h3><p>Full body massage mostly focused on the upper & lower back and shoulders.</p><div class="price">₱530.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                    <div class="glass-card"><i class="fas fa-shoe-prints"></i><h3>Foot Massage</h3><p>A relaxing and stimulating massage which combines reflexology techniques.</p><div class="price">₱450.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                    <div class="glass-card"><i class="fas fa-leaf"></i><h3>Foot Scrub (45 Mins)</h3><p>Treat your feet to a soothing and pampering foot scrub for renewed vitality.</p><div class="price">₱400.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                </div>

                <h3 class="category-title">Specialty (1 Hour)</h3>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 30px; width: 100%; max-width: 1200px;">
                    <div class="glass-card"><i class="fas fa-fire"></i><h3>Ventosa</h3><p>Our Signature Massage coupled with the old tradition of suction cupping.</p><div class="price">₱620.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                    <div class="glass-card"><i class="fas fa-fire-alt"></i><h3>Hot Stone</h3><p>A deeply relaxing type of massage therapy using smooth, heated Hot Stones.</p><div class="price">₱620.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                    <div class="glass-card"><i class="fas fa-pump-soap"></i><h3>Aromatherapy</h3><p>Our Signature Massage with relaxing scented essential oil and thermal pack.</p><div class="price">₱650.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                    <div class="glass-card"><i class="fas fa-spa"></i><h3>Foot Revival (90 Mins)</h3><p>A blissful combo of our pampering foot scrub & relaxing foot massage.</p><div class="price">₱650.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                </div>

                <h3 class="category-title">Packages (2 Hours)</h3>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 30px; width: 100%; max-width: 1200px;">
                    <div class="glass-card"><i class="fas fa-yin-yang"></i><h3>Signature & Foot</h3><p>The ultimate 2-hour combination of full body and foot relaxation.</p><div class="price">₱890.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                    <div class="glass-card"><i class="fas fa-bed"></i><h3>Back & Foot</h3><p>Focused targeted relief for your back, shoulders, and tired feet.</p><div class="price">₱940.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                    <div class="glass-card"><i class="fas fa-gem"></i><h3>Premium Back (90 Mins)</h3><p>Choose between Hot Stone (₱880), Ventosa (₱880), or Aromatherapy (₱920).</p><div class="price">From ₱880</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                    <div class="glass-card"><i class="fas fa-heart"></i><h3>Stress Relief (2.5 Hrs)</h3><p>1-hour whole body aroma massage + thermal pack + 90min Foot Revival.</p><div class="price">₱1,090.00</div><label for="tab-booking" class="btn-gold">Book Now</label></div>
                </div>

                <h3 class="category-title">Add-Ons</h3>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 30px; width: 100%; max-width: 1200px; margin-bottom: 50px;">
                    <div class="glass-card" style="padding: 20px 30px; flex-direction: row; align-items: center;"><h3 style="margin: 0;">Signature Massage +30 Mins</h3><div class="price" style="margin: 0;">₱300.00</div></div>
                    <div class="glass-card" style="padding: 20px 30px; flex-direction: row; align-items: center;"><h3 style="margin: 0;">Scented Oil</h3><div class="price" style="margin: 0;">₱50.00</div></div>
                </div>
            </div>

            <div id="booking-view" class="view-section">
                <div class="form-container">
                    <h2 style="margin-bottom: 30px; color: var(--gold); font-family: 'Playfair Display'; text-align: center;">Reservation</h2>
                    <form onsubmit="return false;">
                        <div class="input-group"><label>Full Name</label><input type="text" placeholder="John Doe" required></div>
                        <div class="input-group"><label>Phone</label><input type="tel" placeholder="09xxxxxxxxx" required></div>
                        
                        <div class="input-group">
                            <label>Select Service</label>
                            <select required>
                                <option value="" disabled selected>-- Choose a Treatment --</option>
                                <optgroup label="Signature">
                                    <option>Padma Signature Massage</option>
                                    <option>Back Massage</option>
                                    <option>Foot Massage</option>
                                    <option>Foot Scrub</option>
                                </optgroup>
                                <optgroup label="Specialty">
                                    <option>Ventosa</option>
                                    <option>Hot Stone Massage</option>
                                    <option>Aromatherapy Massage</option>
                                    <option>Foot Revival Therapy</option>
                                </optgroup>
                                <optgroup label="Packages">
                                    <option>Signature & Foot Massage</option>
                                    <option>Back & Foot Massage</option>
                                    <option>Premium Back Massage</option>
                                    <option>Stress Relief Package</option>
                                </optgroup>
                            </select>
                        </div>
                        
                        <div class="input-group"><label>Date & Time</label><input type="datetime-local" required></div>
                        <label for="tab-home" class="btn-gold" style="width: 100%; cursor: pointer;">Confirm Booking</label>
                    </form>
                </div>
            </div>

            <div id="contact-view" class="view-section">
                <div class="form-container" style="max-width: 600px;">
                    <h2 style="margin-bottom: 30px; font-family: 'Playfair Display'; color: var(--gold);">Get In Touch</h2>
                    <p style="margin-bottom: 20px;"><i class="fas fa-map-marker-alt" style="color:var(--gold); width: 30px;"></i> Tomas Saco 6th, Nazareth, CDO</p>
                    <p style="margin-bottom: 20px;"><i class="fas fa-phone-alt" style="color:var(--gold); width: 30px;"></i> 0997 274 0648</p>
                    <p style="margin-bottom: 20px;"><i class="fas fa-envelope" style="color:var(--gold); width: 30px;"></i> hrpadma2025@gmail.com</p>
                    <p><i class="fab fa-facebook-messenger" style="color:var(--gold); width: 30px;"></i> Padma Massage & Spa</p>
                </div>
            </div>

            <div id="faqs-view" class="view-section">
                <div class="section-header"><h2>FAQs</h2></div>
                <div class="glass-card" style="max-width: 800px; text-align: left; width: 100%;">
                    <h4 style="color: var(--gold); margin-bottom: 10px;">Do I need to book in advance?</h4>
                    <p style="margin-bottom: 20px;">We recommend booking at least 24 hours in advance to secure your preferred slot.</p>
                    <h4 style="color: var(--gold); margin-bottom: 10px;">What is your cancellation policy?</h4>
                    <p>Please notify us at least 2 hours before your schedule for any changes.</p>
                </div>
            </div>

            <div id="login-view" class="view-section">
                <div class="form-container" style="max-width: 400px;">
                    <h2 style="margin-bottom: 30px; text-align: center;">Staff Login</h2>
                    <div class="input-group"><input type="text" placeholder="Username"></div>
                    <div class="input-group"><input type="password" placeholder="Password"></div>
                    <label for="tab-admin" class="btn-gold" style="width: 100%; cursor: pointer;">Enter</label>
                </div>
            </div>

            <div id="admin-view" class="view-section">
                <div style="width: 100%; max-width: 900px;">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 30px;">
                        <h2>Bookings Dashboard</h2>
                        <label for="tab-home" style="color: var(--gold); cursor: pointer;">Logout</label>
                    </div>
                    <div class="glass-card" style="flex-direction: row; justify-content: space-between; align-items: center; padding: 20px;">
                        <div style="text-align: left;"><p><strong>Reinz Ebarat</strong></p><p style="font-size: 12px; color: var(--text-muted);">0997 274 0648 | April 10, 2026 | Hot Stone Massage</p></div>
                        <button style="border:none; color:#ff5555; background:none; cursor:pointer; font-weight: 600;">Remove</button>
                    </div>
                </div>
            </div>

        </div> 
    </div>
</body>
</html>
