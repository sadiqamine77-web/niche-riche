<!DOCTYPE html>
<html lang="fr" dir="ltr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Niche Riche | Parfumerie de Luxe</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700&family=Cormorant+Garamond:wght@300;400;500;600;700&family=Montserrat:wght@200;300;400;500;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-primary: #0a0a0a;
            --bg-secondary: #141414;
            --bg-card: #1a1a1a;
            --gold: #c9a962;
            --gold-light: #d4af37;
            --gold-dark: #a68b4c;
            --cream: #f5f0e8;
            --border: #2a2a2a;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; scroll-behavior: smooth; }
        
        body {
            font-family: 'Montserrat', sans-serif;
            background: var(--bg-primary);
            color: var(--cream);
            overflow-x: hidden;
        }

        /* Support Arabe */
        html[lang="ar"] body { font-family: 'Cairo', sans-serif; }
        .font-display { font-family: 'Cormorant Garamond', serif; }
        html[lang="ar"] .font-display { font-family: 'Cairo', sans-serif; }

        /* Animations */
        @keyframes shimmer { 0% { background-position: -200% center; } 100% { background-position: 200% center; } }
        .gold-shimmer {
            background: linear-gradient(90deg, var(--gold-dark), var(--gold-light), var(--gold-dark));
            background-size: 200% auto;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: shimmer 3s linear infinite;
        }

        .product-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            transition: all 0.4s cubic-bezier(0.165, 0.84, 0.44, 1);
        }
        .product-card:hover {
            transform: translateY(-10px);
            border-color: var(--gold);
            box-shadow: 0 15px 40px rgba(201, 169, 98, 0.15);
        }

        .btn-primary { background: linear-gradient(135deg, var(--gold), var(--gold-dark)); color: black; transition: 0.3s; }
        .btn-primary:hover { transform: scale(1.02); filter: brightness(1.1); }
        .btn-secondary { border: 1px solid var(--gold); color: var(--gold); transition: 0.3s; }
        .btn-secondary:hover { background: var(--gold); color: black; }

        .lang-btn { transition: 0.3s; cursor: pointer; color: #666; }
        .lang-btn.active { color: var(--gold); font-weight: bold; }
        
        #particles { position: fixed; inset: 0; pointer-events: none; z-index: 0; }
        .particle { position: absolute; background: var(--gold); border-radius: 50%; opacity: 0.2; }

        /* Spinner Loading */
        .spinner {
            display: inline-block; width: 14px; height: 14px;
            border: 2px solid rgba(0,0,0,0.2); border-radius: 50%;
            border-top-color: #000; animation: spin 0.8s linear infinite;
            margin-left: 8px; vertical-align: middle;
        }
        @keyframes spin { to { transform: rotate(360deg); } }
        .loading { pointer-events: none; opacity: 0.8; }
    </style>
</head>
<body>
    <div id="particles"></div>

    <nav class="fixed top-0 w-full z-50 bg-black/90 backdrop-blur-md border-b border-white/5">
        <div class="max-w-7xl mx-auto px-6 py-4 flex justify-between items-center">
            <div class="flex items-center gap-2">
                <span class="font-display text-2xl font-bold gold-shimmer tracking-tighter">NICHE RICHE</span>
            </div>
            
            <div class="hidden md:flex gap-8 text-[10px] tracking-[0.2em] uppercase">
                <a href="#collection" class="hover:text-[var(--gold)] transition-colors" data-i18n="nav_collection">Collection</a>
                <a href="#histoire" class="hover:text-[var(--gold)] transition-colors" data-i18n="nav_history">Histoire</a>
                <a href="#contact" class="hover:text-[var(--gold)] transition-colors" data-i18n="nav_contact">Contact</a>
            </div>

            <div class="flex items-center gap-6">
                <div class="flex gap-3 text-[10px] border-r border-white/10 pr-4">
                    <button onclick="changeLang('fr')" class="lang-btn active" data-lang="fr">FR</button>
                    <button onclick="changeLang('ar')" class="lang-btn" data-lang="ar">AR</button>
                    <button onclick="changeLang('en')" class="lang-btn" data-lang="en">EN</button>
                </div>
                <button class="relative hover:text-[var(--gold)] transition-colors" id="cartToggle">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" stroke-width="1.2"/></svg>
                    <span id="cartCount" class="absolute -top-2 -right-2 bg-[var(--gold)] text-black text-[9px] w-4 h-4 rounded-full flex items-center justify-center font-bold">0</span>
                </button>
            </div>
        </div>
    </nav>

    <section class="h-screen flex flex-col justify-center items-center text-center px-6 relative">
        <div class="absolute inset-0 bg-[radial-gradient(circle_at_center,rgba(201,169,98,0.05)_0%,transparent_70%)]"></div>
        <h1 class="font-display text-5xl md:text-8xl mb-6 relative z-10">
            <span data-i18n="hero_title">L'Essence du</span><br>
            <span class="gold-shimmer font-bold" data-i18n="hero_gold">Prestige</span>
        </h1>
        <p class="max-w-xl text-gray-400 mb-10 text-sm md:text-base leading-relaxed" data-i18n="hero_desc">Une collection rare de fragrances conçues pour ceux qui exigent l'exceptionnel.</p>
        <a href="#collection" class="btn-primary px-12 py-4 text-[10px] tracking-[0.3em] uppercase font-bold relative z-10" data-i18n="hero_btn">Découvrir</a>
    </section>

    <section id="collection" class="py-24 max-w-7xl mx-auto px-6">
        <div class="text-center mb-16">
            <h2 class="font-display text-4xl md:text-5xl" data-i18n="col_title">La Collection</h2>
            <div class="w-24 h-px bg-[var(--gold)] mx-auto mt-4"></div>
        </div>
        <div id="grid" class="grid grid-cols-1 md:grid-cols-3 gap-10">
            </div>
    </section>

    <div id="cartModal" class="fixed inset-0 bg-black/95 z-[60] hidden flex justify-end">
        <div class="w-full max-w-md bg-[var(--bg-secondary)] h-full p-8 border-l border-white/10 overflow-y-auto">
            <div class="flex justify-between items-center mb-10">
                <h3 class="font-display text-3xl" data-i18n="cart_title">Mon Panier</h3>
                <button id="cartClose" class="text-gray-500 hover:text-white transition-colors text-2xl">✕</button>
            </div>
            
            <div id="cartItems" class="space-y-4 mb-8">
                </div>

            <div class="border-t border-white/10 pt-8 space-y-4">
                <h4 class="text-[10px] tracking-[0.2em] uppercase text-[var(--gold)] font-bold" data-i18n="delivery_info">Informations de livraison</h4>
                <input type="text" id="custName" data-i18n-placeholder="placeholder_name" placeholder="Nom Complet" class="w-full bg-white/5 border border-white/10 p-4 text-sm focus:outline-none focus:border-[var(--gold)] text-white">
                <input type="text" id="custCity" data-i18n-placeholder="placeholder_city" placeholder="Ville" class="w-full bg-white/5 border border-white/10 p-4 text-sm focus:outline-none focus:border-[var(--gold)] text-white">
                
                <div class="flex justify-between items-center pt-4 mb-4">
                    <span class="text-gray-400 uppercase text-xs tracking-widest" data-i18n="total">Total</span>
                    <span id="totalPrice" class="text-[var(--gold)] text-2xl font-bold font-display">0 DH</span>
                </div>
                
                <button onclick="sendWhatsApp(event)" id="waBtn" class="btn-primary w-full py-5 text-[10px] font-bold uppercase tracking-[0.2em]">
                    <span data-i18n="checkout">Commander via WhatsApp</span>
                </button>
            </div>
        </div>
    </div>

    <script>
        // 1. Configuration & Traductions
        const translations = {
            fr: {
                nav_collection: "Collection", nav_history: "Histoire", nav_contact: "Contact",
                hero_title: "L'Essence du", hero_gold: "Prestige", hero_desc: "Une collection rare de fragrances d'exception.",
                hero_btn: "Découvrir", col_title: "La Collection", cart_title: "Votre Panier",
                checkout: "Commander via WhatsApp", delivery_info: "Infos de livraison",
                placeholder_name: "Votre Nom Complet", placeholder_city: "Votre Ville", total: "Total",
                add: "Ajouter au panier", empty: "Votre panier est vide !", fill: "Veuillez remplir vos informations."
            },
            ar: {
                nav_collection: "المجموعة", nav_history: "قصتنا", nav_contact: "اتصل بنا",
                hero_title: "جوهر", hero_gold: "الفخامة", hero_desc: "مجموعة نادرة من العطور الاستثنائية المصممة للنخبة.",
                hero_btn: "اكتشف الآن", col_title: "المجموعة الحصرية", cart_title: "سلة التسوق",
                checkout: "طلب عبر الواتساب", delivery_info: "معلومات التوصيل",
                placeholder_name: "الاسم الكامل", placeholder_city: "المدينة", total: "المجموع",
                add: "أضف للسلة", empty: "السلة فارغة!", fill: "يرجى ملء البيانات."
            },
            en: {
                nav_collection: "Collection", nav_history: "History", nav_contact: "Contact",
                hero_title: "The Essence of", hero_gold: "Prestige", hero_desc: "A rare collection of exceptional fragrances.",
                hero_btn: "Explore", col_title: "The Collection", cart_title: "Your Cart",
                checkout: "Order via WhatsApp", delivery_info: "Delivery info",
                placeholder_name: "Full Name", placeholder_city: "City", total: "Total",
                add: "Add to Cart", empty: "Your cart is empty!", fill: "Please fill your info."
            }
        };

        const products = [
            { id: 1, name: "Oud Noir Impérial", price: 1200, img: "https://images.unsplash.com/photo-1594035910387-fea47794261f?w=600" },
            { id: 2, name: "Rose de Nuit", price: 950, img: "https://images.unsplash.com/photo-1543466835-00a7907e9de1?w=600" },
            { id: 3, name: "Ambre Royal Luxe", price: 1100, img: "https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?w=600" },
            { id: 4, name: "Musc Blanc Pure", price: 850, img: "https://images.unsplash.com/photo-1523293182086-7651a899d37f?w=600" },
            { id: 5, name: "Cèdre Argenté", price: 1300, img: "https://images.unsplash.com/photo-1594035910387-fea47794261f?w=600" },
            { id: 6, name: "Vanille Précieuse", price: 1050, img: "https://images.unsplash.com/photo-1592945403244-b3fbafd7f539?w=600" }
        ];

        let cart = [];
        let currentLang = 'fr';

        // 2. Fonctions Cœur
        function init() {
            renderProducts();
            createParticles();
            changeLang('fr');
        }

        function renderProducts() {
            const grid = document.getElementById('grid');
            grid.innerHTML = products.map(p => `
                <div class="product-card p-6 flex flex-col items-center">
                    <div class="overflow-hidden w-full h-72 mb-6">
                        <img src="${p.img}" alt="${p.name}" class="w-full h-full object-cover hover:scale-110 transition-transform duration-700">
                    </div>
                    <h3 class="font-display text-2xl mb-2 tracking-wide">${p.name}</h3>
                    <p class="text-[var(--gold)] font-bold mb-6">${p.price} DH</p>
                    <button onclick="addToCart(${p.id})" class="btn-secondary w-full py-3 text-[10px] uppercase tracking-[0.2em] font-bold" data-i18n="add">
                        Ajouter au panier
                    </button>
                </div>
            `).join('');
        }

        function addToCart(id) {
            const product = products.find(p => p.id === id);
            cart.push(product);
            updateCartUI();
            
            // Notification visuelle sur l'icône
            const cartIcon = document.getElementById('cartToggle');
            cartIcon.classList.add('scale-125', 'text-[var(--gold)]');
            setTimeout(() => cartIcon.classList.remove('scale-125', 'text-[var(--gold)]'), 300);
        }

        function updateCartUI() {
            document.getElementById('cartCount').innerText = cart.length;
            const items = document.getElementById('cartItems');
            
            items.innerHTML = cart.map((item, index) => `
                <div class="flex justify-between items-center bg-white/5 p-4 border border-white/5">
                    <div>
                        <p class="text-sm font-medium">${item.name}</p>
                        <p class="text-[var(--gold)] text-xs font-bold">${item.price} DH</p>
                    </div>
                    <button onclick="removeFromCart(${index})" class="text-gray-500 hover:text-red-500 text-xs">✕</button>
                </div>
            `).join('');

            const total = cart.reduce((sum, item) => sum + item.price, 0);
            document.getElementById('totalPrice').innerText = `${total} DH`;
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCartUI();
        }

        function changeLang(lang) {
            currentLang = lang;
            document.documentElement.lang = lang;
            document.documentElement.dir = lang === 'ar' ? 'rtl' : 'ltr';
            
            // Textes
            document.querySelectorAll('[data-i18n]').forEach(el => {
                el.innerText = translations[lang][el.dataset.i18n];
            });

            // Placeholders
            document.querySelectorAll('[data-i18n-placeholder]').forEach(el => {
                el.placeholder = translations[lang][el.getAttribute('data-i18n-placeholder')];
            });

            // Boutons de langue
            document.querySelectorAll('.lang-btn').forEach(b => {
                b.classList.toggle('active', b.dataset.lang === lang);
            });
        }

        function sendWhatsApp(event) {
            const btn = document.getElementById('waBtn');
            const name = document.getElementById('custName').value.trim();
            const city = document.getElementById('custCity').value.trim();

            if (cart.length === 0) { alert(translations[currentLang].empty); return; }
            if (!name || !city) { alert(translations[currentLang].fill); return; }

            // Effet Loading
            const originalText = btn.innerHTML;
            btn.classList.add('loading');
            btn.innerHTML = `... <span class="spinner"></span>`;

            setTimeout(() => {
                const phone = "212600000000"; // VOTRE NUMÉRO ICI
                let msg = `✨ *COMMANDE PRESTIGE - NICHE RICHE* ✨\n\n`;
                msg += `👤 *CLIENT :* ${name.toUpperCase()}\n`;
                msg += `📍 *VILLE :* ${city.toUpperCase()}\n`;
                msg += `━━━━━━━━━━━━━━━━━━━━\n\n`;
                
                cart.forEach((item, i) => {
                    msg += `▪️ ${item.name} - ${item.price} DH\n`;
                });

                const total = cart.reduce((s, i) => s + i.price, 0);
                msg += `\n━━━━━━━━━━━━━━━━━━━━\n`;
                msg += `💰 *TOTAL : ${total} DH*\n`;
                msg += `━━━━━━━━━━━━━━━━━━━━\n\n`;
                msg += `_Commande générée depuis le site web._`;

                window.open(`https://wa.me/${phone}?text=${encodeURIComponent(msg)}`, '_blank');
                
                btn.classList.remove('loading');
                btn.innerHTML = originalText;
            }, 800);
        }

        function createParticles() {
            const container = document.getElementById('particles');
            for(let i=0; i<40; i++) {
                const p = document.createElement('div');
                p.className = 'particle';
                const size = Math.random() * 3;
                p.style.width = size + 'px';
                p.style.height = size + 'px';
                p.style.left = Math.random() * 100 + '%';
                p.style.top = Math.random() * 100 + '%';
                p.style.animation = `float ${5 + Math.random() * 10}s infinite linear`;
                container.appendChild(p);
            }
        }

        // Event Listeners
        document.getElementById('cartToggle').onclick = () => document.getElementById('cartModal').classList.remove('hidden');
        document.getElementById('cartClose').onclick = () => document.getElementById('cartModal').classList.add('hidden');

        window.onload = init;
    </script>
</body>
</html>
