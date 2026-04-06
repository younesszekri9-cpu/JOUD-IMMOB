<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="ImmoSaison">
    <title>ImmoSaison - Dashboard</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        :root {
            --primary: #1a73e8;
            --primary-dark: #1557b0;
            --secondary: #34a853;
            --danger: #ea4335;
            --warning: #fbbc04;
            --purple: #9c27b0;
            --bg: #f0f4f8;
            --card: #ffffff;
            --text: #1a1a2e;
            --text-light: #6b7280;
            --border: #e5e7eb;
            --shadow: 0 4px 20px rgba(0,0,0,0.08);
            --radius: 16px;
            --nav-height: 70px;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'SF Pro Display', 'Segoe UI', sans-serif;
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
            padding-bottom: calc(var(--nav-height) + 20px);
            padding-top: env(safe-area-inset-top);
        }

        /* ===== HEADER ===== */
        .header {
            background: linear-gradient(135deg, #1a73e8 0%, #0d47a1 100%);
            padding: 20px 20px 30px;
            padding-top: calc(env(safe-area-inset-top) + 20px);
            color: white;
            position: relative;
            overflow: hidden;
        }

        .header::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -20%;
            width: 300px;
            height: 300px;
            background: rgba(255,255,255,0.05);
            border-radius: 50%;
        }

        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .agency-name {
            font-size: 22px;
            font-weight: 700;
            letter-spacing: -0.5px;
        }

        .agency-subtitle {
            font-size: 12px;
            opacity: 0.8;
            margin-top: 2px;
        }

        .header-avatar {
            width: 44px;
            height: 44px;
            background: rgba(255,255,255,0.2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            cursor: pointer;
        }

        .header-stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-top: 10px;
        }

        .header-stat {
            background: rgba(255,255,255,0.15);
            border-radius: 12px;
            padding: 12px;
            text-align: center;
            backdrop-filter: blur(10px);
        }

        .header-stat-value {
            font-size: 24px;
            font-weight: 700;
        }

        .header-stat-label {
            font-size: 10px;
            opacity: 0.8;
            margin-top: 2px;
        }

        /* ===== NAVIGATION ===== */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            height: var(--nav-height);
            background: white;
            border-top: 1px solid var(--border);
            display: flex;
            align-items: center;
            justify-content: space-around;
            padding-bottom: env(safe-area-inset-bottom);
            z-index: 1000;
            box-shadow: 0 -4px 20px rgba(0,0,0,0.08);
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            padding: 8px 16px;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.2s;
            color: var(--text-light);
            border: none;
            background: none;
            font-family: inherit;
        }

        .nav-item.active {
            color: var(--primary);
        }

        .nav-item.active .nav-icon {
            background: rgba(26, 115, 232, 0.1);
        }

        .nav-icon {
            width: 36px;
            height: 36px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            transition: all 0.2s;
        }

        .nav-label {
            font-size: 10px;
            font-weight: 600;
        }

        /* ===== PAGES ===== */
        .page {
            display: none;
            padding: 20px;
            animation: fadeIn 0.3s ease;
        }

        .page.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ===== CARDS ===== */
        .card {
            background: var(--card);
            border-radius: var(--radius);
            padding: 18px;
            box-shadow: var(--shadow);
            margin-bottom: 15px;
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .card-title {
            font-size: 16px;
            font-weight: 700;
            color: var(--text);
        }

        .section-title {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 15px;
            color: var(--text);
        }

        /* ===== BUTTONS ===== */
        .btn {
            padding: 12px 20px;
            border-radius: 12px;
            border: none;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            font-family: inherit;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn-primary {
            background: var(--primary);
            color: white;
        }

        .btn-primary:active {
            background: var(--primary-dark);
            transform: scale(0.98);
        }

        .btn-success {
            background: var(--secondary);
            color: white;
        }

        .btn-danger {
            background: var(--danger);
            color: white;
        }

        .btn-outline {
            background: transparent;
            border: 2px solid var(--primary);
            color: var(--primary);
        }

        .btn-sm {
            padding: 8px 14px;
            font-size: 12px;
            border-radius: 8px;
        }

        .btn-full {
            width: 100%;
            justify-content: center;
        }

        .fab {
            position: fixed;
            bottom: calc(var(--nav-height) + 20px);
            right: 20px;
            width: 56px;
            height: 56px;
            border-radius: 50%;
            background: var(--primary);
            color: white;
            border: none;
            font-size: 24px;
            cursor: pointer;
            box-shadow: 0 4px 20px rgba(26, 115, 232, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 999;
            transition: all 0.2s;
        }

        .fab:active {
            transform: scale(0.95);
        }

        /* ===== FORMS ===== */
        .form-group {
            margin-bottom: 16px;
        }

        .form-label {
            display: block;
            font-size: 13px;
            font-weight: 600;
            color: var(--text-light);
            margin-bottom: 6px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .form-control {
            width: 100%;
            padding: 13px 16px;
            border: 2px solid var(--border);
            border-radius: 12px;
            font-size: 15px;
            font-family: inherit;
            color: var(--text);
            background: white;
            transition: border-color 0.2s;
            -webkit-appearance: none;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--primary);
        }

        select.form-control {
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 12 12'%3E%3Cpath fill='%236b7280' d='M6 8L1 3h10z'/%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: right 16px center;
            padding-right: 40px;
        }

        .form-row {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
        }

        /* ===== MODAL ===== */
        .modal-overlay {
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.5);
            z-index: 2000;
            display: none;
            align-items: flex-end;
            backdrop-filter: blur(4px);
        }

        .modal-overlay.active {
            display: flex;
        }

        .modal {
            background: white;
            border-radius: 24px 24px 0 0;
            width: 100%;
            max-height: 90vh;
            overflow-y: auto;
            padding: 20px;
            padding-bottom: calc(env(safe-area-inset-bottom) + 20px);
            animation: slideUp 0.3s ease;
        }

        @keyframes slideUp {
            from { transform: translateY(100%); }
            to { transform: translateY(0); }
        }

        .modal-handle {
            width: 40px;
            height: 4px;
            background: var(--border);
            border-radius: 2px;
            margin: 0 auto 20px;
        }

        .modal-title {
            font-size: 20px;
            font-weight: 700;
            margin-bottom: 20px;
            text-align: center;
        }

        /* ===== APARTMENT CARDS ===== */
        .apt-card {
            background: white;
            border-radius: var(--radius);
            overflow: hidden;
            box-shadow: var(--shadow);
            margin-bottom: 15px;
        }

        .apt-card-header {
            background: linear-gradient(135deg, #1a73e8, #0d47a1);
            padding: 20px;
            color: white;
            position: relative;
        }

        .apt-card-emoji {
            font-size: 36px;
            margin-bottom: 8px;
        }

        .apt-card-name {
            font-size: 18px;
            font-weight: 700;
        }

        .apt-card-address {
            font-size: 12px;
            opacity: 0.8;
            margin-top: 4px;
        }

        .apt-status-badge {
            position: absolute;
            top: 15px;
            right: 15px;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 11px;
            font-weight: 700;
        }

        .status-available {
            background: rgba(52, 168, 83, 0.2);
            color: #34a853;
            border: 1px solid rgba(52, 168, 83, 0.3);
        }

        .status-occupied {
            background: rgba(234, 67, 53, 0.2);
            color: #ea4335;
            border: 1px solid rgba(234, 67, 53, 0.3);
        }

        .status-checkin {
            background: rgba(251, 188, 4, 0.2);
            color: #f57c00;
            border: 1px solid rgba(251, 188, 4, 0.3);
        }

        .apt-card-body {
            padding: 15px;
        }

        .apt-info-grid {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 15px;
        }

        .apt-info-item {
            text-align: center;
            padding: 10px;
            background: var(--bg);
            border-radius: 10px;
        }

        .apt-info-value {
            font-size: 18px;
            font-weight: 700;
            color: var(--primary);
        }

        .apt-info-label {
            font-size: 10px;
            color: var(--text-light);
            margin-top: 2px;
        }

        .apt-actions {
            display: flex;
            gap: 8px;
        }

        /* ===== RESERVATION CARDS ===== */
        .res-card {
            background: white;
            border-radius: var(--radius);
            padding: 16px;
            box-shadow: var(--shadow);
            margin-bottom: 12px;
            border-left: 4px solid var(--primary);
        }

        .res-card.checkout-today {
            border-left-color: var(--danger);
        }

        .res-card.checkin-today {
            border-left-color: var(--secondary);
        }

        .res-card.pending {
            border-left-color: var(--warning);
        }

        .res-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 12px;
        }

        .res-client-name {
            font-size: 16px;
            font-weight: 700;
        }

        .res-
