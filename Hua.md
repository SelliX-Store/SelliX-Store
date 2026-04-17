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
<span class="text-xl font-bold text-white mx-8 flex items-center gap-2 inline-flex"><span class="text-pink-500">✦</s
