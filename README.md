# teravolt-energyTest2
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Dashboard - Modern Web App</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #6366f1;
            --secondary: #8b5cf6;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --dark: #1e293b;
            --light: #f1f5f9;
            --white: #ffffff;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 2rem;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            color: var(--white);
            margin-bottom: 3rem;
            animation: fadeInDown 0.8s ease;
        }

        .header h1 {
            font-size: 3rem;
            margin-bottom: 0.5rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2rem;
            opacity: 0.9;
        }

        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
            margin-bottom: 2rem;
        }

        .card {
            background: var(--white);
            border-radius: 20px;
            padding: 2rem;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
            animation: fadeInUp 0.8s ease;
        }

        .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 60px rgba(0,0,0,0.2);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.5rem;
        }

        .card-title {
            font-size: 1.2rem;
            font-weight: 600;
            color: var(--dark);
        }

        .card-icon {
            width: 50px;
            height: 50px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            color: var(--white);
        }

        .icon-primary { background: linear-gradient(135deg, var(--primary), var(--secondary)); }
        .icon-success { background: linear-gradient(135deg, var(--success), #059669); }
        .icon-warning { background: linear-gradient(135deg, var(--warning), #d97706); }
        .icon-danger { background: linear-gradient(135deg, var(--danger), #dc2626); }

        .stat-value {
            font-size: 2.5rem;
            font-weight: 800;
            color: var(--dark);
            margin-bottom: 0.5rem;
        }

        .stat-label {
            color: #64748b;
            font-size: 0.9rem;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: var(--light);
            border-radius: 10px;
            overflow: hidden;
            margin-top: 1rem;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--primary), var(--secondary));
            border-radius: 10px;
            transition: width 1s ease;
            animation: progressAnimation 2s ease-in-out;
        }

        @keyframes progressAnimation {
            from { width: 0%; }
        }

        .chart-container {
            grid-column: span 2;
            background: var(--white);
            border-radius: 20px;
            padding: 2rem;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            animation: fadeInUp 0.8s ease 0.2s backwards;
        }

        .chart {
            display: flex;
            align-items: flex-end;
            justify-content: space-around;
            height: 250px;
            gap: 1rem;
            margin-top: 2rem;
        }

        .bar {
            flex: 1;
            background: linear-gradient(to top, var(--primary), var(--secondary));
            border-radius: 8px 8px 0 0;
            position: relative;
            cursor: pointer;
            transition: all 0.3s ease;
            animation: barGrow 1s ease-out backwards;
        }

        .bar:hover {
            opacity: 0.8;
            transform: scaleY(1.05);
        }

        .bar-label {
            position: absolute;
            bottom: -30px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 0.85rem;
            color: var(--dark);
            white-space: nowrap;
        }

        .bar-value {
            position: absolute;
            top: -30px;
            left: 50%;
            transform: translateX(-50%);
            font-weight: 600;
            color: var(--dark);
        }

        @keyframes barGrow {
            from {
                transform: scaleY(0);
            }
            to {
                transform: scaleY(1);
            }
        }

        .button-group {
            display: flex;
            gap: 1rem;
            margin-top: 2rem;
            flex-wrap: wrap;
        }

        .btn {
            padding: 0.8rem 2rem;
            border: none;
            border-radius: 10px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1rem;
            color: var(--white);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
        }

        .btn-success {
            background: linear-gradient(135deg, var(--success), #059669);
        }

        .btn-warning {
            background: linear-gradient(135deg, var(--warning), #d97706);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
        }

        .btn:active {
            transform: translateY(0);
        }

        .activity-feed {
            background: var(--white);
            border-radius: 20px;
            padding: 2rem;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            animation: fadeInUp 0.8s ease 0.4s backwards;
        }

        .activity-item {
            display: flex;
            gap: 1rem;
            padding: 1rem;
            border-left: 3px solid var(--primary);
            margin-bottom: 1rem;
            background: var(--light);
            border-radius: 8px;
            transition: all 0.3s ease;
        }

        .activity-item:hover {
            background: #e2e8f0;
            transform: translateX(5px);
        }

        .activity-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
            flex-shrink: 0;
        }

        .activity-content h4 {
            font-size: 1rem;
            margin-bottom: 0.3rem;
            color: var(--dark);
        }

        .activity-content p {
            font-size: 0.85rem;
            color: #64748b;
        }

        .time-badge {
            font-size: 0.75rem;
            color: #94a3b8;
            margin-left: auto;
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2rem;
            }

            .chart-container {
                grid-column: span 1;
            }

            .dashboard {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <h1>Interactive Dashboard</h1>
            <p>Real-time analytics and monitoring</p>
        </div>

        <!-- Stats Cards -->
        <div class="dashboard">
            <div class="card">
                <div class="card-header">
                    <span class="card-title">Total Users</span>
                    <div class="card-icon icon-primary">👥</div>
                </div>
                <div class="stat-value" id="users">12,458</div>
                <div class="stat-label">+15% from last month</div>
                <div class="progress-bar">
                    <div class="progress-fill" style="width: 75%;"></div>
                </div>
            </div>

            <div class="card">
                <div class="card-header">
                    <span class="card-title">Revenue</span>
                    <div class="card-icon icon-success">💰</div>
                </div>
                <div class="stat-value">$89,432</div>
                <div class="stat-label">+28% from last month</div>
                <div class="progress-bar">
                    <div class="progress-fill" style="width: 85%;"></div>
                </div>
            </div>

            <div class="card">
                <div class="card-header">
                    <span class="card-title">Active Sessions</span>
                    <div class="card-icon icon-warning">⚡</div>
                </div>
                <div class="stat-value" id="sessions">3,247</div>
                <div class="stat-label">Currently online</div>
                <div class="progress-bar">
                    <div class="progress-fill" style="width: 60%;"></div>
                </div>
            </div>

            <div class="card">
                <div class="card-header">
                    <span class="card-title">Tasks Completed</span>
                    <div class="card-icon icon-danger">✅</div>
                </div>
                <div class="stat-value" id="tasks">847</div>
                <div class="stat-label">89% completion rate</div>
                <div class="progress-bar">
                    <div class="progress-fill" style="width: 89%;"></div>
                </div>
            </div>
        </div>

        <!-- Chart -->
        <div class="chart-container">
            <div class="card-header">
                <h2 class="card-title">Weekly Performance</h2>
            </div>
            <div class="chart" id="chart">
                <div class="bar" style="height: 60%;">
                    <span class="bar-value">120</span>
                    <span class="bar-label">Mon</span>
                </div>
                <div class="bar" style="height: 80%;">
                    <span class="bar-value">160</span>
                    <span class="bar-label">Tue</span>
                </div>
                <div class="bar" style="height: 45%;">
                    <span class="bar-value">90</span>
                    <span class="bar-label">Wed</span>
                </div>
                <div class="bar" style="height: 95%;">
                    <span class="bar-value">190</span>
                    <span class="bar-label">Thu</span>
                </div>
                <div class="bar" style="height: 70%;">
                    <span class="bar-value">140</span>
                    <span class="bar-label">Fri</span>
                </div>
                <div class="bar" style="height: 55%;">
                    <span class="bar-value">110</span>
                    <span class="bar-label">Sat</span>
                </div>
                <div class="bar" style="height: 40%;">
                    <span class="bar-value">80</span>
                    <span class="bar-label">Sun</span>
                </div>
            </div>
            <div class="button-group">
                <button class="btn btn-primary" onclick="refreshData()">Refresh Data</button>
                <button class="btn btn-success" onclick="exportData()">Export Report</button>
                <button class="btn btn-warning" onclick="showNotification()">Send Alert</button>
            </div>
        </div>

        <!-- Activity Feed -->
        <div class="activity-feed">
            <div class="card-header">
                <h2 class="card-title">Recent Activity</h2>
            </div>
            <div class="activity-item">
                <div class="activity-icon icon-success">✓</div>
                <div class="activity-content">
                    <h4>New user registered</h4>
                    <p>John Doe joined the platform</p>
                </div>
                <span class="time-badge">2 min ago</span>
            </div>
            <div class="activity-item">
                <div class="activity-icon icon-primary">📊</div>
                <div class="activity-content">
                    <h4>Report generated</h4>
                    <p>Monthly analytics report is ready</p>
                </div>
                <span class="time-badge">15 min ago</span>
            </div>
            <div class="activity-item">
                <div class="activity-icon icon-warning">⚠️</div>
                <div class="activity-content">
                    <h4>System update</h4>
                    <p>Server maintenance scheduled for tonight</p>
                </div>
                <span class="time-badge">1 hour ago</span>
            </div>
            <div class="activity-item">
                <div class="activity-icon icon-danger">🔔</div>
                <div class="activity-content">
                    <h4>Payment received</h4>
                    <p>Invoice #12345 has been paid</p>
                </div>
                <span class="time-badge">2 hours ago</span>
            </div>
        </div>
    </div>

    <script>
        // Animate numbers on load
        function animateValue(id, start, end, duration) {
            let element = document.getElementById(id);
            if (!element) return;

            let range = end - start;
            let current = start;
            let increment = end > start ? 1 : -1;
            let stepTime = Math.abs(Math.floor(duration / range));

            let timer = setInterval(function() {
                current += increment * Math.ceil(range / 50);
                if ((increment > 0 && current >= end) || (increment < 0 && current <= end)) {
                    current = end;
                    clearInterval(timer);
                }
                element.textContent = current.toLocaleString();
            }, stepTime);
        }

        // Animate stats on page load
        window.addEventListener('load', function() {
            animateValue("users", 0, 12458, 2000);
            animateValue("sessions", 0, 3247, 2000);
            animateValue("tasks", 0, 847, 2000);
        });

        // Refresh data function
        function refreshData() {
            const users = document.getElementById('users');
            const sessions = document.getElementById('sessions');
            const tasks = document.getElementById('tasks');

            animateValue("users", parseInt(users.textContent.replace(/,/g, '')),
                        Math.floor(Math.random() * 5000) + 10000, 1500);
            animateValue("sessions", parseInt(sessions.textContent.replace(/,/g, '')),
                        Math.floor(Math.random() * 2000) + 2000, 1500);
            animateValue("tasks", parseInt(tasks.textContent.replace(/,/g, '')),
                        Math.floor(Math.random() * 500) + 500, 1500);

            showNotification('Data refreshed successfully!', 'success');
        }

        // Export data function
        function exportData() {
            showNotification('Report exported to Downloads folder', 'success');
        }

        // Show notification function
        function showNotification(message = 'Alert sent to all users!', type = 'warning') {
            const notification = document.createElement('div');
            notification.style.cssText = `
                position: fixed;
                top: 20px;
                right: 20px;
                padding: 1.5rem 2rem;
                background: ${type === 'success' ? 'linear-gradient(135deg, #10b981, #059669)' :
                              type === 'warning' ? 'linear-gradient(135deg, #f59e0b, #d97706)' :
                              'linear-gradient(135deg, #6366f1, #8b5cf6)'};
                color: white;
                border-radius: 12px;
                box-shadow: 0 10px 30px rgba(0,0,0,0.3);
                font-weight: 600;
                z-index: 10000;
                animation: slideIn 0.3s ease;
            `;
            notification.textContent = message;
            document.body.appendChild(notification);

            setTimeout(() => {
                notification.style.animation = 'slideOut 0.3s ease';
                setTimeout(() => notification.remove(), 300);
            }, 3000);
        }

        // Add slide animations
        const style = document.createElement('style');
        style.textContent = `
            @keyframes slideIn {
                from {
                    transform: translateX(400px);
                    opacity: 0;
                }
                to {
                    transform: translateX(0);
                    opacity: 1;
                }
            }
            @keyframes slideOut {
                from {
                    transform: translateX(0);
                    opacity: 1;
                }
                to {
                    transform: translateX(400px);
                    opacity: 0;
                }
            }
        `;
        document.head.appendChild(style);

        // Update time badges every minute
        setInterval(() => {
            const badges = document.querySelectorAll('.time-badge');
            badges.forEach((badge, index) => {
                const times = ['3 min ago', '16 min ago', '1 hour ago', '2 hours ago'];
                if (times[index]) badge.textContent = times[index];
            });
        }, 60000);
    </script>
</body>
</html>
