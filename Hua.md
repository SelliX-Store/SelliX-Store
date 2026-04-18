<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SelliX - Shop Now Enjoy Later</title>
<script src="https://cdn.tailwindcss.com"></script>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800;900&display=swap" rel="stylesheet">
<style>
*{font-family:'Inter',sans-serif}
.gradient-text{background:linear-gradient(135deg,#06b6d4,#ec4899);-webkit-background-clip:text;-webkit-text-fill-color:transparent}
.cyan-accent{color:#06b6d4}
.pink-accent{color:#ec4899}
.hero-text-shadow{text-shadow:4px 4px 0 rgba(236,72,153,.3)}
.floating{animation:floating 3s ease-in-out infinite}
@keyframes floating{0%,100%{transform:translateY(0)}50%{transform:translateY(-20px)}}
.slide-up{animation:slideUp .8s ease-out}
@keyframes slideUp{from{opacity:0;transform:translateY(30px)}to{opacity:1;transform:translateY(0)}}
.product-card{transition:all .3s ease}
.product-card:hover{transform:translateY(-10px);box-shadow:0 20px 40px rgba(0,0,0,.1)}
.btn-primary{background:linear-gradient(135deg,#06b6d4,#0891b2);transition:all .3s}
.btn-primary:hover{transform:scale(1.05);box-shadow:0 10px 30px rgba(6,182,212,.4)}
.btn-secondary{background:linear-gradient(135deg,#ec4899,#db2777);transition:all .3s}
.btn-secondary:hover{transform:scale(1.05);box-shadow:0 10px 30px rgba(236,72,153,.4)}
.cart-sidebar{transform:translateX(100%);transition:transform .3s}
.cart-sidebar.open{transform:translateX(0)}
.cart-overlay,.modal-overlay{opacity:0;pointer-events:none;transition:opacity .3s}
.cart-overlay.open,.modal-overlay.open{opacity:1;pointer-events:auto}
.modal-content{transform:scale(.9);transition:transform .3s}
.modal-overlay.open .modal-content{transform:scale(1)}
.category-btn.active{background:#000;color:#fff}
.marquee-container{overflow:hidden;white-space:nowrap}
.marquee-content{display:inline-block;animation:marquee 20s linear infinite}
@keyframes marquee{0%{transform:translateX(0)}100%{transform:translateX(-50%)}}
.quantity-btn{width:28px;height:28px;display:flex;align-items:center;justify-content:center;border-radius:50%;background:#f3f4f6;cursor:pointer;transition:all .2s}
.quantity-btn:hover{background:#06b6d4;color:#fff}
.remove-btn{color:#ef4444;cursor:pointer;transition:all .2s}
.remove-btn:hover{transform:scale(1.1)}
.whatsapp-btn{position:fixed;bottom:30px;right:30px;background:#25D366;color:#fff;padding:16px 24px;border-radius:50px;font-weight:bold;box-shadow:0 10px 30px rgba(37,211,102,.4);z-index:40;transition:all .3s;display:flex;align-items:center;gap:8px}
.whatsapp-btn:hover{transform:scale(1.1);box-shadow:0 15px 40px rgba(37,211,102,.5)}
.admin-badge{background:linear-gradient(135deg,#fbbf24,#f59e0b);color:#000;padding:4px 12px;border-radius:20px;font-size:.75rem;font-weight:800;text-transform:uppercase;letter-spacing:.05em}
.user-menu{position:relative}
.user-dropdown{position:absolute;top:100%;right:0;margin-top:8px;background:#fff;border-radius:16px;box-shadow:0 20px 40px rgba(0,0,0,.15);padding:8px;min-width:200px;opacity:0;pointer-events:none;transform:translateY(-10px);transition:all .2s}
.user-menu:hover .user-dropdown{opacity:1;pointer-events:auto;transform:translateY(0)}
.search-highlight{background:rgba(6,182,212,.2);padding:0 2px;border-radius:2px}
.shake{animation:shake .5s ease-in-out}
@keyframes shake{0%,100%{transform:translateX(0)}25%{transform:translateX(-10px)}75%{transform:translateX(10px)}}
.fade-in{animation:fadeIn .3s ease-in}
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
</style>
</head>
<body class="bg-gray-50 overflow-x-hidden">

<div id="cartOverlay" class="cart-overlay fixed inset-0 bg-black/50 z-50" onclick="toggleCart()"></div>

<div id="cartSidebar" class="cart-sidebar fixed top-0 right-0 w-full max-w-md h-full bg-white z-50 shadow-2xl flex flex-col">
<div class="p-6 border-b border-gray-200 flex justify-between items-center bg-black text-white">
<h2 class="text-2xl font-black flex items-center gap-2">
<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"/></svg>
Your Cart
</h2>
<button onclick="toggleCart()" class="p-2 hover:bg-gray-800 rounded-full"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg></button>
</div>
<div id="cartItems" class="flex-1 overflow-y-auto p-6"></div>
<div class="p-6 border-t border-gray-200 bg-gray-50">
<div class="flex justify-between items-center mb-4">
<span class="text-lg font-semibold text-gray-600">Subtotal</span>
<span id="cartTotal" class="text-2xl font-black text-gray-900">$0.00</span>
</div>
<button onclick="checkout()" class="w-full btn-secondary py-4 rounded-full text-white font-bold text-lg">Checkout via WhatsApp</button>
</div>
</div>

<div id="loginModal" class="modal-overlay fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4">
<div class="modal-content bg-white rounded-3xl p-8 max-w-md w-full">
<div class="flex justify-between items-center mb-6">
<h3 class="text-2xl font-black">Welcome Back</h3>
<button onclick="hideModal('loginModal')" class="p-2 hover:bg-gray-100 rounded-full"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg></button>
</div>
<form id="loginForm" class="space-y-4">
<div><label class="block text-sm font-bold mb-2">Username</label><input type="text" name="username" required class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<div><label class="block text-sm font-bold mb-2">Password</label><input type="password" name="password" required class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<button type="submit" class="w-full btn-primary py-3 rounded-full text-white font-bold">Login</button>
<p class="text-center text-sm text-gray-500">Don't have an account? <button type="button" onclick="showSignup()" class="text-cyan-500 font-bold hover:underline">Sign up</button></p>
</form>
</div>
</div>

<div id="signupModal" class="modal-overlay fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4 hidden">
<div class="modal-content bg-white rounded-3xl p-8 max-w-md w-full">
<div class="flex justify-between items-center mb-6">
<h3 class="text-2xl font-black">Create Account</h3>
<button onclick="hideModal('signupModal')" class="p-2 hover:bg-gray-100 rounded-full"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg></button>
</div>
<form id="signupForm" class="space-y-4">
<div><label class="block text-sm font-bold mb-2">Username</label><input type="text" name="username" required class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<div><label class="block text-sm font-bold mb-2">Email</label><input type="email" name="email" required class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<div><label class="block text-sm font-bold mb-2">Password</label><input type="password" name="password" required minlength="4" class="w-full px-4 py-3 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<button type="submit" class="w-full btn-secondary py-3 rounded-full text-white font-bold">Create Account</button>
<p class="text-center text-sm text-gray-500">Already have an account? <button type="button" onclick="showLogin()" class="text-cyan-500 font-bold hover:underline">Login</button></p>
</form>
</div>
</div>

<div id="addProductModal" class="modal-overlay fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4 hidden">
<div class="modal-content bg-white rounded-3xl p-8 max-w-md w-full max-h-[90vh] overflow-y-auto">
<div class="flex justify-between items-center mb-6">
<h3 class="text-2xl font-black">Add Product</h3>
<button onclick="hideModal('addProductModal')" class="p-2 hover:bg-gray-100 rounded-full"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg></button>
</div>
<form id="addProductForm" class="space-y-4">
<div><label class="block text-sm font-bold mb-2">Product Name</label><input type="text" name="name" required class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<div><label class="block text-sm font-bold mb-2">Price ($)</label><input type="number" name="price" step="0.01" required class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<div><label class="block text-sm font-bold mb-2">Category</label><select name="category" class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"><option value="new">New Arrivals</option><option value="bestseller">Best Sellers</option><option value="electronics">Electronics</option><option value="fashion">Fashion</option><option value="home">Home</option></select></div>
<div><label class="block text-sm font-bold mb-2">Image URL</label><input type="url" name="image" placeholder="https://..." class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<div><label class="block text-sm font-bold mb-2">Badge (optional)</label><select name="badge" class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"><option value="">None</option><option value="NEW">New</option><option value="HOT">Hot</option><option value="SALE">Sale</option></select></div>
<button type="submit" class="w-full btn-primary py-3 rounded-full text-white font-bold mt-4">Add Product</button>
</form>
</div>
</div>

<div id="editProductModal" class="modal-overlay fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4 hidden">
<div class="modal-content bg-white rounded-3xl p-8 max-w-md w-full max-h-[90vh] overflow-y-auto">
<div class="flex justify-between items-center mb-6">
<h3 class="text-2xl font-black">Edit Product</h3>
<button onclick="hideModal('editProductModal')" class="p-2 hover:bg-gray-100 rounded-full"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg></button>
</div>
<form id="editProductForm" class="space-y-4">
<input type="hidden" name="productId">
<div><label class="block text-sm font-bold mb-2">Product Name</label><input type="text" name="name" required class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<div><label class="block text-sm font-bold mb-2">Price ($)</label><input type="number" name="price" step="0.01" required class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<div><label class="block text-sm font-bold mb-2">Category</label><select name="category" class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"><option value="new">New Arrivals</option><option value="bestseller">Best Sellers</option><option value="electronics">Electronics</option><option value="fashion">Fashion</option><option value="home">Home</option></select></div>
<div><label class="block text-sm font-bold mb-2">Image URL</label><input type="url" name="image" class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"></div>
<div><label class="block text-sm font-bold mb-2">Badge (optional)</label><select name="badge" class="w-full px-4 py-2 rounded-xl border border-gray-200 focus:outline-none focus:border-cyan-400"><option value="">None</option><option value="NEW">New</option><option value="HOT">Hot</option><option value="SALE">Sale</option></select></div>
<div class="flex gap-3">
<button type="submit" class="flex-1 btn-primary py-3 rounded-full text-white font-bold">Save Changes</button>
<button type="button" onclick="deleteCurrentProduct()" class="flex-1 bg-red-500 hover:bg-red-600 text-white py-3 rounded-full font-bold transition-colors">Delete</button>
</div>
</form>
</div>
</div>

<nav class="fixed top-0 w-full bg-white/90 backdrop-blur-md z-40 border-b border-gray-100">
<div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
<div class="flex justify-between items-center h-20">
<div class="flex items-center cursor-pointer" onclick="window.scrollTo(0,0)">
<div class="bg-black p-3 rounded-xl border-l-4 border-cyan-400 border-r-4 border-pink-500 mr-3">
<svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"/></svg>
</div>
<span class="text-3xl font-black tracking-tighter"><span class="text-black">Sell</span><span class="cyan-accent">i</span><span class="pink-accent">X</span></span>
</div>
<div class="hidden md:flex items-center space-x-8">
<a href="#shop" class="text-gray-700 hover:text-cyan-500 font-semibold transition-colors">Shop</a>
<a href="#new" class="text-gray-700 hover:text-cyan-500 font-semibold transition-colors">New Arrivals</a>
<a href="#bestsellers" class="text-gray-700 hover:text-cyan-500 font-semibold transition-colors">Best Sellers</a>
<a href="#contact" class="text-gray-700 hover:text-cyan-500 font-semibold transition-colors">Contact</a>
</div>
<div class="flex items-center space-x-4">
<div class="relative hidden sm:block">
<input type="text" id="searchInput" placeholder="Search products..." class="pl-10 pr-4 py-2 rounded-full border border-gray-200 focus:outline-none focus:border-cyan-400 w-64 transition-all" oninput="handleSearch(this.value)">
<svg class="w-5 h-5 text-gray-400 absolute left-3 top-2.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/></svg>
</div>
<button onclick="toggleCart()" class="p-2 hover:bg-gray-100 rounded-full transition-colors relative">
<svg class="w-6 h-6 text-gray-700" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"/></svg>
<span id="cartBadge" class="absolute -top-1 -right-1 bg-pink-500 text-white text-xs w-5 h-5 rounded-full flex items-center justify-center font-bold hidden">0</span>
</button>
<div id="authButtons">
<button onclick="showLogin()" class="px-6 py-2 rounded-full border-2 border-black font-bold hover:bg-black hover:text-white transition-all">Login</button>
</div>
<div id="userMenu" class="user-menu hidden">
<button class="flex items-center gap-2 p-2 hover:bg-gray-100 rounded-full transition-colors">
<div class="w-8 h-8 bg-gradient-to-br from-cyan-400 to-pink-500 rounded-full flex items-center justify-center text-white font-bold text-sm" id="userAvatar">A</div>
<span class="font-bold text-sm hidden lg:block" id="userName">Admin</span>
<svg class="w-4 h-4 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/></svg>
</button>
<div class="user-dropdown">
<div class="px-4 py-3 border-b border-gray-100">
<p class="font-bold text-gray-900" id="dropdownUserName">Admin</p>
<p class="text-xs text-gray-500" id="dropdownUserEmail">admin@sellix.com</p>
</div>
<div id="adminMenuItem" class="hidden">
<button onclick="showAddProductModal()" class="w-full text-left px-4 py-3 hover:bg-gray-50 rounded-xl flex items-center gap-2 text-cyan-600 font-bold">
<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg>
Add Product
</button>
</div>
<button onclick="logout()" class="w-full text-left px-4 py-3 hover:bg-gray-50 rounded-xl flex items-center gap-2 text-red-500 font-bold">
<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"/></svg>
Logout
</button>
</div>
</div>
</div>
</div>
</div>
</nav>

<section class="pt-32 pb-20 px-4 relative overflow-hidden bg-gray-100">
<div class="max-w-7xl mx-auto relative z-10">
<div class="grid md:grid-cols-2 gap-12 items-center">
<div class="slide-up">
<div class="mb-6">
<h1 class="text-7xl md:text-9xl font-black leading-none tracking-tighter">
<span class="block text-black hero-text-shadow">Shop</span>
<span class="block relative">
<span class="text-pink-500 hero-text-shadow">Enjoy</span>
<span class="absolute -right-4 top-0 text-2xl md:text-4xl font-bold cyan-accent rotate-12">Now</span>
</span>
<span class="block text-black hero-text-shadow relative">
Later
<span class="absolute -right-8 bottom-0 text-xl md:text-3xl font-bold text-pink-500 -rotate-6">Later</span>
</span>
</h1>
</div>
<p class="text-xl text-gray-600 mb-8 max-w-md font-medium">Discover curated products that bring joy to your everyday life.</p>
<a href="#shop" class="btn-primary px-8 py-4 rounded-full text-white font-bold text-lg flex items-center gap-2 inline-flex">
Shop Now
<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
</a>
</div>
<div class="relative floating">
<div class="relative bg-white rounded-3xl p-8 shadow-2xl">
<div class="absolute -top-6 -right-6 bg-cyan-400 text-white px-4 py-2 rounded-full font-bold shadow-lg transform rotate-12">New!</div>
<img src="https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=600&h=600&fit=crop" alt="Featured" class="w-full h-96 object-cover rounded-2xl mb-4">
<div class="flex justify-between items-center">
<div>
<h3 class="text-2xl font-bold text-gray-900">Featured Collection</h3>
<p class="text-gray-500">Starting from $29.99</p>
</div>
<button class="bg-black text-white p-4 rounded-full hover:scale-110 transition-transform"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg></button>
</div>
</div>
</div>
</div>
</div>
</section>

<section class="bg-black py-6 overflow-hidden">
<div class="marquee-container">
<div class="marquee-content">
<span class="text-xl font-bold text-white mx-8 flex items-center gap-2 inline-flex"><span class="text-cyan-400">✦</span> FREE SHIPPING OVER $50</span>
<span class="text-xl font-bold text-white mx-8 flex items-center gap-2 inline-flex"><span class="text-pink-500">✦</span> 24/7 CUSTOMER SUPPORT</span>
<span class="text-xl font-bold text-white mx-8 flex items-center gap-2 inline-flex"><span class="text-cyan-400">✦</span> 30-DAY RETURNS</span>
<span class="text-xl font-bold text-white mx-8 flex items-center gap-2 inline-flex"><span class="text-pink-500">✦</span> SECURE PAYMENT</span>
<span class="text-xl font-bold text-white mx-8 flex items-center gap-2 inline-flex"><span class="text-cyan-400">✦</span> FREE SHIPPING OVER $50</span>
<span class="text-xl font-bold text-white mx-8 flex items-center gap-2 inline-flex"><span class="text-pink-500">✦</span> 24/7 CUSTOMER SUPPORT</span>
<span class="text-xl font-bold text-white mx-8 flex items-center gap-2 inline-flex"><span class="text-cyan-400">✦</span> 30-DAY RETURNS</span>
<span class="text-xl font-bold text-white mx-8 flex items-center gap-2 inline-flex"><span class="text-pink-500">✦</span> SECURE PAYMENT</span>
</div>
</div>
</section>

<section id="shop" class="py-20 px-4 bg-white">
<div class="max-w-7xl mx-auto">
<div class="text-center mb-12">
<h2 class="text-5xl md:text-6xl font-black mb-4"><span class="text-black">Our</span><span class="gradient-text">Collection</span></h2>
<p class="text-gray-600 text-lg" id="resultsCount">Browse our products</p>
</div>
<div class="sm:hidden mb-6">
<div class="relative">
<input type="text" id="mobileSearchInput" placeholder="Search products..." class="w-full pl-10 pr-4 py-3 rounded-full border border-gray-200 focus:outline-none focus:border-cyan-400" oninput="handleSearch(this.value)">
<svg class="w-5 h-5 text-gray-400 absolute left-3 top-3.5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/></svg>
</div>
</div>
<div class="flex flex-wrap justify-center gap-3 mb-12" id="categoryFilters">
<button onclick="filterCategory('all')" class="category-btn active px-6 py-2 rounded-full border-2 border-black font-bold transition-all hover:bg-black hover:text-white">All</button>
<button onclick="filterCategory('new')" class="category-btn px-6 py-2 rounded-full border-2 border-black font-bold transition-all hover:bg-black hover:text-white">New Arrivals</button>
<button onclick="filterCategory('bestseller')" class="category-btn px-6 py-2 rounded-full border-2 border-black font-bold transition-all hover:bg-black hover:text-white">Best Sellers</button>
<button onclick="filterCategory('electronics')" class="category-btn px-6 py-2 rounded-full border-2 border-black font-bold transition-all hover:bg-black hover:text-white">Electronics</button>
<button onclick="filterCategory('fashion')" class="category-btn px-6 py-2 rounded-full border-2 border-black font-bold transition-all hover:bg-black hover:text-white">Fashion</button>
<button onclick="filterCategory('home')" class="category-btn px-6 py-2 rounded-full border-2 border-black font-bold transition-all hover:bg-black hover:text-white">Home</button>
</div>
<div id="adminNotice" class="hidden mb-8 p-4 bg-gradient-to-r from-yellow-50 to-orange-50 border border-yellow-200 rounded-2xl flex items-center gap-3">
<span class="admin-badge">Admin Mode</span>
<p class="text-sm text-gray-700">You can add, edit, and delete products.</p>
</div>
<div id="productsGrid" class="grid md:grid-cols-2 lg:grid-cols-4 gap-8"></div>
<div id="noResults" class="hidden text-center py-12">
<svg class="w-16 h-16 mx-auto text-gray-300 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/></svg>
<p class="text-gray-500 text-lg">No products found matching your search.</p>
<button onclick="clearSearch()" class="mt-4 text-cyan-500 font-bold hover:underline">Clear search</button>
</div>
<div id="addProductSection" class="hidden mt-16 text-center p-8 border-2 border-dashed border-gray-300 rounded-3xl">
<p class="text-gray-500 mb-4">Admin Control Panel</p>
<button onclick="showAddProductModal()" class="btn-primary px-8 py-3 rounded-full text-white font-bold">+ Add New Product</button>
</div>
</div>
</section>

<section id="contact" class="py-20 px-4 bg-gray-100">
<div class="max-w-4xl mx-auto text-center">
<h2 class="text-5xl font-black mb-6"><span class="text-black">Get in</span><span class="gradient-text">Touch</span></h2>
<p class="text-gray-600 text-lg mb-8">Have questions? Reach out to us on WhatsApp!</p>
<a href="https://wa.me/70549124" target="_blank" class="inline-flex items-center gap-3 bg-[#25D366] text-white px-8 py-4 rounded-full font-bold text-lg hover:scale-105 transition-transform shadow-lg">
<svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
Chat on WhatsApp: 70 549 124
</a>
</div>
</section>

<footer class="bg-black text-white pt-16 pb-8 px-4">
<div class="max-w-7xl mx-auto">
<div class="grid md:grid-cols-4 gap-8 mb-12">
<div>
<div class="flex items-center mb-4">
<div class="bg-white p-2 rounded-lg border-l-2 border-cyan-400 border-r-2 border-pink-500 mr-2">
<svg class="w-6 h-6 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"/></svg>
</div>
<span class="text-2xl font-black">SelliX</span>
</div>
<p class="text-gray-400 text-sm">Your destination for curated lifestyle products.</p>
</div>
<div>
<h4 class="font-bold mb-4">Quick Links</h4>
<ul class="space-y-2 text-sm text-gray-400">
<li><a href="#shop" class="hover:text-cyan-400 transition-colors">Shop</a></li>
<li><a href="#new" class="hover:text-cyan-400 transition-colors">New Arrivals</a></li>
<li><a href="#bestsellers" class="hover:text-cyan-400 transition-colors">Best Sellers</a></li>
</ul>
</div>
<div>
<h4 class="font-bold mb-4">Support</h4>
<ul class="space-y-2 text-sm text-gray-400">
<li><a href="#contact" class="hover:text-cyan-400 transition-colors">Contact Us</a></li>
<li><a href="#" class="hover:text-cyan-400 transition-colors">FAQ</a></li>
<li><a href="#" class="hover:text-cyan-400 transition-colors">Shipping</a></li>
</ul>
</div>
<div>
<h4 class="font-bold mb-4">Follow Us</h4>
<div class="flex gap-4">
<a href="#" class="w-10 h-10 bg-gray-800 rounded-full flex items-center justify-center hover:bg-cyan-400 transition-colors"><svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"/></svg></a>
<a href="#" class="w-10 h-10 bg-gray-800 rounded-full flex items-center justify-center hover:bg-pink-500 transition-colors"><svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg></a>
</div>
</div>
</div>
<div class="border-t border-gray-800 pt-8 text-center">
<p class="text-gray-500 text-sm">&copy; 2024 SelliX. All rights reserved.</p>
</div>
</div>
</footer>

<a href="https://wa.me/70549124" target="_blank" class="whatsapp-btn">
<svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/></svg>
Contact Us
</a>

<script>
let products=JSON.parse(localStorage.getItem('sellix_products'))||[];
let users=JSON.parse(localStorage.getItem('sellix_users'))||[];
let currentUser=JSON.parse(localStorage.getItem('sellix_currentUser'))||null;
let cart=JSON.parse(localStorage.getItem('sellix_cart'))||[];
let currentCategory='all';
let searchQuery='';
let editingProductId=null;

function ensureAdmin(){
    if(!users.find(u=>u.username==='admin')){
        users.push({username:'admin',email:'admin@sellix.com',password:'1243',isAdmin:true});
        localStorage.setItem('sellix_users',JSON.stringify(users));
    }
}

document.addEventListener('DOMContentLoaded',function(){
    ensureAdmin();
    if(currentUser) updateUI();
    renderProducts();
    updateCart();
    
    document.getElementById('loginForm').addEventListener('submit',handleLogin);
    document.getElementById('signupForm').addEventListener('submit',handleSignup);
    document.getElementById('addProductForm').addEventListener('submit',handleAddProduct);
    document.getElementById('editProductForm').addEventListener('submit',handleEditProduct);
    
    document.querySelectorAll('.modal-overlay').forEach(function(m){
        m.addEventListener('click',function(e){
            if(e.target===e.currentTarget) hideModal(e.currentTarget.id);
        });
    });
});

function updateUI(){
    document.getElementById('authButtons').classList.add('hidden');
    document.getElementById('userMenu').classList.remove('hidden');
    document.getElementById('userName').textContent=currentUser.username;
    document.getElementById('dropdownUserName').textContent=currentUser.username;
    document.getElementById('dropdownUserEmail').textContent=currentUser.email;
    document.getElementById('userAvatar').textContent=currentUser.username.charAt(0).toUpperCase();
    
    if(currentUser.isAdmin || (currentUser.username==='admin' && currentUser.password==='1243')){
        document.getElementById('adminMenuItem').classList.remove('hidden');
        document.getElementById('addProductSection').classList.remove('hidden');
        document.getElementById('adminNotice').classList.remove('hidden');
        currentUser.isAdmin=true;
        localStorage.setItem('sellix_currentUser',JSON.stringify(currentUser));
    }
}

function showLogin(){
    hideModal('signupModal');
    document.getElementById('loginModal').classList.remove('hidden');
    setTimeout(function(){document.getElementById('loginModal').classList.add('open');},10);
}

function showSignup(){
    hideModal('loginModal');
    document.getElementById('signupModal').classList.remove('hidden');
    setTimeout(function(){document.getElementById('signupModal').classList.add('open');},10);
}

function hideModal(id){
    var m=document.getElementById(id);
    m.classList.remove('open');
    setTimeout(function(){m.classList.add('hidden');},300);
}

function handleLogin(e){
    e.preventDefault();
    var f=e.target,u=f.username.value.trim(),p=f.password.value,x=users.find(function(y){return y.username===u && y.password===p;});
    if(!x){
        f.classList.add('shake');
        setTimeout(function(){f.classList.remove('shake');},500);
        alert('Invalid credentials');
        return;
    }
    currentUser=x;
    localStorage.setItem('sellix_currentUser',JSON.stringify(currentUser));
    hideModal('loginModal');
    updateUI();
    f.reset();
}

function handleSignup(e){
    e.preventDefault();
    var f=e.target,u=f.username.value.trim(),m=f.email.value.trim(),p=f.password.value;
    if(users.find(function(y){return y.username===u;})){
        alert('Username exists');
        return;
    }
    var n={username:u,email:m,password:p,isAdmin:false};
    users.push(n);
    localStorage.setItem('sellix_users',JSON.stringify(users));
    currentUser=n;
    localStorage.setItem('sellix_currentUser',JSON.stringify(n));
    hideModal('signupModal');
    updateUI();
    f.reset();
    alert('Account created!');
}

function logout(){
    currentUser=null;
    localStorage.removeItem('sellix_currentUser');
    cart=[];
    localStorage.removeItem('sellix_cart');
    location.reload();
}

function renderProducts(){
    var g=document.getElementById('productsGrid'),n=document.getElementById('noResults'),r=document.getElementById('resultsCount');
    g.innerHTML='';
    var f=products.filter(function(p){
        return (currentCategory==='all' || p.category===currentCategory) && (!searchQuery || p.name.toLowerCase().includes(searchQuery.toLowerCase()));
    });
    if(!f.length){
        g.classList.add('hidden');
        n.classList.remove('hidden');
        r.textContent=searchQuery?'No results for "'+searchQuery+'"':'No products yet';
        return;
    }
    g.classList.remove('hidden');
    n.classList.add('hidden');
    r.textContent=searchQuery?'Found '+f.length+' result'+(f.length!==1?'s':'')+' for "'+searchQuery+'"':f.length+' product'+(f.length!==1?'s':'');
    
    f.forEach(function(p){
        var a=currentUser && currentUser.isAdmin;
        var d=document.createElement('div');
        d.className='product-card bg-gray-50 rounded-3xl overflow-hidden group cursor-pointer relative';
        d.innerHTML='<div class="relative h-64 bg-white p-6 flex items-center justify-center"><img src="'+p.image+'" alt="'+p.name+'" class="w-full h-full object-contain group-hover:scale-110 transition-transform duration-500">'+(p.badge?'<div class="absolute top-4 right-4 '+(p.badge==='SALE'?'bg-pink-500':p.badge==='HOT'?'bg-red-500':'bg-cyan-400')+' text-white px-3 py-1 rounded-full text-sm font-bold">'+p.badge+'</div>':'')+(a?'<button class="edit-btn absolute top-4 left-4 w-10 h-10 bg-black/80 text-white rounded-full flex items-center justify-center hover:bg-cyan-400 transition-colors opacity-0 group-hover:opacity-100"><svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"/></svg></button>':'')+'</div><div class="p-6"><h3 class="text-xl font-bold text-gray-900 mb-2">'+(searchQuery?p.name.replace(new RegExp('('+searchQuery+')','gi'),'<span class="search-highlight">$1</span>'):p.name)+'</h3><div class="flex justify-between items-center"><span class="text-2xl font-black text-gray-900">$'+p.price.toFixed(2)+'</span><button class="add-cart-btn w-12 h-12 bg-black text-white rounded-full flex items-center justify-center hover:bg-cyan-400 transition-all hover:scale-110 active:scale-95"><svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg></button></div></div>';
        
        if(a){
            d.querySelector('.edit-btn').addEventListener('click',function(evt){
                evt.stopPropagation();
                editProduct(p.id);
            });
        }
        d.querySelector('.add-cart-btn').addEventListener('click',function(evt){
            evt.stopPropagation();
            addToCart(p.id,this);
        });
        g.appendChild(d);
    });
}

function showAddProductModal(){
    if(!currentUser || !currentUser.isAdmin){
        alert('Admin access required');
        return;
    }
    document.getElementById('addProductModal').classList.remove('hidden');
    setTimeout(function(){document.getElementById('addProductModal').classList.add('open');},10);
}

function handleAddProduct(e){
    e.preventDefault();
    if(!currentUser || !currentUser.isAdmin) return;
    var f=e.target,n={id:Date.now(),name:f.name.value,price:parseFloat(f.price.value),category:f.category.value,image:f.image.value||'https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=400&h=400&fit=crop',badge:f.badge.value};
    products.push(n);
    localStorage.setItem('sellix_products',JSON.stringify(products));
    renderProducts();
    hideModal('addProductModal');
    f.reset();
}

function editProduct(id){
    if(!currentUser || !currentUser.isAdmin) return;
    var p=products.find(function(x){return x.id===id;});
    if(!p) return;
    editingProductId=id;
    var f=document.getElementById('editProductForm');
    f.productId.value=id;
    f.name.value=p.name;
    f.price.value=p.price;
    f.category.value=p.category;
    f.image.value=p.image;
    f.badge.value=p.badge||'';
    document.getElementById('editProductModal').classList.remove('hidden');
    setTimeout(function(){document.getElementById('editProductModal').classList.add('open');},10);
}

function handleEditProduct(e){
    e.preventDefault();
    if(!currentUser || !currentUser.isAdmin) return;
    var f=e.target,id=parseInt(f.productId.value),p=products.find(function(x){return x.id===id;});
    if(p){
        p.name=f.name.value;
        p.price=parseFloat(f.price.value);
        p.category=f.category.value;
        p.image=f.image.value;
        p.badge=f.badge.value;
        localStorage.setItem('sellix_products',JSON.stringify(products));
        renderProducts();
        hideModal('editProductModal');
    }
}

function deleteCurrentProduct(){
    if(!currentUser || !currentUser.isAdmin) return;
    if(confirm('Delete this product?')){
        products=products.filter(function(x){return x.id!==editingProductId;});
        localStorage.setItem('sellix_products',JSON.stringify(products));
        renderProducts();
        hideModal('editProductModal');
    }
}

function toggleCart(){
    var s=document.getElementById('cartSidebar'),o=document.getElementById('cartOverlay');
    s.classList.toggle('open');
    o.classList.toggle('open');
    document.body.style.overflow=s.classList.contains('open')?'hidden':'';
}

function addToCart(id,btn){
    var p=products.find(function(x){return x.id===id;});
    if(!p) return;
    var e=cart.find(function(x){return x.id===id;});
    if(e) e.quantity++;
    else cart.push({id:p.id,name:p.name,price:p.price,image:p.image,quantity:1});
    localStorage.setItem('sellix_cart',JSON.stringify(cart));
    updateCart();
    var h=btn.innerHTML;
    btn.innerHTML='<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/></svg>';
    btn.classList.add('bg-green-500');
    setTimeout(function(){
        btn.innerHTML=h;
        btn.classList.remove('bg-green-500');
    },1000);
}

function removeFromCart(id){
    cart=cart.filter(function(x){return x.id!==id;});
    localStorage.setItem('sellix_cart',JSON.stringify(cart));
    updateCart();
}

function updateQuantity(id,c){
    var i=cart.find(function(x){return x.id===id;});
    if(!i) return;
    i.quantity+=c;
    if(i.quantity<=0) removeFromCart(id);
    else{
        localStorage.setItem('sellix_cart',JSON.stringify(cart));
        updateCart();
    }
}

function updateCart(){
    var ci=document.getElementById('cartItems'),ct=document.getElementById('cartTotal'),cb=document.getElementById('cartBadge');
    var t=cart.reduce(function(s,i){return s+i.quantity;},0),p=cart.reduce(function(s,i){return s+i.price*i.quantity;},0);
    if(t){
        cb.textContent=t;
        cb.classList.remove('hidden');
    }else{
        cb.classList.add('hidden');
    }
    ct.textContent='$'+p.toFixed(2);
    if(cart.length){
        ci.innerHTML=cart.map(function(i){
            return '<div class="flex gap-4 mb-6 pb-6 border-b border-gray-100 fade-in"><img src="'+i.image+'" alt="'+i.name+'" class="w-20 h-20 object-cover rounded-xl bg-gray-100"><div class="flex-1"><div class="flex justify-between items-start mb-2"><h4 class="font-bold text-gray-900">'+i.name+'</h4><button onclick="removeFromCart('+i.id+')" class="remove-btn"><svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/></svg></button></div><p class="text-cyan-600 font-bold mb-2">$'+i.price.toFixed(2)+'</p><div class="flex items-center gap-3"><button onclick="updateQuantity('+i.id+',-1)" class="quantity-btn">-</button><span class="font-bold w-8 text-center">'+i.quantity+'</span><button onclick="updateQuantity('+i.id+',1)" class="quantity-btn">+</button></div></div></div>';
        }).join('');
    }else{
        ci.innerHTML='<div class="flex flex-col items-center justify-center h-full text-gray-400"><svg class="w-16 h-16 mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"/></svg><p class="text-lg">Your cart is empty</p><button onclick="toggleCart()" class="mt-4 text-cyan-500 font-bold hover:underline">Start Shopping</button></div>';
    }
}

function checkout(){
    if(!cart.length){
        alert('Cart is empty');
        return;
    }
    var m='Hello! I would like to order:\n\n';
    cart.forEach(function(i){
        m+='- '+i.name+' (x'+i.quantity+') - $'+(i.price*i.quantity).toFixed(2)+'\n';
    });
    m+='\nTotal: $'+cart.reduce(function(s,i){return s+i.price*i.quantity;},0).toFixed(2);
    window.open('https://wa.me/70549124?text='+encodeURIComponent(m),'_blank');
}

function filterCategory(c){
    currentCategory=c;
    var btns=document.querySelectorAll('.category-btn');
    for(var i=0;i<btns.length;i++){
        btns[i].classList.remove('active');
    }
    event.target.classList.add('active');
    renderProducts();
}

function handleSearch(q){
    searchQuery=q;
    renderProducts();
}

function clearSearch(){
    searchQuery='';
    document.getElementById('searchInput').value='';
    document.getElementById('mobileSearchInput').value='';
    renderProducts();
}
</script>
</body>
</html>
