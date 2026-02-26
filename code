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
            box-shadow: 0 5px 15px var(--shadow);
            margin-bottom: 30px;
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
            top: 50%;
            left: 0;
            right: 0;
            height: 2px;
            background-color: var(--primary-light);
            z-index: -1;
        }
