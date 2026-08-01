# pricepulse-AI
PricePulse AI — Smart Shopping Assistant
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes" />
    <title>PricePulse AI - Smart Shopping</title>

    <style>
        /* ===== RESET & BASE ===== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
        }

        body {
            background: #ffffff;
            color: #202123;
            height: 100vh;
            overflow: hidden;
        }

        /* =========================
           SIDEBAR
        ========================= */

        .sidebar {
            position: fixed;
            left: 0;
            top: 0;
            width: 280px;
            height: 100vh;
            background: #f7f7f8;
            border-right: 1px solid #ddd;
            z-index: 1000;
            display: flex;
            flex-direction: column;
            transform: translateX(-100%);
            transition: 0.3s ease;
        }

        .sidebar.open {
            transform: translateX(0);
        }

        .sidebar-header {
            padding: 18px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #eee;
        }

        .logo {
            font-size: 22px;
            font-weight: 800;
            color: #1a1a2e;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .logo .brand-symbol {
            display: inline-block;
            width: 28px;
            height: 28px;
            border: 2.5px solid #1a1a2e;
            border-radius: 50%;
            position: relative;
            flex-shrink: 0;
        }

        .logo .brand-symbol::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 8px;
            height: 8px;
            background: #1a1a2e;
            border-radius: 50%;
        }

        .logo .brand-symbol .line {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 14px;
            height: 0;
            border-top: 2px solid #1a1a2e;
        }

        .logo .brand-symbol .line:nth-child(2) {
            transform: translate(-50%, -50%) rotate(90deg);
        }

        .logo span {
            color: #f5c842;
        }

        .close-menu {
            font-size: 25px;
            cursor: pointer;
            color: #888;
            background: none;
            border: none;
            padding: 4px 8px;
        }

        .close-menu:hover {
            color: #1a1a2e;
        }

        .new-chat-btn {
            margin: 14px 16px;
            padding: 14px 16px;
            border: 1px solid #ddd;
            border-radius: 10px;
            background: white;
            cursor: pointer;
            text-align: left;
            font-weight: 600;
            font-size: 15px;
            color: #1a1a2e;
            transition: 0.2s;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .new-chat-btn:hover {
            background: #ececec;
            border-color: #1a1a2e;
        }

        .sidebar-content {
            flex: 1;
            overflow-y: auto;
            padding: 8px 0 20px;
        }

        .section-title {
            font-size: 11px;
            color: #999;
            font-weight: 700;
            margin: 16px 16px 8px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .menu-item {
            padding: 10px 16px;
            border-radius: 8px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 12px;
            font-size: 14px;
            color: #1a1a2e;
            background: none;
            border: none;
            width: 100%;
            text-align: left;
            font-family: inherit;
            transition: 0.2s;
        }

        .menu-item:hover {
            background: #e5e5e5;
        }

        .menu-item .icon {
            font-size: 16px;
            font-weight: 600;
            width: 28px;
            text-align: center;
            color: #555;
        }

        .menu-item .badge {
            margin-left: auto;
            background: #1a1a2e;
            color: #f5c842;
            font-size: 11px;
            padding: 2px 10px;
            border-radius: 12px;
        }

        /* =========================
           MAIN
        ========================= */

        .main {
            height: 100vh;
            display: flex;
            flex-direction: column;
        }

        .topbar {
            height: 60px;
            border-bottom: 1px solid #eee;
            display: flex;
            align-items: center;
            padding: 0 18px;
            justify-content: space-between;
            background: #ffffff;
            flex-shrink: 0;
        }

        .left-top {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .hamburger {
            font-size: 25px;
            cursor: pointer;
            background: none;
            border: none;
            color: #1a1a2e;
            padding: 4px;
            line-height: 1;
        }

        .hamburger:hover {
            opacity: 0.7;
        }

        .top-logo {
            font-size: 20px;
            font-weight: 800;
            color: #1a1a2e;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .top-logo .brand-symbol {
            display: inline-block;
            width: 24px;
            height: 24px;
            border: 2px solid #1a1a2e;
            border-radius: 50%;
            position: relative;
            flex-shrink: 0;
        }

        .top-logo .brand-symbol::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 6px;
            height: 6px;
            background: #1a1a2e;
            border-radius: 50%;
        }

        .top-logo span {
            color: #f5c842;
        }

        .profile {
            width: 35px;
            height: 35px;
            background: #1a1a2e;
            color: white;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: 700;
            font-size: 14px;
            cursor: pointer;
        }

        /* =========================
           CHAT AREA
        ========================= */

        .chat-area {
            flex: 1;
            overflow-y: auto;
            padding: 20px 20px 140px;
            background: #ffffff;
        }

        .chat-container {
            max-width: 1100px;
            margin: auto;
        }

        /* WELCOME */
        .welcome {
            text-align: center;
            margin-top: 10vh;
        }

        .welcome .brand-display {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 20px;
        }

        .welcome .brand-display .big-symbol {
            display: inline-block;
            width: 72px;
            height: 72px;
            border: 3px solid #1a1a2e;
            border-radius: 50%;
            position: relative;
            margin-bottom: 12px;
        }

        .welcome .brand-display .big-symbol::after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 20px;
            height: 20px;
            background: #1a1a2e;
            border-radius: 50%;
        }

        .welcome .brand-display .big-symbol .line {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 36px;
            height: 0;
            border-top: 3px solid #1a1a2e;
        }

        .welcome .brand-display .big-symbol .line:nth-child(2) {
            transform: translate(-50%, -50%) rotate(90deg);
        }

        .welcome .brand-display .ai-label {
            font-size: 12px;
            font-weight: 700;
            color: #888;
            letter-spacing: 3px;
            text-transform: uppercase;
        }

        .welcome h1 {
            font-size: 28px;
            font-weight: 700;
            color: #1a1a2e;
            margin-bottom: 8px;
        }

        .welcome p {
            color: #888;
            font-size: 15px;
            margin-bottom: 30px;
        }

        /* ===== CATEGORY GRID ===== */
        .category-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
            max-width: 700px;
            margin: 0 auto;
        }

        .category-grid .cat-item {
            padding: 16px 10px;
            border: 1px solid #e0e4e8;
            border-radius: 12px;
            text-align: center;
            cursor: pointer;
            background: white;
            transition: 0.2s;
        }

        .category-grid .cat-item:hover {
            background: #f5f5f5;
            border-color: #1a1a2e;
            transform: translateY(-3px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.06);
        }

        .category-grid .cat-item .cat-icon {
            font-size: 28px;
            display: block;
            margin-bottom: 6px;
            font-weight: 400;
        }

        .category-grid .cat-item .cat-name {
            font-size: 12px;
            font-weight: 600;
            color: #1a1a2e;
        }

        /* QUICK OPTIONS */
        .quick-options {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 12px;
            max-width: 600px;
            margin: auto;
        }

        .quick {
            padding: 16px;
            border: 1px solid #e0e4e8;
            border-radius: 12px;
            text-align: left;
            cursor: pointer;
            background: white;
            transition: 0.2s;
        }

        .quick:hover {
            background: #f5f5f5;
            border-color: #1a1a2e;
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.06);
        }

        .quick .quick-icon {
            font-size: 18px;
            font-weight: 400;
            margin-right: 6px;
            color: #555;
        }

        .quick strong {
            display: block;
            font-size: 15px;
            margin: 4px 0 2px;
            color: #1a1a2e;
        }

        .quick small {
            font-size: 12px;
            color: #888;
        }

        /* MESSAGE */
        .message {
            display: flex;
            margin-bottom: 20px;
            gap: 12px;
            animation: fadeIn 0.4s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .message.user {
            justify-content: flex-end;
        }

        .avatar {
            width: 32px;
            height: 32px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-shrink: 0;
            font-weight: 700;
            font-size: 13px;
        }

        .ai-avatar {
            background: #1a1a2e;
            color: #f5c842;
            font-size: 12px;
            font-weight: 700;
        }

        .user-avatar {
            background: #555;
            color: white;
        }

        .message-content {
            max-width: 100%;
            padding: 12px 18px;
            line-height: 1.6;
            border-radius: 14px;
            font-size: 15px;
            color: #1a1a2e;
            width: 100%;
        }

        .message.user .message-content {
            background: #f0f0f0;
        }

        .message.ai .message-content {
            background: white;
            border: 1px solid #e8ecf1;
        }

        .message-content strong {
            color: #1a1a2e;
        }

        /* =========================
           PRODUCT CARDS - FIXED 4 PER ROW
        ========================= */

        .products {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 16px;
            margin-top: 14px;
            width: 100%;
        }

        .product-card {
            border: 1px solid #e8ecf1;
            border-radius: 12px;
            overflow: hidden;
            background: white;
            transition: 0.3s;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            height: 100%;
            min-height: 280px;
            max-height: 340px;
        }

        .product-card:hover {
            border-color: #1a1a2e;
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.08);
        }

        .product-image {
            height: 130px;
            background: #f8f9fa;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 44px;
            flex-shrink: 0;
            color: #555;
            font-weight: 400;
        }

        .product-info {
            padding: 10px 12px 12px;
            flex: 1;
            display: flex;
            flex-direction: column;
        }

        .product-info h3 {
            font-size: 14px;
            font-weight: 600;
            color: #1a1a2e;
            margin-bottom: 4px;
            line-height: 1.3;
            min-height: 36px;
            overflow: hidden;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
        }

        .product-info .product-desc {
            font-size: 12px;
            color: #888;
            margin-bottom: 6px;
            line-height: 1.3;
            flex: 1;
            min-height: 30px;
            overflow: hidden;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
        }

        .product-price {
            color: #1a1a2e;
            font-weight: 700;
            font-size: 16px;
            margin-bottom: 8px;
        }

        .product-price .currency {
            font-size: 12px;
            font-weight: 400;
            color: #888;
        }

        .product-button {
            width: 100%;
            padding: 8px;
            border: none;
            border-radius: 8px;
            background: #1a1a2e;
            color: white;
            cursor: pointer;
            font-weight: 600;
            font-size: 13px;
            transition: 0.3s;
            font-family: inherit;
            margin-top: auto;
        }

        .product-button:hover {
            background: #f5c842;
            color: #1a1a2e;
        }

        /* =========================
           INPUT AREA
        ========================= */

        .input-area {
            position: fixed;
            bottom: 0;
            left: 0;
            width: 100%;
            padding: 16px 20px 20px;
            background: linear-gradient(transparent, white 30%);
            z-index: 100;
        }

        .input-box {
            max-width: 1100px;
            margin: auto;
            border: 1px solid #e0e4e8;
            border-radius: 16px;
            background: white;
            display: flex;
            align-items: center;
            padding: 4px 6px 4px 18px;
            box-shadow: 0 2px 12px rgba(0,0,0,0.06);
            transition: 0.3s;
        }

        .input-box:focus-within {
            border-color: #1a1a2e;
            box-shadow: 0 4px 20px rgba(0,0,0,0.08);
        }

        .input-box textarea {
            flex: 1;
            resize: none;
            border: none;
            outline: none;
            padding: 10px 0;
            font-size: 15px;
            height: 44px;
            font-family: inherit;
            background: transparent;
            color: #1a1a2e;
        }

        .input-box textarea::placeholder {
            color: #bbb;
        }

        .input-actions {
            display: flex;
            gap: 4px;
            align-items: center;
        }

        .input-actions button {
            background: transparent;
            border: none;
            color: #888;
            font-size: 13px;
            cursor: pointer;
            padding: 6px 10px;
            border-radius: 8px;
            transition: 0.3s;
            font-family: inherit;
            font-weight: 500;
        }

        .input-actions button:hover {
            background: #f0f2f5;
            color: #1a1a2e;
        }

        .send-button {
            width: 42px;
            height: 42px;
            border-radius: 12px;
            border: none;
            background: #1a1a2e;
            color: white;
            cursor: pointer;
            font-size: 18px;
            transition: 0.3s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .send-button:hover {
            background: #f5c842;
            color: #1a1a2e;
        }

        .send-button:disabled {
            opacity: 0.4;
            cursor: not-allowed;
        }

        .disclaimer {
            text-align: center;
            font-size: 11px;
            color: #bbb;
            margin-top: 8px;
        }

        /* =========================
           OVERLAY
        ========================= */

        .overlay {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.3);
            z-index: 900;
        }

        .overlay.show {
            display: block;
        }

        /* =========================
           CART
        ========================= */

        .cart-panel {
            position: fixed;
            right: -420px;
            top: 0;
            width: 400px;
            height: 100vh;
            background: white;
            z-index: 2000;
            box-shadow: -5px 0 30px rgba(0,0,0,0.15);
            transition: 0.3s ease;
            padding: 24px;
            overflow-y: auto;
        }

        .cart-panel.open {
            right: 0;
        }

        .cart-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 12px;
            border-bottom: 1px solid #eee;
        }

        .cart-header h2 {
            font-size: 20px;
            font-weight: 700;
        }

        .cart-close {
            cursor: pointer;
            font-size: 28px;
            color: #888;
            background: none;
            border: none;
            padding: 4px;
        }

        .cart-close:hover {
            color: #1a1a2e;
        }

        .cart-item {
            border-bottom: 1px solid #f0f2f5;
            padding: 14px 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .cart-item .item-info {
            flex: 1;
        }

        .cart-item .item-info strong {
            font-size: 15px;
            color: #1a1a2e;
        }

        .cart-item .item-info .item-price {
            color: #1a1a2e;
            font-weight: 600;
            margin-top: 2px;
        }

        .cart-item .remove-btn {
            background: none;
            border: none;
            color: #999;
            cursor: pointer;
            font-size: 18px;
            padding: 4px 8px;
        }

        .cart-item .remove-btn:hover {
            color: #1a1a2e;
        }

        .cart-total {
            font-size: 20px;
            font-weight: 700;
            margin-top: 20px;
            padding-top: 16px;
            border-top: 2px solid #1a1a2e;
            display: flex;
            justify-content: space-between;
        }

        .checkout {
            width: 100%;
            margin-top: 16px;
            padding: 14px;
            border: none;
            background: #1a1a2e;
            color: white;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 700;
            font-size: 16px;
            transition: 0.3s;
            font-family: inherit;
        }

        .checkout:hover {
            background: #f5c842;
            color: #1a1a2e;
        }

        .empty-cart {
            text-align: center;
            padding: 40px 0;
            color: #888;
        }

        .empty-cart .empty-icon {
            font-size: 32px;
            margin-bottom: 12px;
            font-weight: 400;
        }

        /* =========================
           TYPING INDICATOR
        ========================= */

        .typing-indicator {
            display: none;
            align-items: center;
            gap: 12px;
            padding: 8px 0;
        }

        .typing-indicator.active {
            display: flex;
        }

        .typing-indicator .dots {
            display: flex;
            gap: 4px;
        }

        .typing-indicator .dots span {
            width: 8px;
            height: 8px;
            background: #1a1a2e;
            border-radius: 50%;
            animation: dotPulse 1.4s infinite both;
        }

        .typing-indicator .dots span:nth-child(2) { animation-delay: 0.2s; }
        .typing-indicator .dots span:nth-child(3) { animation-delay: 0.4s; }

        @keyframes dotPulse {
            0%, 80%, 100% { transform: scale(0.6); opacity: 0.3; }
            40% { transform: scale(1); opacity: 1; }
        }

        .typing-indicator .typing-text {
            font-size: 14px;
            color: #888;
        }

        /* =========================
           RESPONSIVE
        ========================= */

        /* Desktop: 4 items per row */
        @media (min-width: 1025px) {
            .products {
                grid-template-columns: repeat(4, 1fr);
            }

            .chat-container {
                max-width: 1100px;
            }

            .input-box {
                max-width: 1100px;
            }
        }

        /* Tablet: 3 items per row */
        @media (max-width: 1024px) and (min-width: 601px) {
            .products {
                grid-template-columns: repeat(3, 1fr);
                gap: 14px;
            }

            .chat-container {
                max-width: 100%;
            }

            .input-box {
                max-width: 100%;
            }

            .product-card {
                min-height: 250px;
                max-height: 320px;
            }

            .product-image {
                height: 110px;
                font-size: 38px;
            }
        }

        /* Mobile: 2 items per row */
        @media (max-width: 600px) {
            .sidebar {
                width: 280px;
            }

            .welcome h1 {
                font-size: 22px;
            }

            .quick-options {
                grid-template-columns: 1fr;
                max-width: 100%;
            }

            .cart-panel {
                width: 100%;
                right: -100%;
            }

            .chat-area {
                padding: 16px 14px 140px;
            }

            .input-area {
                padding: 12px 12px 16px;
            }

            .input-box {
                padding: 4px 4px 4px 14px;
                max-width: 100%;
            }

            .input-actions button {
                font-size: 12px;
                padding: 4px 8px;
            }

            .send-button {
                width: 38px;
                height: 38px;
                font-size: 16px;
            }

            .category-grid {
                grid-template-columns: repeat(3, 1fr);
            }

            .products {
                grid-template-columns: repeat(2, 1fr);
                gap: 10px;
            }

            .product-card {
                min-height: 210px;
                max-height: 280px;
            }

            .product-image {
                height: 90px;
                font-size: 32px;
            }

            .product-info {
                padding: 8px 10px 10px;
            }

            .product-info h3 {
                font-size: 12px;
                min-height: 30px;
            }

            .product-info .product-desc {
                font-size: 11px;
                min-height: 24px;
            }

            .product-price {
                font-size: 14px;
            }

            .product-button {
                font-size: 12px;
                padding: 6px;
            }

            .welcome .brand-display .big-symbol {
                width: 56px;
                height: 56px;
            }

            .welcome .brand-display .big-symbol .line {
                width: 28px;
            }

            .welcome .brand-display .big-symbol::after {
                width: 16px;
                height: 16px;
            }
        }

        /* Small mobile: 2 items per row with smaller cards */
        @media (max-width: 400px) {
            .products {
                grid-template-columns: repeat(2, 1fr);
                gap: 8px;
            }

            .product-card {
                min-height: 190px;
                max-height: 250px;
            }

            .product-image {
                height: 75px;
                font-size: 28px;
            }

            .product-info h3 {
                font-size: 11px;
                min-height: 24px;
            }

            .product-info .product-desc {
                font-size: 10px;
                min-height: 20px;
                display: -webkit-box;
                -webkit-line-clamp: 2;
                -webkit-box-orient: vertical;
                overflow: hidden;
            }

            .product-price {
                font-size: 13px;
            }

            .product-button {
                font-size: 11px;
                padding: 5px;
            }

            .category-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }
    </style>
</head>

<body>

    <!-- ==========================================
         SIDEBAR
    ========================================== -->

    <div class="sidebar" id="sidebar">

        <div class="sidebar-header">
            <div class="logo">
                <span class="brand-symbol"><span class="line"></span><span class="line"></span></span>
                Price<span>Pulse</span>
            </div>
            <button class="close-menu" onclick="closeSidebar()">×</button>
        </div>

        <button class="new-chat-btn" onclick="newChat()">
            ✦ New Chat
        </button>

        <div class="sidebar-content">

            <div class="section-title">Shopping</div>

            <button class="menu-item" onclick="openCart()">
                <span class="icon">🛒</span> My Cart
                <span class="badge" id="sideCartCount">0</span>
            </button>

            <button class="menu-item" onclick="quickAsk('Show me my orders')">
                <span class="icon">📦</span> My Orders
            </button>

            <button class="menu-item" onclick="quickAsk('Show me deals')">
                <span class="icon">⭐</span> Deals
            </button>

            <div class="section-title">Account</div>

            <button class="menu-item" onclick="quickAsk('Help me with shopping')">
                <span class="icon">❓</span> Help
            </button>

        </div>

    </div>

    <div class="overlay" id="overlay" onclick="closeSidebar()"></div>

    <!-- ==========================================
         MAIN
    ========================================== -->

    <div class="main">

        <!-- TOP BAR -->
        <div class="topbar">
            <div class="left-top">
                <button class="hamburger" onclick="openSidebar()">☰</button>
                <div class="top-logo">
                    <span class="brand-symbol"></span>
                    Price<span>Pulse</span>
                </div>
            </div>
            <div class="profile">U</div>
        </div>

        <!-- CHAT -->
        <div class="chat-area" id="chatArea">
            <div class="chat-container" id="chatContainer">

                <!-- WELCOME -->
                <div class="welcome" id="welcome">
                    <div class="brand-display">
                        <span class="big-symbol"><span class="line"></span><span class="line"></span></span>
                        <span class="ai-label">AI Shopping Assistant</span>
                    </div>
                    <h1>What are you shopping for?</h1>
                    <p>Ask PricePulse AI to find, compare and recommend products for you.</p>

                    <div class="quick-options">
                        <div class="quick" onclick="quickAsk('I need a phone under GH₵2,000')">
                            <span class="quick-icon">📱</span>
                            <strong>Find a phone</strong>
                            <small>Find phones within my budget</small>
                        </div>

                        <div class="quick" onclick="quickAsk('I need a laptop for university')">
                            <span class="quick-icon">💻</span>
                            <strong>Find a laptop</strong>
                            <small>Help me choose a laptop</small>
                        </div>

                        <div class="quick" onclick="quickAsk('Show me electronics')">
                            <span class="quick-icon">🔌</span>
                            <strong>Electronics</strong>
                            <small>Explore electronic products</small>
                        </div>

                        <div class="quick" onclick="quickAsk('Show me agricultural products')">
                            <span class="quick-icon">🌾</span>
                            <strong>Agriculture</strong>
                            <small>Farming products and equipment</small>
                        </div>
                    </div>
                </div>

                <!-- Typing Indicator -->
                <div class="typing-indicator" id="typingIndicator">
                    <div class="dots">
                        <span></span>
                        <span></span>
                        <span></span>
                    </div>
                    <span class="typing-text">PricePulse AI is thinking...</span>
                </div>

            </div>
        </div>

    </div>

    <!-- ==========================================
         INPUT AREA
    ========================================== -->

    <div class="input-area">
        <div class="input-box">
            <textarea id="userInput" placeholder="Ask PricePulse AI anything..." onkeydown="handleKey(event)"></textarea>
            <div class="input-actions">
                <button onclick="toggleSearch()" id="searchBtn">Search</button>
            </div>
            <button class="send-button" onclick="sendMessage()">↑</button>
        </div>
        <div class="disclaimer">PricePulse AI can make recommendations. Always check product information before purchasing.</div>
    </div>

    <!-- ==========================================
         CART
    ========================================== -->

    <div class="cart-panel" id="cartPanel">
        <div class="cart-header">
            <h2>My Cart</h2>
            <button class="cart-close" onclick="closeCart()">×</button>
        </div>
        <div id="cartItems">
            <div class="empty-cart">
                <div class="empty-icon">○</div>
                <p>Your cart is empty.</p>
                <p style="font-size:13px; color:#bbb;">Start shopping to add items!</p>
            </div>
        </div>
        <div class="cart-total">
            <span>Total:</span>
            <span>GH₵<span id="cartTotal">0</span></span>
        </div>
        <button class="checkout" onclick="checkout()">Proceed to Checkout</button>
    </div>

    <!-- ==========================================
         JAVASCRIPT
    ========================================== -->

    <script>
        // ==========================================
        // PRODUCTS DATABASE
        // ==========================================

        const products = [{
            name: "Samsung Galaxy A15",
            category: "Phones",
            price: 1800,
            icon: "📱",
            description: "Affordable smartphone with good battery life."
        }, {
            name: "Tecno Camon 30",
            category: "Phones",
            price: 2300,
            icon: "📱",
            description: "Smartphone suitable for photography."
        }, {
            name: "iPhone 13",
            category: "Phones",
            price: 4200,
            icon: "📱",
            description: "Premium smartphone with strong performance."
        }, {
            name: "HP Core i5 Laptop",
            category: "Laptops",
            price: 4500,
            icon: "💻",
            description: "Good laptop for students and office."
        }, {
            name: "Dell Latitude",
            category: "Laptops",
            price: 3800,
            icon: "💻",
            description: "Reliable business and university laptop."
        }, {
            name: "Wireless Bluetooth Headphones",
            category: "Electronics",
            price: 450,
            icon: "🎧",
            description: "Wireless headphones with 20hr battery."
        }, {
            name: "Sony Noise Cancelling Headphones",
            category: "Electronics",
            price: 1200,
            icon: "🎧",
            description: "Premium headphones with noise cancellation."
        }, {
            name: "Men's Casual Shirt",
            category: "Fashion",
            price: 180,
            icon: "👕",
            description: "Comfortable casual shirt for everyday."
        }, {
            name: "Running Shoes",
            category: "Shoes",
            price: 350,
            icon: "👟",
            description: "Lightweight shoes for running and gym."
        }, {
            name: "Rice 5kg",
            category: "Groceries",
            price: 120,
            icon: "🍚",
            description: "5kg bag of premium quality rice."
        }, {
            name: "Fertilizer 50kg",
            category: "Agriculture",
            price: 450,
            icon: "🌾",
            description: "Agricultural fertilizer for crop production."
        }, {
            name: "Knapsack Sprayer",
            category: "Agriculture",
            price: 600,
            icon: "🚜",
            description: "Manual agricultural spraying equipment."
        }, {
            name: "Smart Watch Pro",
            category: "Electronics",
            price: 850,
            icon: "⌚",
            description: "Fitness smartwatch with GPS."
        }, {
            name: "Sofa Set 3-Seater",
            category: "Furniture",
            price: 3200,
            icon: "🛋️",
            description: "Comfortable 3-seater sofa for living room."
        }, {
            name: "Wireless Mouse",
            category: "Electronics",
            price: 120,
            icon: "🖱️",
            description: "Ergonomic wireless mouse with 2yr battery."
        }, {
            name: "Backpack Laptop Bag",
            category: "Fashion",
            price: 250,
            icon: "🎒",
            description: "Durable laptop bag with 15.6 inch capacity."
        }, {
            name: "Gaming Monitor 24\"",
            category: "Electronics",
            price: 1500,
            icon: "🖥️",
            description: "144Hz gaming monitor with 1ms response."
        }, {
            name: "Office Chair Ergonomic",
            category: "Furniture",
            price: 800,
            icon: "🪑",
            description: "Ergonomic chair with lumbar support."
        }, {
            name: "Wireless Earbuds",
            category: "Electronics",
            price: 280,
            icon: "🎧",
            description: "True wireless earbuds with noise isolation."
        }, {
            name: "Men's Running Shorts",
            category: "Fashion",
            price: 95,
            icon: "🩳",
            description: "Lightweight running shorts with zipper pocket."
        }];

        let cart = [];
        let searchEnabled = false;
        let isNewChat = false;

        // ==========================================
        // CATEGORIES DATA
        // ==========================================

        const categories = [
            { name: 'Phones', icon: '📱' },
            { name: 'Laptops', icon: '💻' },
            { name: 'Electronics', icon: '🔌' },
            { name: 'Fashion', icon: '👕' },
            { name: 'Shoes', icon: '👟' },
            { name: 'Groceries', icon: '🛒' },
            { name: 'Agriculture', icon: '🌾' },
            { name: 'Furniture', icon: '🪑' }
        ];

        // ==========================================
        // SIDEBAR
        // ==========================================

        function openSidebar() {
            document.getElementById("sidebar").classList.add("open");
            document.getElementById("overlay").classList.add("show");
        }

        function closeSidebar() {
            document.getElementById("sidebar").classList.remove("open");
            document.getElementById("overlay").classList.remove("show");
        }

        // ==========================================
        // NEW CHAT
        // ==========================================

        function newChat() {
            closeSidebar();

            const container = document.getElementById("chatContainer");
            const welcome = document.getElementById("welcome");
            const typing = document.getElementById("typingIndicator");

            const children = container.children;
            for (let i = children.length - 1; i >= 0; i--) {
                const child = children[i];
                if (child.id !== "welcome" && child.id !== "typingIndicator") {
                    child.remove();
                }
            }

            if (welcome) {
                welcome.style.display = 'block';
            }

            document.getElementById("userInput").value = '';

            setTimeout(() => {
                removeWelcome();
                showCategoryPrompt();
            }, 300);
        }

        // ==========================================
        // SHOW CATEGORY PROMPT
        // ==========================================

        function showCategoryPrompt() {
            const container = document.getElementById("chatContainer");

            const message = document.createElement("div");
            message.className = "message ai";

            let categoryHTML = `
                <div class="message-content">
                    <strong>Welcome to PricePulse AI</strong>
                    <br><br>
                    What would you like to shop for today?
                    <br><br>
                    <div class="category-grid">
            `;

            categories.forEach(cat => {
                categoryHTML += `
                    <div class="cat-item" onclick="quickAsk('Show me ${cat.name}')">
                        <span class="cat-icon">${cat.icon}</span>
                        <span class="cat-name">${cat.name}</span>
                    </div>
                `;
            });

            categoryHTML += `
                    </div>
                    <br>
                    <small style="color:#888;">Or type what you're looking for in the chat below.</small>
                </div>
            `;

            message.innerHTML = `
                <div class="avatar ai-avatar">AI</div>
                ${categoryHTML}
            `;

            container.appendChild(message);
            scrollChat();
        }

        // ==========================================
        // QUICK QUESTIONS
        // ==========================================

        function quickAsk(text) {
            document.getElementById("userInput").value = text;
            sendMessage();
        }

        // ==========================================
        // SEND MESSAGE
        // ==========================================

        function sendMessage() {
            const input = document.getElementById("userInput");
            const text = input.value.trim();
            if (!text) return;

            removeWelcome();
            addUserMessage(text);
            input.value = "";

            showTyping();

            setTimeout(function() {
                hideTyping();
                processAI(text);
            }, 500 + Math.random() * 400);
        }

        // ==========================================
        // ENTER KEY
        // ==========================================

        function handleKey(event) {
            if (event.key === "Enter" && !event.shiftKey) {
                event.preventDefault();
                sendMessage();
            }
        }

        // ==========================================
        // TOGGLE SEARCH
        // ==========================================

        function toggleSearch() {
            searchEnabled = !searchEnabled;
            const btn = document.getElementById('searchBtn');
            btn.classList.toggle('active');
            btn.style.color = searchEnabled ? '#1a1a2e' : '#888';
            btn.style.fontWeight = searchEnabled ? '600' : '400';
        }

        // ==========================================
        // REMOVE WELCOME
        // ==========================================

        function removeWelcome() {
            const welcome = document.getElementById("welcome");
            if (welcome) {
                welcome.style.display = 'none';
            }
        }

        // ==========================================
        // USER MESSAGE
        // ==========================================

        function addUserMessage(text) {
            const container = document.getElementById("chatContainer");
            const message = document.createElement("div");
            message.className = "message user";
            message.innerHTML = `
                <div class="message-content">${escapeHTML(text)}</div>
                <div class="avatar user-avatar">U</div>
            `;
            container.appendChild(message);
            scrollChat();
        }

        // ==========================================
        // AI MESSAGE
        // ==========================================

        function addAIMessage(text) {
            const container = document.getElementById("chatContainer");
            const message = document.createElement("div");
            message.className = "message ai";
            message.innerHTML = `
                <div class="avatar ai-avatar">AI</div>
                <div class="message-content">${text}</div>
            `;
            container.appendChild(message);
            scrollChat();
        }

        // ==========================================
        // TYPING INDICATOR
        // ==========================================

        function showTyping() {
            document.getElementById('typingIndicator').classList.add('active');
        }

        function hideTyping() {
            document.getElementById('typingIndicator').classList.remove('active');
        }

        // ==========================================
        // AI PROCESSING
        // ==========================================

        function processAI(text) {
            const lower = text.toLowerCase();

            const budgetMatch = lower.match(/(?:under|below|less than|budget)\s*(?:gh₵|ghc|₵)?\s*([\d,]+)/i);
            let budget = null;
            if (budgetMatch) {
                budget = parseInt(budgetMatch[1].replace(/,/g, ""));
            }

            const categoryMap = {
                phone: { cat: 'Phones', msg: 'I found some phones that may be suitable for you.' },
                iphone: { cat: 'Phones', msg: 'Here are some iPhones available.' },
                samsung: { cat: 'Phones', msg: 'Here are some Samsung phones.' },
                tecno: { cat: 'Phones', msg: 'Here are some Tecno phones.' },
                laptop: { cat: 'Laptops', msg: 'Here are some laptops I recommend.' },
                computer: { cat: 'Laptops', msg: 'Here are some computers available.' },
                electronics: { cat: 'Electronics', msg: 'Here are some electronics you may be interested in.' },
                headphone: { cat: 'Electronics', msg: 'Here are some headphones available.' },
                headset: { cat: 'Electronics', msg: 'Here are some headsets.' },
                fashion: { cat: 'Fashion', msg: 'Here are some fashion items.' },
                shirt: { cat: 'Fashion', msg: 'Here are some shirts.' },
                shoes: { cat: 'Shoes', msg: 'Here are some shoes available.' },
                sneaker: { cat: 'Shoes', msg: 'Here are some sneakers.' },
                groceries: { cat: 'Groceries', msg: 'Here are some groceries.' },
                rice: { cat: 'Groceries', msg: 'Here are some rice options.' },
                furniture: { cat: 'Furniture', msg: 'Here are some furniture items.' },
                sofa: { cat: 'Furniture', msg: 'Here are some sofas available.' },
                agriculture: { cat: 'Agriculture', msg: 'Here are some agricultural products.' },
                farm: { cat: 'Agriculture', msg: 'Here are some farming products.' },
                fertilizer: { cat: 'Agriculture', msg: 'Here are some fertilizers.' },
                sprayer: { cat: 'Agriculture', msg: 'Here are some sprayers available.' }
            };

            let detectedCategory = null;
            let categoryMessage = '';

            for (const [key, value] of Object.entries(categoryMap)) {
                if (lower.includes(key)) {
                    detectedCategory = value.cat;
                    categoryMessage = value.msg;
                    break;
                }
            }

            if (lower.includes('cheap') || lower.includes('cheapest') || lower.includes('affordable')) {
                let result = [...products].sort((a, b) => a.price - b.price).slice(0, 8);
                addAIMessage('These are some of the most affordable products available.');
                showProducts(result);
                return;
            }

            if (lower.includes('deal') || lower.includes('discount') || lower.includes('sale')) {
                let result = products.filter(p => p.price < 500);
                if (result.length === 0) result = products.slice(0, 8);
                addAIMessage('Here are some great deals and affordable products.');
                showProducts(result);
                return;
            }

            if (lower.includes('best') || lower.includes('recommend') || lower.includes('top')) {
                let result = [...products].sort((a, b) => b.price - a.price).slice(0, 8);
                addAIMessage('Here are some top-rated and premium products we recommend.');
                showProducts(result);
                return;
            }

            if (detectedCategory) {
                let result = products.filter(p => p.category === detectedCategory);
                if (budget !== null) {
                    result = result.filter(p => p.price <= budget);
                    if (result.length === 0) {
                        addAIMessage(
                            `I couldn't find any ${detectedCategory} under GH₵${budget.toLocaleString()}. Here are some options.`);
                        result = products.filter(p => p.category === detectedCategory);
                    } else {
                        categoryMessage = `${categoryMessage} I've filtered to show items under GH₵${budget.toLocaleString()}.`;
                    }
                }
                if (result.length > 8) {
                    result = result.slice(0, 8);
                }
                addAIMessage(categoryMessage);
                showProducts(result);
                return;
            }

            if (lower.includes('compare') || lower.includes('difference') || lower.includes('vs')) {
                let result = products.slice(0, 8);
                addAIMessage('Here\'s a price comparison of some popular products.');
                showProducts(result);
                return;
            }

            if (!detectedCategory && !lower.includes('cheap') && !lower.includes('best') && !lower.includes('deal')) {
                showCategoryPrompt();
                return;
            }

            let result = products;
            if (budget !== null) {
                result = result.filter(p => p.price <= budget);
                if (result.length === 0) {
                    addAIMessage(`I couldn't find products under GH₵${budget.toLocaleString()}. Showing all products.`);
                    result = products;
                } else {
                    addAIMessage(`I found ${result.length} products under GH₵${budget.toLocaleString()}.`);
                }
            } else {
                addAIMessage(`Here are some products available. You can ask for specific categories like "Phones", "Laptops", "Electronics", "Agriculture", or ask for "cheap" or "best" products.`);
            }
            if (result.length > 8) {
                result = result.slice(0, 8);
            }
            showProducts(result);
        }

        // ==========================================
        // PRODUCT DISPLAY - 4 per row, max 10 per column
        // ==========================================

        function showProducts(list) {
            const container = document.getElementById("chatContainer");

            const message = document.createElement("div");
            message.className = "message ai";

            let cards = "";

            if (list.length === 0) {
                cards = `<p>I couldn't find products matching your request. Try a different search!</p>`;
            } else {
                // Limit to 10 products max
                const displayList = list.slice(0, 10);

                cards = `<div class="products">`;
                displayList.forEach((product, index) => {
                    cards += `
                        <div class="product-card">
                            <div class="product-image">${product.icon}</div>
                            <div class="product-info">
                                <h3>${product.name}</h3>
                                <div class="product-desc">${product.description}</div>
                                <div class="product-price"><span class="currency">GH₵</span> ${product.price.toLocaleString()}</div>
                                <button class="product-button" onclick="addToCart(${products.indexOf(product)})">Add to Cart</button>
                            </div>
                        </div>
                    `;
                });
                cards += `</div>`;

                if (list.length > 10) {
                    cards += `<p style="text-align:center; color:#888; font-size:13px; margin-top:10px;">Showing 10 of ${list.length} products.</p>`;
                }
            }

            message.innerHTML = `
                <div class="avatar ai-avatar">AI</div>
                <div class="message-content">${cards}</div>
            `;

            container.appendChild(message);
            scrollChat();
        }

        // ==========================================
        // CART
        // ==========================================

        function addToCart(index) {
            const product = products[index];

            const existing = cart.find(item => item.name === product.name);
            if (existing) {
                addAIMessage(`<strong>${product.name}</strong> is already in your cart.`);
                return;
            }

            cart.push(product);
            updateCart();
            addAIMessage(`<strong>${product.name}</strong> has been added to your cart.`);
        }

        function updateCart() {
            const container = document.getElementById("cartItems");
            const count = document.getElementById("sideCartCount");

            count.textContent = cart.length;

            if (cart.length === 0) {
                container.innerHTML = `
                    <div class="empty-cart">
                        <div class="empty-icon">○</div>
                        <p>Your cart is empty.</p>
                        <p style="font-size:13px; color:#bbb;">Start shopping to add items!</p>
                    </div>
                `;
                document.getElementById("cartTotal").textContent = "0";
                return;
            }

            let total = 0;
            container.innerHTML = "";

            cart.forEach((item, index) => {
                total += item.price;
                container.innerHTML += `
                    <div class="cart-item">
                        <div class="item-info">
                            <strong>${item.icon} ${item.name}</strong>
                            <div class="item-price">GH₵ ${item.price.toLocaleString()}</div>
                        </div>
                        <button class="remove-btn" onclick="removeFromCart(${index})">✕</button>
                    </div>
                `;
            });

            document.getElementById("cartTotal").textContent = total.toLocaleString();
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCart();
        }

        function openCart() {
            document.getElementById("cartPanel").classList.add("open");
        }

        function closeCart() {
            document.getElementById("cartPanel").classList.remove("open");
        }

        function checkout() {
            if (cart.length === 0) {
                alert('Your cart is empty!');
                return;
            }
            alert(`Thank you for your order!\n\nTotal: GH₵ ${document.getElementById("cartTotal").textContent}\n\nThis would proceed to checkout with your affiliate links.`);
        }

        // ==========================================
        // SCROLL
        // ==========================================

        function scrollChat() {
            const area = document.querySelector(".chat-area");
            setTimeout(() => {
                area.scrollTop = area.scrollHeight;
            }, 100);
        }

        // ==========================================
        // SECURITY
        // ==========================================

        function escapeHTML(text) {
            const div = document.createElement("div");
            div.textContent = text;
            return div.innerHTML;
        }

        // ==========================================
        // INITIALIZE
        // ==========================================

        console.log('PricePulse AI — Smart Shopping Assistant');
        console.log('Products displayed: 4 per row, max 10 per column');
        console.log('DeepThink button removed from search engine.');
    </script>

</body>
</html>