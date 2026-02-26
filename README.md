<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>cevi.n - Мониторинг панических атак</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        :root {
            --primary: #1a5f7a;
            --primary-light: #2a8db0;
            --secondary: #8a2be2;
            --secondary-light: #9d4edd;
            --success: #00b894;
            --warning: #fdcb6e;
            --danger: #e74c3c;
            --light: #f8f9fa;
            --dark: #2d3436;
            --gray: #636e72;
            --card-bg: #ffffff;
            --bg-color: #f0f8ff;
            --shadow: rgba(0, 0, 0, 0.08);
        }
        
        body {
            background-color: var(--bg-color);
            color: var(--dark);
            line-height: 1.6;
        }
        
        .container {
            width: 100%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        /* Header */
        header {
            background: linear-gradient(135deg, var(--primary) 0%, var(--secondary) 100%);
            color: white;
            padding: 20px 0;
            box-shadow: 0 4px 12px var(--shadow);
            position: relative;
            overflow: hidden;
        }
        
        header::before {
            content: "";
            position: absolute;
            top: -50%;
            right: -50%;
            width: 200%;
            height: 200%;
            background: radial-gradient(circle, rgba(255,255,255,0.1) 1px, transparent 1px);
            background-size: 30px 30px;
            opacity: 0.2;
            z-index: 0;
        }
        
        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: relative;
            z-index: 1;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo-icon {
            background-color: white;
            color: var(--primary);
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
            font-weight: bold;
        }
        
        .logo-text h1 {
            font-size: 32px;
            font-weight: 800;
            letter-spacing: -1px;
        }
        
        .logo-text p {
            font-size: 14px;
            opacity: 0.9;
        }
        
        .user-info {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .user-avatar {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background-color: white;
            color: var(--primary);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            font-weight: bold;
        }
        
        /* Main Content */
        .main-content {
            display: none;
            padding: 30px 0;
            min-height: calc(100vh - 180px);
        }
        
        .page-title {
            font-size: 28px;
            color: var(--primary);
            margin-bottom: 25px;
            padding-bottom: 15px;
            border-bottom: 2px solid var(--primary-light);
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .page-title i {
            color: var(--secondary);
        }
        
        /* Login Page */
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: calc(100vh - 180px);
            padding: 20px;
        }
        
        .login-box {
            background-color: var(--card-bg);
            border-radius: 20px;
            box-shadow: 0 10px 30px var(--shadow);
            width: 100%;
            max-width: 450px;
            padding: 40px;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        .login-box::before {
            content: "";
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(90deg, var(--primary) 0%, var(--secondary) 100%);
        }
        
        .login-title {
            font-size: 36px;
            color: var(--primary);
            margin-bottom: 10px;
            font-weight: 800;
            letter-spacing: -1px;
        }
        
        .login-subtitle {
            color: var(--gray);
            margin-bottom: 30px;
            font-size: 16px;
        }
        
        .form-group {
            margin-bottom: 25px;
            text-align: left;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--dark);
        }
        
        .form-control {
            width: 100%;
            padding: 15px;
            border: 2px solid #e0e6ea;
            border-radius: 10px;
            font-size: 16px;
            transition: all 0.3s;
        }
        
        .form-control:focus {
            border-color: var(--primary);
            outline: none;
            box-shadow: 0 0 0 3px rgba(26, 95, 122, 0.1);
        }
        
        .btn {
            display: inline-block;
            padding: 15px 30px;
            background: linear-gradient(90deg, var(--primary) 0%, var(--primary-light) 100%);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            width: 100%;
            margin-top: 10px;
        }
        
        .btn:hover {
            background: linear-gradient(90deg, var(--primary-light) 0%, var(--primary) 100%);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(26, 95, 122, 0.2);
        }
        
        .btn-secondary {
            background: linear-gradient(90deg, var(--secondary) 0%, var(--secondary-light) 100%);
        }
        
        .btn-secondary:hover {
            background: linear-gradient(90deg, var(--secondary-light) 0%, var(--secondary) 100%);
            box-shadow: 0 5px 15px rgba(138, 43, 226, 0.2);
        }
        
        .auth-link {
            margin-top: 25px;
            font-size: 14px;
            color: var(--gray);
        }
        
        .auth-link a {
            color: var(--primary);
            font-weight: 600;
            text-decoration: none;
        }
        
        .auth-link a:hover {
            text-decoration: underline;
        }
        
        /* Dashboard */
        .dashboard-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 25px;
            margin-bottom: 30px;
        }
        
        .card {
            background-color: var(--card-bg);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 15px var(--shadow);
            transition: transform 0.3s;
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .card-title {
            font-size: 20px;
            font-weight: 700;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .status-indicator {
            display: inline-block;
            width: 12px;
            height: 12px;
            border-radius: 50%;
            margin-right: 8px;
        }
        
        .status-good {
            background-color: var(--success);
            box-shadow: 0 0 8px var(--success);
        }
        
        .status-warning {
            background-color: var(--warning);
            box-shadow: 0 0 8px var(--warning);
        }
        
        .status-danger {
            background-color: var(--danger);
            box-shadow: 0 0 8px var(--danger);
        }
        
        .vitals-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
        }
        
        .vital-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            padding: 15px;
            border-radius: 10px;
            background-color: #f8fafc;
        }
        
        .vital-value {
            font-size: 32px;
            font-weight: 700;
            margin: 10px 0 5px;
        }
        
        .vital-label {
            font-size: 14px;
            color: var(--gray);
        }
        
        .vital-good {
            color: var(--success);
        }
        
        .vital-warning {
            color: var(--warning);
        }
        
        .vital-danger {
            color: var(--danger);
        }
        
        /* Charts */
        .charts-container {
            background-color: var(--card-bg);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 15px var(--shadow);
            margin-bottom: 30px;
        }
        
        .chart-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
            gap: 25px;
            margin-top: 20px;
        }
        
        .chart-container {
            background-color: #f8fafc;
            border-radius: 10px;
            padding: 20px;
        }
        
        .chart-title {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 15px;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .chart-canvas {
            width: 100%;
            height: 200px;
            background-color: white;
            border-radius: 8px;
            position: relative;
        }
        
        .chart-legend {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 15px;
            font-size: 14px;
        }
        
        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .legend-color {
            width: 12px;
            height: 12px;
            border-radius: 2px;
        }
        
        .ai-insights {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 25px;
        }
        
        .insight-card {
            background-color: #f8fafc;
            border-radius: 10px;
            padding: 20px;
            border-left: 4px solid var(--primary);
        }
        
        .insight-title {
            font-size: 16px;
            font-weight: 600;
            margin-bottom: 10px;
            color: var(--dark);
        }
        
        .insight-value {
            font-size: 28px;
            font-weight: 700;
            color: var(--primary);
            margin-bottom: 5px;
        }
        
        .insight-desc {
            font-size: 14px;
            color: var(--gray);
        }
        
        /* Device Connection */
        .device-connection {
            background-color: var(--card-bg);
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 15px var(--shadow);
            margin-bottom: 30px;
        }
        
        .device-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .device-card {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;
            padding: 20px;
            border-radius: 10px;
            background-color: #f8fafc;
            transition: all 0.3s;
        }
        
        .device-card:hover {
            background-color: #e8f4f8;
        }
        
        .device-icon {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            margin-bottom: 15px;
        }
        
        .device-connected .device-icon {
            background: linear-gradient(135deg, var(--success) 0%, #00cec9 100%);
        }
        
        .connect-btn {
            margin-top: 15px;
            padding: 10px 20px;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            width: 100%;
        }
        
        .connect-btn:hover {
            background-color: var(--primary-light);
        }
        
        .connect-btn.connected {
            background-color: var(--success);
        }
        
        .connect-btn.connected:hover {
            background-color: #00a085;
        }
        
        /* Navigation */
        .nav-tabs {
            display: flex;
            background-color: var(--card-bg);
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 12px var(--shadow);
            margin-bottom: 30px;
        }
        
        .nav-tab {
            flex: 1;
            text-align: center;
            padding: 18px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            color: var(--dark);
            border-bottom: 3px solid transparent;
        }
        
        .nav-tab:hover {
            background-color: #f8fafc;
            color: var(--primary);
        }
        
        .nav-tab.active {
            color: var(--primary);
            border-bottom: 3px solid var(--primary);
            background-color: #f0f9fb;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        /* Footer */
        footer {
            background-color: var(--dark);
            color: white;
            padding: 30px 0;
            text-align: center;
            margin-top: 50px;
        }
        
        .footer-content {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 20px;
        }
        
        .footer-logo {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 28px;
            font-weight: 800;
        }
        
        .footer-links {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        .footer-links a {
            color: #bdc3c7;
            text-decoration: none;
            transition: color 0.3s;
        }
        
        .footer-links a:hover {
            color: white;
        }
        
        .copyright {
            color: #95a5a6;
            font-size: 14px;
            margin-top: 10px;
        }
        
        /* Animation for status */
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .pulse {
            animation: pulse 2s infinite;
        }
        
        /* Results label in dashboard */
        .results-label {
            display: inline-block;
            background: linear-gradient(90deg, var(--success) 0%, #00cec9 100%);
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 14px;
            font-weight: 600;
            margin-top: 10px;
        }
        
        /* Real-time monitoring indicator */
        .monitoring-indicator {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            padding: 5px 12px;
            background-color: rgba(0, 184, 148, 0.1);
            border-radius: 20px;
            font-size: 14px;
            color: var(--success);
            margin-left: 15px;
        }
        
        .monitoring-indicator .pulse-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background-color: var(--success);
            animation: pulse 1.5s infinite;
        }
        
        /* Data time info */
        .data-time {
            font-size: 14px;
            color: var(--gray);
            margin-top: 10px;
            text-align: center;
        }
        
        /* Connection Flow */
        .connection-flow {
            margin-top: 30px;
            padding: 25px;
            background-color: #f8fafc;
            border-radius: 15px;
            border: 2px dashed var(--primary-light);
        }
        
        .flow-steps {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 20px;
            position: relative;
        }
        
        .flow-steps::before {
            content: '';
            position: absolute;
            top: 30px;
            left: 50px;
            right: 50px;
            height: 3px;
            background-color: var(--primary-light);
            z-index: 1;
        }
        
        .flow-step {
            display: flex;
            flex-direction: column;
            align-items: center;
            position: relative;
            z-index: 2;
            flex: 1;
        }
        
        .step-icon {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background-color: white;
            border: 3px solid var(--primary-light);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            color: var(--primary);
            margin-bottom: 10px;
        }
        
        .flow-step.active .step-icon {
            background-color: var(--primary);
            color: white;
            border-color: var(--primary);
        }
        
        .flow-step.completed .step-icon {
            background-color: var(--success);
            color: white;
            border-color: var(--success);
        }
        
        .step-text {
            font-size: 14px;
            font-weight: 600;
            color: var(--dark);
            text-align: center;
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            .dashboard-cards, .chart-grid, .ai-insights, .device-grid {
                grid-template-columns: 1fr;
            }
            
            .login-box {
                padding: 30px 20px;
            }
            
            .nav-tabs {
                flex-direction: column;
            }
            
            .header-content {
                flex-direction: column;
                gap: 20px;
                text-align: center;
            }
            
            .chart-grid {
                grid-template-columns: 1fr;
            }
            
            .login-title {
                font-size: 28px;
            }
            
            .flow-steps {
                flex-direction: column;
                gap: 30px;
            }
            
            .flow-steps::before {
                display: none;
            }
        }
        
        /* Device status */
        .device-status {
            margin-top: 10px;
            font-size: 12px;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .device-status.connected {
            color: var(--success);
        }
        
        .device-status.disconnected {
            color: var(--gray);
        }
        
        /* Time selector for charts */
        .time-selector {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .time-btn {
            padding: 8px 16px;
            background-color: #f8fafc;
            border: 2px solid #e0e6ea;
            border-radius: 8px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .time-btn:hover {
            background-color: #e8f4f8;
            border-color: var(--primary-light);
        }
        
        .time-btn.active {
            background-color: var(--primary);
            color: white;
            border-color: var(--primary);
        }

        /* ECG Status Style */
        .ecg-status {
            font-size: 18px;
            font-weight: 600;
            padding: 4px 12px;
            border-radius: 20px;
            background-color: #f0f9fb;
            margin-top: 5px;
        }
        .ecg-normal { color: var(--success); }
        .ecg-warning { color: var(--warning); }
        .ecg-danger { color: var(--danger); }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container header-content">
            <div class="logo">
                <div class="logo-icon">c</div>
                <div class="logo-text">
                    <h1>cevi.n</h1>
                    <p>Система мониторинга панических атак</p>
                </div>
            </div>
            <div class="user-info" id="userInfo" style="display: none;">
                <div class="user-avatar" id="userAvatar">ДП</div>
                <div>
                    <div id="userName">Демо Пользователь</div>
                    <div style="font-size: 14px; opacity: 0.8;">Статус: <span id="userStatus">Мониторинг активен</span></div>
                </div>
            </div>
        </div>
    </header>
    
    <!-- Login Page -->
    <div class="container login-container" id="loginPage">
        <div class="login-box">
            <div class="login-title">cevi.n</div>
            <div class="login-subtitle">Войдите в систему мониторинга</div>
            
            <form id="loginForm">
                <div class="form-group">
                    <label for="email"><i class="fas fa-envelope"></i> Электронная почта</label>
                    <input type="email" class="form-control" id="email" placeholder="demo@cevi.n" required>
                </div>
                
                <div class="form-group">
                    <label for="password"><i class="fas fa-lock"></i> Пароль</label>
                    <input type="password" class="form-control" id="password" placeholder="demo123" required>
                </div>
                
                <button type="submit" class="btn">Войти</button>
                
                <div class="auth-link">
                    <i class="fas fa-info-circle"></i> Используйте демо доступ
                </div>
            </form>
        </div>
    </div>
    
    <!-- Main Content (Dashboard) -->
    <div class="container main-content" id="mainContent">
        <!-- Navigation Tabs -->
        <div class="nav-tabs">
            <div class="nav-tab" data-tab="connection">
                <i class="fas fa-bluetooth-b"></i> Подключение
            </div>
            <div class="nav-tab active" data-tab="dashboard">
                <i class="fas fa-tachometer-alt"></i> Панель состояния
                <span class="monitoring-indicator" id="monitoringIndicator">
                    <span class="pulse-dot"></span>
                    Live
                </span>
            </div>
            <div class="nav-tab" data-tab="results">
                <i class="fas fa-chart-line"></i> Графики
            </div>
        </div>
        
        <!-- Connection Tab -->
        <div class="tab-content" id="connectionTab">
            <h2 class="page-title"><i class="fas fa-bluetooth-b"></i> Подключение устройств</h2>
            
            <div class="device-connection">
                <p style="margin-bottom: 20px; color: var(--dark); font-size: 16px;">
                    Подключите устройства для начала мониторинга показателей.
                </p>
                
                <div class="device-grid">
                    <!-- Основное устройство (носимое) -->
                    <div class="device-card" id="deviceMain">
                        <div class="device-icon">
                            <i class="fas fa-heartbeat"></i>
                        </div>
                        <h3>Основное устройство</h3>
                        <p style="color: var(--gray); font-size: 14px; margin-top: 5px;">Мониторинг пульса, ЭКГ, температуры, стресса</p>
                        <button class="connect-btn" data-device="main">Подключить</button>
                        <div class="device-status disconnected">
                            <i class="fas fa-times-circle"></i> Не подключено
                        </div>
                        <div style="margin-top: 15px; padding: 10px; background-color: #f0f9fb; border-radius: 8px; width: 100%; display: none;" id="deviceMainInfo">
                            <div style="display: flex; justify-content: space-between; font-size: 13px;">
                                <span>Заряд батареи:</span>
                                <span style="font-weight: 600; color: var(--success);">92%</span>
                            </div>
                            <div style="display: flex; justify-content: space-between; font-size: 13px; margin-top: 5px;">
                                <span>Сигнал:</span>
                                <span style="font-weight: 600; color: var(--success);">Отличный</span>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Смартфон (для уведомлений) -->
                    <div class="device-card" id="devicePhone">
                        <div class="device-icon">
                            <i class="fas fa-mobile-alt"></i>
                        </div>
                        <h3>Смартфон</h3>
                        <p style="color: var(--gray); font-size: 14px; margin-top: 5px;">Приложение для уведомлений и удаленного просмотра</p>
                        <button class="connect-btn" data-device="phone">Подключить</button>
                        <div class="device-status disconnected">
                            <i class="fas fa-times-circle"></i> Не подключено
                        </div>
                        <div style="margin-top: 15px; padding: 10px; background-color: #f0f9fb; border-radius: 8px; width: 100%; display: none;" id="devicePhoneInfo">
                            <div style="display: flex; justify-content: space-between; font-size: 13px;">
                                <span>Устройство:</span>
                                <span style="font-weight: 600;">iPhone 14 Pro</span>
                            </div>
                            <div style="display: flex; justify-content: space-between; font-size: 13px; margin-top: 5px;">
                                <span>Статус:</span>
                                <span style="font-weight: 600; color: var(--success);">Активно</span>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div style="margin-top: 30px; padding: 20px; background-color: #f0f9fb; border-radius: 10px;">
                    <h3 style="color: var(--primary); margin-bottom: 15px; display: flex; align-items: center; gap: 10px;">
                        <i class="fas fa-info-circle"></i> Техническая информация
                    </h3>
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 15px;">
                        <div style="padding: 15px; background-color: white; border-radius: 8px;">
                            <div style="font-weight: 600; color: var(--primary); margin-bottom: 5px;">Используемые модули</div>
                            <div style="font-size: 14px;">ESP32-C3 для беспроводной связи</div>
                        </div>
                        <div style="padding: 15px; background-color: white; border-radius: 8px;">
                            <div style="font-weight: 600; color: var(--primary); margin-bottom: 5px;">Протокол связи</div>
                            <div style="font-size: 14px;">Bluetooth 5.0 с шифрованием данных</div>
                        </div>
                        <div style="padding: 15px; background-color: white; border-radius: 8px;">
                            <div style="font-weight: 600; color: var(--primary); margin-bottom: 5px;">Частота обновления</div>
                            <div style="font-size: 14px;">Данные обновляются каждые 5 секунд</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Dashboard Tab -->
        <div class="tab-content active" id="dashboardTab">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
                <h2 class="page-title" style="margin-bottom: 0;"><i class="fas fa-heartbeat"></i> Текущее состояние</h2>
                <div id="monitoringTime" style="color: var(--gray); font-size: 14px;"></div>
            </div>
            
            <div class="dashboard-cards">
                <!-- Current State Card -->
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title"><i class="fas fa-user-check"></i> Текущее состояние</h3>
                        <div class="status-indicator pulse" id="overallStatus"></div>
                    </div>
                    <div class="vitals-grid">
                        <div class="vital-item">
                            <i class="fas fa-heartbeat fa-2x"></i>
                            <div class="vital-value" id="currentPulse">-</div>
                            <div class="vital-label">Пульс (уд/мин)</div>
                            <div style="font-size: 12px; margin-top: 5px;">Норма: 60-100</div>
                        </div>
                        <div class="vital-item">
                            <i class="fas fa-lungs fa-2x"></i>
                            <div class="vital-value" id="currentOxygen">-</div>
                            <div class="vital-label">Кислород (SpO2)</div>
                            <div style="font-size: 12px; margin-top: 5px;">Норма: 95-100%</div>
                        </div>
                        <div class="vital-item">
                            <i class="fas fa-temperature-high fa-2x"></i>
                            <div class="vital-value" id="currentTemp">-</div>
                            <div class="vital-label">Температура</div>
                            <div style="font-size: 12px; margin-top: 5px;">Норма: 36.0-37.2°C</div>
                        </div>
                        <div class="vital-item">
                            <i class="fas fa-brain fa-2x"></i>
                            <div class="vital-value" id="currentStress">-</div>
                            <div class="vital-label">Индекс стресса</div>
                            <div style="font-size: 12px; margin-top: 5px;">Норма: 0.0-0.5</div>
                        </div>
                        <div class="vital-item" style="grid-column: span 2;">
                            <i class="fas fa-heartbeat fa-2x" style="color: var(--secondary);"></i>
                            <div class="ecg-status" id="currentEcg">-</div>
                            <div class="vital-label">ЭКГ (ритм)</div>
                        </div>
                    </div>
                    
                    <div style="margin-top: 20px; padding: 15px; background-color: #f8fafc; border-radius: 10px;">
                        <div style="display: flex; align-items: center; gap: 10px; margin-bottom: 10px;">
                            <i class="fas fa-robot" style="color: var(--primary);"></i>
                            <div style="font-weight: 600; color: var(--dark);">ИИ анализ в реальном времени</div>
                        </div>
                        <p style="margin-top: 5px; font-size: 14px;" id="aiAnalysis">
                            Подключите устройство для начала мониторинга показателей.
                        </p>
                        <div class="data-time" id="lastUpdateTime">
                            Последнее обновление: <span id="currentTime">-</span>
                        </div>
                    </div>
                </div>
                
                <!-- Results Summary Card -->
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title"><i class="fas fa-chart-bar"></i> Результаты</h3>
                        <div class="monitoring-indicator">
                            <span class="pulse-dot"></span>
                            Ожидание
                        </div>
                    </div>
                    
                    <div style="margin-bottom: 20px;">
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                            <span>Сердечных случаев за всё время:</span>
                            <span style="font-weight: 600; color: var(--primary);" id="panicAttacks">0</span>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                            <span>Предупреждений системы:</span>
                            <span style="font-weight: 600; color: var(--warning);" id="systemWarnings">0</span>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                            <span>Средний пульс:</span>
                            <span style="font-weight: 600;" id="avgPulse">-</span>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin-bottom: 8px;">
                            <span>Средний уровень стресса:</span>
                            <span style="font-weight: 600;" id="avgStress">-</span>
                        </div>
                        <div style="display: flex; justify-content: space-between;">
                            <span>Средняя вариабельность сердечного ритма:</span>
                            <span style="font-weight: 600;" id="avgHRV">-</span>
                        </div>
                    </div>
                    
                    <div class="results-label" id="resultsStatus" style="background: linear-gradient(90deg, var(--gray) 0%, #a0aec0 100%);">Ожидание подключения</div>
                    
                    <div style="margin-top: 25px;">
                        <h4 style="color: var(--primary); margin-bottom: 15px; display: flex; align-items: center; gap: 10px;">
                            <i class="fas fa-robot"></i> ИИ оценка рисков
                        </h4>
                        <div class="ai-insights">
                            <div class="insight-card">
                                <div class="insight-title">Риск панической атаки</div>
                                <div class="insight-value" id="riskPanic">-</div>
                                <div class="insight-desc">Подключите устройство</div>
                            </div>
                            <div class="insight-card">
                                <div class="insight-title">Риск аритмии</div>
                                <div class="insight-value" id="riskArrhythmia">-</div>
                                <div class="insight-desc">На основе ЭКГ</div>
                            </div>
                            <div class="insight-card">
                                <div class="insight-title">Риск ишемии</div>
                                <div class="insight-value" id="riskIschemia">-</div>
                                <div class="insight-desc">Сегмент ST</div>
                            </div>
                            <div class="insight-card">
                                <div class="insight-title">Вегетативный дисбаланс</div>
                                <div class="insight-value" id="riskAutonomic">-</div>
                                <div class="insight-desc">Нервная регуляция</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div style="margin-top: 30px; padding: 20px; background-color: var(--card-bg); border-radius: 15px; box-shadow: 0 5px 15px var(--shadow);" id="deviceStatusPanel">
                <h3 style="color: var(--primary); margin-bottom: 15px; display: flex; align-items: center; gap: 10px;">
                    <i class="fas fa-info-circle"></i> Состояние устройств
                </h3>
                <div style="display: flex; gap: 20px; flex-wrap: wrap;" id="deviceStatusList">
                    <!-- Динамически заполняется скриптом -->
                </div>
            </div>
        </div>
        
        <!-- Results Tab -->
        <div class="tab-content" id="resultsTab">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                <h2 class="page-title" style="margin-bottom: 0;"><i class="fas fa-chart-line"></i> Графики в реальном времени</h2>
                <div id="sessionDuration" style="color: var(--gray); font-size: 14px;">
                    Выберите период
                </div>
            </div>
            
            <div class="charts-container">
                <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px;">
                    <h3 style="color: var(--primary); display: flex; align-items: center; gap: 10px;">
                        <i class="fas fa-heartbeat"></i> Динамика показателей
                    </h3>
                    <div class="time-selector">
                        <button class="time-btn active" data-time="10s">10 сек</button>
                        <button class="time-btn" data-time="1m">1 мин</button>
                        <button class="time-btn" data-time="10m">10 мин</button>
                        <button class="time-btn" data-time="1h">1 час</button>
                        <button class="time-btn" data-time="1d">День</button>
                        <button class="time-btn" data-time="1w">Неделя</button>
                        <button class="time-btn" data-time="1M">Месяц</button>
                    </div>
                </div>
                
                <div class="chart-grid">
                    <div class="chart-container">
                        <div class="chart-title">
                            <i class="fas fa-wave-square"></i> Вариабельность сердечного ритма (норма: 50-100 мс)
                        </div>
                        <div class="chart-canvas">
                            <canvas id="hrvChart"></canvas>
                        </div>
                        <div class="data-time" id="hrvTimeInfo">
                            Подключите устройство для отображения данных
                        </div>
                    </div>
                    
                    <div class="chart-container">
                        <div class="chart-title">
                            <i class="fas fa-tachometer-alt"></i> Уровень SpO2 (норма: 95-100%)
                        </div>
                        <div class="chart-canvas">
                            <canvas id="oxygenChart"></canvas>
                        </div>
                        <div class="data-time" id="oxygenTimeInfo">
                            Подключите устройство для отображения данных
                        </div>
                    </div>
                </div>
                
                <div class="chart-grid" style="margin-top: 25px;">
                    <div class="chart-container">
                        <div class="chart-title">
                            <i class="fas fa-fire"></i> Уровень стресса (норма: 0.0-0.5)
                        </div>
                        <div class="chart-canvas">
                            <canvas id="stressChart"></canvas>
                        </div>
                        <div class="data-time" id="stressTimeInfo">
                            Подключите устройство для отображения данных
                        </div>
                    </div>
                    
                    <div class="chart-container">
                        <div class="chart-title">
                            <i class="fas fa-heart"></i> Пульс (норма: 60-100 уд/мин)
                        </div>
                        <div class="chart-canvas">
                            <canvas id="pulseChart"></canvas>
                        </div>
                        <div class="data-time" id="pulseTimeInfo">
                            Подключите устройство для отображения данных
                        </div>
                    </div>
                </div>
                
                <div style="margin-top: 30px;">
                    <h3 style="color: var(--primary); margin-bottom: 20px; display: flex; align-items: center; gap: 10px;">
                        <i class="fas fa-robot"></i> ИИ анализ рисков
                    </h3>
                    
                    <div class="ai-insights">
                        <div class="insight-card">
                            <div class="insight-title">Риск панической атаки</div>
                            <div class="insight-value" id="riskPanicChart">-</div>
                            <div class="insight-desc">Подключите устройство</div>
                        </div>
                        <div class="insight-card">
                            <div class="insight-title">Риск аритмии</div>
                            <div class="insight-value" id="riskArrhythmiaChart">-</div>
                            <div class="insight-desc">На основе ЭКГ</div>
                        </div>
                        <div class="insight-card">
                            <div class="insight-title">Риск ишемии</div>
                            <div class="insight-value" id="riskIschemiaChart">-</div>
                            <div class="insight-desc">Сегмент ST</div>
                        </div>
                        <div class="insight-card">
                            <div class="insight-title">Вегетативный дисбаланс</div>
                            <div class="insight-value" id="riskAutonomicChart">-</div>
                            <div class="insight-desc">Нервная регуляция</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Footer -->
    <footer>
        <div class="container footer-content">
            <div class="footer-logo">
                <i class="fas fa-brain"></i>
                <span>cevi.n</span>
            </div>
            
            <div class="footer-links">
                <a href="#">О системе</a>
                <a href="#">Конфиденциальность</a>
                <a href="#">Поддержка</a>
                <a href="#">Исследования</a>
                <a href="#">Для врачей</a>
            </div>
            
            <div class="copyright">
                © 2023 cevi.n. Система мониторинга панических атак. Все права защищены.
            </div>
        </div>
    </footer>
    
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script>
        // DOM Elements
        const loginPage = document.getElementById('loginPage');
        const mainContent = document.getElementById('mainContent');
        const loginForm = document.getElementById('loginForm');
        const userInfo = document.getElementById('userInfo');
        const navTabs = document.querySelectorAll('.nav-tab');
        const tabContents = document.querySelectorAll('.tab-content');
        
        // Device connection elements
        const connectButtons = document.querySelectorAll('.connect-btn');
        
        // Dashboard elements
        const monitoringIndicator = document.getElementById('monitoringIndicator');
        const monitoringTime = document.getElementById('monitoringTime');
        const currentPulse = document.getElementById('currentPulse');
        const currentOxygen = document.getElementById('currentOxygen');
        const currentTemp = document.getElementById('currentTemp');
        const currentStress = document.getElementById('currentStress');
        const currentEcg = document.getElementById('currentEcg');
        const aiAnalysis = document.getElementById('aiAnalysis');
        const currentTime = document.getElementById('currentTime');
        const panicAttacks = document.getElementById('panicAttacks');
        const systemWarnings = document.getElementById('systemWarnings');
        const avgPulse = document.getElementById('avgPulse');
        const avgStress = document.getElementById('avgStress');
        const avgHRV = document.getElementById('avgHRV');
        const resultsStatus = document.getElementById('resultsStatus');
        const riskPanic = document.getElementById('riskPanic');
        const riskArrhythmia = document.getElementById('riskArrhythmia');
        const riskIschemia = document.getElementById('riskIschemia');
        const riskAutonomic = document.getElementById('riskAutonomic');
        const overallStatus = document.getElementById('overallStatus');
        
        // Results tab elements
        const riskPanicChart = document.getElementById('riskPanicChart');
        const riskArrhythmiaChart = document.getElementById('riskArrhythmiaChart');
        const riskIschemiaChart = document.getElementById('riskIschemiaChart');
        const riskAutonomicChart = document.getElementById('riskAutonomicChart');
        const timeButtons = document.querySelectorAll('.time-btn');
        
        // Device status
        const deviceStatusList = document.getElementById('deviceStatusList');
        
        // Chart instances
        let hrvChartInstance, oxygenChartInstance, stressChartInstance, pulseChartInstance;
        
        // Real-time data storage
        let realTimeData = {
            timestamps: [],
            pulse: [],
            oxygen: [],
            stress: [],
            hrv: []
        };
        
        // Base values within normal range
        let baseValues = {
            pulse: 72,
            oxygen: 97,
            stress: 0.35,
            hrv: 65,
            temperature: 36.6
        };
        
        // Device connection status (main device + phone)
        let deviceStatus = {
            main: false,
            phone: false
        };
        
        // Time interval for charts
        let currentTimeInterval = '10s';
        let dataInterval = null;
        let cardiacEventsCount = 0; // Симуляция сердечных случаев
        
        // Initialize empty charts
        function initCharts() {
            // Empty HRV Chart
            const hrvCtx = document.getElementById('hrvChart').getContext('2d');
            hrvChartInstance = new Chart(hrvCtx, {
                type: 'line',
                data: { labels: [], datasets: [{ label: 'HRV (мс)', data: [], borderColor: '#1a5f7a', backgroundColor: 'rgba(26, 95, 122, 0.1)', borderWidth: 2, fill: true, tension: 0.4 }] },
                options: { responsive: true, maintainAspectRatio: false, scales: { y: { min: 40, max: 110, grid: { color: 'rgba(0,0,0,0.05)' }, title: { display: true, text: 'мс' } }, x: { grid: { color: 'rgba(0,0,0,0.05)' } } }, plugins: { legend: { display: false } } }
            });
            
            // Empty Oxygen Chart
            const oxygenCtx = document.getElementById('oxygenChart').getContext('2d');
            oxygenChartInstance = new Chart(oxygenCtx, {
                type: 'line',
                data: { labels: [], datasets: [{ label: 'SpO2 (%)', data: [], borderColor: '#00b894', backgroundColor: 'rgba(0, 184, 148, 0.1)', borderWidth: 2, fill: true, tension: 0.4 }] },
                options: { responsive: true, maintainAspectRatio: false, scales: { y: { min: 94, max: 100, grid: { color: 'rgba(0,0,0,0.05)' }, title: { display: true, text: '%' } }, x: { grid: { color: 'rgba(0,0,0,0.05)' } } }, plugins: { legend: { display: false } } }
            });
            
            // Empty Stress Chart
            const stressCtx = document.getElementById('stressChart').getContext('2d');
            stressChartInstance = new Chart(stressCtx, {
                type: 'line',
                data: { labels: [], datasets: [{ label: 'Стресс', data: [], borderColor: '#fdcb6e', backgroundColor: 'rgba(253, 203, 110, 0.1)', borderWidth: 2, fill: true, tension: 0.4 }] },
                options: { responsive: true, maintainAspectRatio: false, scales: { y: { min: 0.1, max: 0.6, grid: { color: 'rgba(0,0,0,0.05)' } }, x: { grid: { color: 'rgba(0,0,0,0.05)' } } }, plugins: { legend: { display: false } } }
            });
            
            // Empty Pulse Chart
            const pulseCtx = document.getElementById('pulseChart').getContext('2d');
            pulseChartInstance = new Chart(pulseCtx, {
                type: 'line',
                data: { labels: [], datasets: [{ label: 'Пульс', data: [], borderColor: '#8a2be2', backgroundColor: 'rgba(138, 43, 226, 0.1)', borderWidth: 2, fill: true, tension: 0.4 }] },
                options: { responsive: true, maintainAspectRatio: false, scales: { y: { min: 55, max: 105, grid: { color: 'rgba(0,0,0,0.05)' }, title: { display: true, text: 'уд/мин' } }, x: { grid: { color: 'rgba(0,0,0,0.05)' } } }, plugins: { legend: { display: false } } }
            });
        }
        
        // Generate smooth data for charts based on time interval
        function generateChartData(interval) {
            let dataPoints = 10;
            let timeStep = 1;
            
            switch(interval) {
                case '1m': dataPoints = 30; timeStep = 2; break;
                case '10m': dataPoints = 50; timeStep = 12; break;
                case '1h': dataPoints = 60; timeStep = 60; break;
                case '1d': dataPoints = 80; timeStep = 1080; break;
                case '1w': dataPoints = 100; timeStep = 6048; break;
                case '1M': dataPoints = 120; timeStep = 21600; break;
                default: // 10s
                    dataPoints = 10; timeStep = 1;
            }
            
            realTimeData.timestamps = [];
            realTimeData.pulse = [];
            realTimeData.oxygen = [];
            realTimeData.stress = [];
            realTimeData.hrv = [];
            
            for (let i = 0; i < dataPoints; i++) {
                const timeValue = i * timeStep;
                let timeLabel;
                if (interval === '1d' || interval === '1w' || interval === '1M') {
                    timeLabel = `${Math.floor(timeValue/60)}ч`;
                } else {
                    timeLabel = timeValue + 'с';
                }
                realTimeData.timestamps.push(timeLabel);
                
                // Плавная генерация с трендом и шумом
                let trendFactor = Math.sin(i / dataPoints * Math.PI * 2) * 0.3;
                realTimeData.pulse.push(generateNormalValue(baseValues.pulse + trendFactor, 1.5, 60, 100));
                realTimeData.oxygen.push(generateNormalValue(baseValues.oxygen + trendFactor * 0.1, 0.3, 95, 100));
                realTimeData.stress.push(generateNormalValue(baseValues.stress + trendFactor * 0.05, 0.02, 0.1, 0.5));
                realTimeData.hrv.push(generateNormalValue(baseValues.hrv + trendFactor * 2, 3, 50, 100));
            }
        }
        // Generate a value within normal range with slight variation
        function generateNormalValue(base, variation, min, max) {
            const newValue = base + (Math.random() * variation * 2 - variation);
            return Math.max(min, Math.min(max, newValue));
        }
        
        // Update all data in real-time (every 5 seconds)
        function updateAllData() {
            const now = new Date();
            
            // Update current time display
            const timeString = now.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit', second:'2-digit'});
            currentTime.textContent = timeString;
            monitoringTime.textContent = `Время: ${timeString}`;
            
            // Only update data if main device is connected
            if (!deviceStatus.main) {
                // Show waiting state
                currentPulse.textContent = '-';
                currentOxygen.textContent = '-';
                currentTemp.textContent = '-';
                currentStress.textContent = '-';
                currentEcg.textContent = '-';
                aiAnalysis.textContent = 'Подключите основное устройство для начала мониторинга показателей.';
                return;
            }
            
            // Generate slight variations in base values (small spread)
            baseValues.pulse = generateNormalValue(72, 1.2, 60, 100);
            baseValues.oxygen = generateNormalValue(97, 0.3, 95, 100);
            baseValues.stress = generateNormalValue(0.35, 0.02, 0.1, 0.5);
            baseValues.hrv = generateNormalValue(65, 3, 50, 100);
            baseValues.temperature = generateNormalValue(36.6, 0.08, 36.0, 37.2);
            
            // Симуляция статуса ЭКГ
            const ecgTypes = ['Синусовый ритм', 'Синусовый ритм', 'Синусовый ритм', 'Синусовый ритм', 'Легкая брадикардия', 'Синусовая тахикардия'];
            const ecgValue = ecgTypes[Math.floor(Math.random() * ecgTypes.length)];
            let ecgClass = 'ecg-normal';
            if (ecgValue.includes('брадикардия') || ecgValue.includes('тахикардия')) ecgClass = 'ecg-warning';
            currentEcg.textContent = ecgValue;
            currentEcg.className = `ecg-status ${ecgClass}`;
            
            // Update dashboard displays
            currentPulse.textContent = Math.round(baseValues.pulse);
            currentOxygen.textContent = Math.round(baseValues.oxygen) + '%';
            currentTemp.textContent = baseValues.temperature.toFixed(1) + '°';
            currentStress.textContent = baseValues.stress.toFixed(2);
            
            // Update color indicators
            updateVitalColor(currentPulse, baseValues.pulse, 60, 100);
            updateVitalColor(currentOxygen, baseValues.oxygen, 95, 100);
            updateVitalColor(currentTemp, baseValues.temperature, 36.0, 37.2);
            updateVitalColor(currentStress, baseValues.stress, 0.0, 0.5);
            
            // Update averages (based on current chart data)
            if (realTimeData.pulse.length > 0) {
                const pulseAvg = Math.round(realTimeData.pulse.reduce((a, b) => a + b, 0) / realTimeData.pulse.length);
                const stressAvg = (realTimeData.stress.reduce((a, b) => a + b, 0) / realTimeData.stress.length).toFixed(2);
                const hrvAvg = Math.round(realTimeData.hrv.reduce((a, b) => a + b, 0) / realTimeData.hrv.length);
                
                avgPulse.textContent = `${pulseAvg} уд/мин`;
                avgStress.textContent = stressAvg;
                avgHRV.textContent = `${hrvAvg} мс`;
            }
            
            // Симуляция сердечных случаев (очень редко)
            if (Math.random() < 0.02) {
                cardiacEventsCount++;
                panicAttacks.textContent = cardiacEventsCount;
            }
            
            // Симуляция предупреждений
            systemWarnings.textContent = Math.floor(Math.random() * 3);
            
            // Calculate risks (all under 10%)
            const panicRisk = calculateRisk('panic');
            const arrhythmiaRisk = calculateRisk('arrhythmia');
            const ischemiaRisk = calculateRisk('ischemia');
            const autonomicRisk = calculateRisk('autonomic');
            
            // Update risk displays
            riskPanic.textContent = `${panicRisk}%`;
            riskArrhythmia.textContent = `${arrhythmiaRisk}%`;
            riskIschemia.textContent = `${ischemiaRisk}%`;
            riskAutonomic.textContent = `${autonomicRisk}%`;
            
            riskPanicChart.textContent = `${panicRisk}%`;
            riskArrhythmiaChart.textContent = `${arrhythmiaRisk}%`;
            riskIschemiaChart.textContent = `${ischemiaRisk}%`;
            riskAutonomicChart.textContent = `${autonomicRisk}%`;
            
            // Update AI analysis
            updateAIAnalysis(panicRisk, arrhythmiaRisk, ischemiaRisk, autonomicRisk);
            
            // Update charts with new data point (smoothly)
            updateCharts();
            
            // Update overall status
            updateOverallStatus(panicRisk, arrhythmiaRisk, ischemiaRisk, autonomicRisk);
        }
        
        // Update vital color based on value
        function updateVitalColor(element, value, min, max) {
            element.className = 'vital-value';
            if (value >= min && value <= max) {
                element.classList.add('vital-good');
            } else if ((value >= min * 0.9 && value < min) || (value > max && value <= max * 1.1)) {
                element.classList.add('vital-warning');
            } else {
                element.classList.add('vital-danger');
            }
        }
        
        // Calculate various risks (kept under 10%)
        function calculateRisk(type) {
            let risk = 2 + Math.random() * 5; // База 2-7%
            
            // Небольшая корреляция с показателями
            if (type === 'panic' && baseValues.stress > 0.4) risk += 2;
            if (type === 'arrhythmia' && (baseValues.pulse < 65 || baseValues.pulse > 85)) risk += 1.5;
            if (type === 'ischemia' && baseValues.oxygen < 96) risk += 2;
            if (type === 'autonomic' && (baseValues.hrv < 60 || baseValues.hrv > 80)) risk += 1.5;
            
            return Math.min(10, Math.round(risk * 10) / 10); // Max 10%, один знак после запятой
        }
        
        // Update AI analysis text
        function updateAIAnalysis(panic, arrhythmia, ischemia, autonomic) {
            let analysis = 'Показатели в норме. ';
            if (panic > 7 || arrhythmia > 7) {
                analysis = 'Незначительные отклонения. Рекомендуется контролировать дыхание.';
            } else {
                analysis = 'Все системы работают стабильно. Отличное состояние.';
            }
            aiAnalysis.textContent = analysis;
            
            if (panic < 5) {
                resultsStatus.textContent = 'Показатели в норме';
                resultsStatus.style.background = 'linear-gradient(90deg, var(--success) 0%, #00cec9 100%)';
            } else {
                resultsStatus.textContent = 'Требуется внимание';
                resultsStatus.style.background = 'linear-gradient(90deg, var(--warning) 0%, #fdcb6e 100%)';
            }
        }
        
        // Update overall status indicator
        function updateOverallStatus(panic, arrhythmia, ischemia, autonomic) {
            overallStatus.className = 'status-indicator pulse';
            const maxRisk = Math.max(panic, arrhythmia, ischemia, autonomic);
            if (maxRisk < 5) {
                overallStatus.classList.add('status-good');
            } else if (maxRisk < 8) {
                overallStatus.classList.add('status-warning');
            } else {
                overallStatus.classList.add('status-danger');
            }
        }
        
        // Update charts with new data
        function updateCharts() {
            generateChartData(currentTimeInterval);
            
            hrvChartInstance.data.labels = realTimeData.timestamps;
            hrvChartInstance.data.datasets[0].data = realTimeData.hrv;
            hrvChartInstance.update('none');
            
            oxygenChartInstance.data.labels = realTimeData.timestamps;
            oxygenChartInstance.data.datasets[0].data = realTimeData.oxygen;
            oxygenChartInstance.update('none');
            
            stressChartInstance.data.labels = realTimeData.timestamps;
            stressChartInstance.data.datasets[0].data = realTimeData.stress;
            stressChartInstance.update('none');
            
            pulseChartInstance.data.labels = realTimeData.timestamps;
            pulseChartInstance.data.datasets[0].data = realTimeData.pulse;
            pulseChartInstance.update('none');
            
            updateTimeInfoLabels();
        }
        
        // Update time info labels
        function updateTimeInfoLabels() {
            const timeLabels = {
                '10s': 'Последние 10 секунд', '1m': 'Последняя минута', '10m': 'Последние 10 минут',
                '1h': 'Последний час', '1d': 'Последние 24 часа', '1w': 'Последние 7 дней', '1M': 'Последние 30 дней'
            };
            
            document.getElementById('hrvTimeInfo').textContent = timeLabels[currentTimeInterval];
            document.getElementById('oxygenTimeInfo').textContent = timeLabels[currentTimeInterval];
            document.getElementById('stressTimeInfo').textContent = timeLabels[currentTimeInterval];
            document.getElementById('pulseTimeInfo').textContent = timeLabels[currentTimeInterval];
            document.getElementById('sessionDuration').textContent = `Период: ${timeLabels[currentTimeInterval]}`;
        }
        
        // Toggle device connection
        function toggleDeviceConnection(device) {
            const deviceCard = document.getElementById(device === 'main' ? 'deviceMain' : 'devicePhone');
            const connectBtn = deviceCard.querySelector('.connect-btn');
            const statusIndicator = deviceCard.querySelector('.device-status');
            const deviceInfo = document.getElementById(device === 'main' ? 'deviceMainInfo' : 'devicePhoneInfo');
            
            deviceStatus[device] = !deviceStatus[device];
            
            if (deviceStatus[device]) {
                // Connect device
                deviceCard.classList.add('device-connected');
                connectBtn.textContent = 'Отключить';
                connectBtn.classList.add('connected');
                statusIndicator.innerHTML = '<i class="fas fa-check-circle"></i> Подключено';
                statusIndicator.className = 'device-status connected';
                if (deviceInfo) deviceInfo.style.display = 'block';
            } else {
                // Disconnect device
                deviceCard.classList.remove('device-connected');
                connectBtn.textContent = 'Подключить';
                connectBtn.classList.remove('connected');
                statusIndicator.innerHTML = '<i class="fas fa-times-circle"></i> Не подключено';
                statusIndicator.className = 'device-status disconnected';
                if (deviceInfo) deviceInfo.style.display = 'none';
            }
            
            // Update monitoring indicator based on main device
            if (device === 'main') {
                if (deviceStatus.main) {
                    monitoringIndicator.innerHTML = '<span class="pulse-dot"></span> Live';
                    monitoringIndicator.style.backgroundColor = 'rgba(0, 184, 148, 0.1)';
                    monitoringIndicator.style.color = 'var(--success)';
                } else {
                    monitoringIndicator.innerHTML = '<span class="pulse-dot"></span> Ожидание';
                    monitoringIndicator.style.backgroundColor = 'rgba(253, 203, 110, 0.1)';
                    monitoringIndicator.style.color = 'var(--warning)';
                }
            }
            
            // Update device status panel
            updateDeviceStatusPanel();
            
            // Start/stop data interval based on main device
            if (deviceStatus.main) {
                if (!dataInterval) {
                    dataInterval = setInterval(updateAllData, 5000);
                    updateAllData();
                }
            } else {
                if (dataInterval) {
                    clearInterval(dataInterval);
                    dataInterval = null;
                }
            }
        }
        
        // Update device status panel
        function updateDeviceStatusPanel() {
            deviceStatusList.innerHTML = '';
            
            const devices = [
                { id: 'main', name: 'Основное устройство', icon: 'fa-heartbeat' },
                { id: 'phone', name: 'Смартфон', icon: 'fa-mobile-alt' }
            ];
            
            devices.forEach(device => {
                const isConnected = deviceStatus[device.id];
                const statusDiv = document.createElement('div');
                statusDiv.style.cssText = 'display: flex; align-items: center; gap: 10px; padding: 10px 15px; background-color: ' + (isConnected ? '#e8f6ef' : '#f8f9fa') + '; border-radius: 8px;';
                
                statusDiv.innerHTML = `
                    <i class="fas ${device.icon}" style="color: ${isConnected ? 'var(--success)' : 'var(--gray)'};"></i>
                    <div>
                        <div style="font-weight: 600;">${device.name}</div>
                        <div style="font-size: 14px; color: ${isConnected ? 'var(--success)' : 'var(--gray)'};">${isConnected ? 'Подключено' : 'Не подключено'}</div>
                    </div>
                `;
                
                deviceStatusList.appendChild(statusDiv);
            });
        }
        
        // Login functionality
        loginForm.addEventListener('submit', function(e) {
            e.preventDefault();
            loginPage.style.display = 'none';
            mainContent.style.display = 'block';
            userInfo.style.display = 'flex';
            
            initCharts();
            updateDeviceStatusPanel();
            updateAllData();
        });
        
        // Tab navigation
        navTabs.forEach(tab => {
            tab.addEventListener('click', function() {
                const tabId = this.getAttribute('data-tab');
                navTabs.forEach(t => t.classList.remove('active'));
                this.classList.add('active');
                
                tabContents.forEach(content => {
                    content.classList.remove('active');
                    if (content.id === `${tabId}Tab`) {
                        content.classList.add('active');
                    }
                });
            });
        });
        
        // Device connection buttons
        connectButtons.forEach(button => {
            button.addEventListener('click', function() {
                const device = this.getAttribute('data-device');
                toggleDeviceConnection(device);
            });
        });
        
        // Time interval selection for charts
        timeButtons.forEach(button => {
            button.addEventListener('click', function() {
                const time = this.getAttribute('data-time');
                currentTimeInterval = time;
                
                timeButtons.forEach(btn => btn.classList.remove('active'));
                this.classList.add('active');
                
                if (deviceStatus.main) {
                    updateCharts();
                }
            });
        });
        
        // Initial setup
        document.addEventListener('DOMContentLoaded', function() {
            document.getElementById('email').value = 'demo@cevi.n';
            document.getElementById('password').value = 'demo123';
        });
    </script>
</body>
</html>
