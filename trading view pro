<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TradingView Pro - Advanced Trading Platform</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        .chart-container { position: relative; height: 400px; }
        .indicator-panel { max-height: 300px; overflow-y: auto; }
        .signal-item { animation: pulse 2s infinite; }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.7; } }
        .premium-gradient { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .chart-tools { position: absolute; top: 10px; left: 10px; z-index: 10; }
        .alert-popup { position: fixed; top: 20px; right: 20px; z-index: 1000; }
    </style>
</head>
<body class="bg-gray-900 text-white font-sans">
    <!-- Login Modal -->
    <div id="loginModal" class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50">
        <div class="bg-gray-800 p-8 rounded-lg max-w-md w-full mx-4">
            <div class="text-center mb-6">
                <h1 class="text-3xl font-bold premium-gradient bg-clip-text text-transparent">TradingView Pro</h1>
                <p class="text-gray-400 mt-2">New Version - Premium Trading Platform</p>
            </div>
            
            <div class="space-y-4">
                <input type="email" placeholder="Email Address" class="w-full p-3 bg-gray-700 rounded border border-gray-600 focus:border-blue-500 focus:outline-none">
                <input type="password" placeholder="Password" class="w-full p-3 bg-gray-700 rounded border border-gray-600 focus:border-blue-500 focus:outline-none">
                <button onclick="showPricing()" class="w-full bg-blue-600 hover:bg-blue-700 p-3 rounded font-semibold transition-colors">Sign In / Register</button>
            </div>
            
            <div class="text-center mt-4">
                <p class="text-sm text-gray-400">New to TradingView Pro? <span class="text-blue-400 cursor-pointer" onclick="showPricing()">Choose Premium Plan</span></p>
            </div>
        </div>
    </div>

    <!-- Pricing Modal -->
    <div id="pricingModal" class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50 hidden">
        <div class="bg-gray-800 p-8 rounded-lg max-w-4xl w-full mx-4">
            <h2 class="text-2xl font-bold text-center mb-6">Choose Your Premium Plan</h2>
            
            <div class="grid md:grid-cols-3 gap-6">
                <!-- Monthly Plan -->
                <div class="bg-gray-700 p-6 rounded-lg border border-gray-600">
                    <h3 class="text-xl font-bold mb-2">Monthly</h3>
                    <div class="text-3xl font-bold mb-4">$20<span class="text-sm text-gray-400">/month</span></div>
                    <ul class="space-y-2 text-sm mb-6">
                        <li>✓ All Premium Indicators</li>
                        <li>✓ Multiple Charts</li>
                        <li>✓ Advanced Alerts</li>
                        <li>✓ Real-time Signals</li>
                        <li>✓ Technical Analysis Tools</li>
                    </ul>
                    <button onclick="selectPlan('monthly', 20)" class="w-full bg-blue-600 hover:bg-blue-700 p-3 rounded font-semibold transition-colors">Select Plan</button>
                </div>

                <!-- Annual Plan -->
                <div class="bg-gray-700 p-6 rounded-lg border-2 border-yellow-500 relative">
                    <div class="absolute -top-3 left-1/2 transform -translate-x-1/2 bg-yellow-500 text-black px-3 py-1 rounded text-sm font-bold">POPULAR</div>
                    <h3 class="text-xl font-bold mb-2">Annual</h3>
                    <div class="text-3xl font-bold mb-4">$110<span class="text-sm text-gray-400">/year</span></div>
                    <ul class="space-y-2 text-sm mb-6">
                        <li>✓ All Premium Indicators</li>
                        <li>✓ Multiple Charts</li>
                        <li>✓ Advanced Alerts</li>
                        <li>✓ Real-time Signals</li>
                        <li>✓ Technical Analysis Tools</li>
                        <li>✓ Priority Support</li>
                    </ul>
                    <button onclick="selectPlan('annual', 110)" class="w-full bg-yellow-500 hover:bg-yellow-600 text-black p-3 rounded font-semibold transition-colors">Select Plan</button>
                </div>

                <!-- Lifetime Plan -->
                <div class="bg-gray-700 p-6 rounded-lg border border-gray-600">
                    <h3 class="text-xl font-bold mb-2">Lifetime</h3>
                    <div class="text-3xl font-bold mb-4">$699<span class="text-sm text-gray-400">/once</span></div>
                    <ul class="space-y-2 text-sm mb-6">
                        <li>✓ All Premium Indicators</li>
                        <li>✓ Multiple Charts</li>
                        <li>✓ Advanced Alerts</li>
                        <li>✓ Real-time Signals</li>
                        <li>✓ Technical Analysis Tools</li>
                        <li>✓ Lifetime Updates</li>
                        <li>✓ VIP Support</li>
                    </ul>
                    <button onclick="selectPlan('lifetime', 699)" class="w-full bg-purple-600 hover:bg-purple-700 p-3 rounded font-semibold transition-colors">Select Plan</button>
                </div>
            </div>
            
            <div class="text-center mt-6">
                <button onclick="hidePricing()" class="text-gray-400 hover:text-white">Back to Login</button>
            </div>
        </div>
    </div>

    <!-- Payment Modal -->
    <div id="paymentModal" class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50 hidden">
        <div class="bg-gray-800 p-8 rounded-lg max-w-md w-full mx-4">
            <h2 class="text-2xl font-bold text-center mb-6">Complete Payment</h2>
            
            <div class="bg-gray-700 p-4 rounded mb-6">
                <div class="flex justify-between mb-2">
                    <span>Plan:</span>
                    <span id="selectedPlan" class="font-bold"></span>
                </div>
                <div class="flex justify-between mb-2">
                    <span>Amount:</span>
                    <span id="selectedAmount" class="font-bold text-green-400"></span>
                </div>
                <div class="text-sm text-gray-400 mt-4">
                    <p>Send USDT (TRC20) to:</p>
                    <div class="bg-gray-600 p-2 rounded mt-2 break-all text-xs">
                        0xa187F2767960e92915DAA7A88C8ED00D7C99cbf0
                    </div>
                </div>
            </div>
            
            <div class="space-y-4">
                <input type="text" placeholder="Transaction Hash" class="w-full p-3 bg-gray-700 rounded border border-gray-600 focus:border-blue-500 focus:outline-none">
                <button onclick="completePurchase()" class="w-full bg-green-600 hover:bg-green-700 p-3 rounded font-semibold transition-colors">Verify Payment & Activate</button>
            </div>
            
            <div class="text-center mt-4">
                <button onclick="hidePayment()" class="text-gray-400 hover:text-white">Cancel</button>
            </div>
        </div>
    </div>

    <!-- Main Trading Interface -->
    <div id="tradingInterface" class="hidden">
        <!-- Header -->
        <header class="bg-gray-800 border-b border-gray-700 p-4">
            <div class="flex items-center justify-between">
                <div class="flex items-center space-x-4">
                    <h1 class="text-2xl font-bold premium-gradient bg-clip-text text-transparent">TradingView Pro</h1>
                    <div class="flex space-x-2">
                        <button onclick="addChart()" class="bg-blue-600 hover:bg-blue-700 px-3 py-1 rounded text-sm">+ Chart</button>
                        <button onclick="showIndicators()" class="bg-purple-600 hover:bg-purple-700 px-3 py-1 rounded text-sm">Indicators</button>
                        <button onclick="showAlerts()" class="bg-yellow-600 hover:bg-yellow-700 px-3 py-1 rounded text-sm">Alerts</button>
                    </div>
                </div>
                
                <div class="flex items-center space-x-4">
                    <select id="symbolSelect" class="bg-gray-700 border border-gray-600 rounded px-3 py-1" onchange="changeSymbol()">
                        <option value="BTCUSDT">BTC/USDT</option>
                        <option value="ETHUSDT">ETH/USDT</option>
                        <option value="ADAUSDT">ADA/USDT</option>
                        <option value="DOTUSDT">DOT/USDT</option>
                        <option value="LINKUSDT">LINK/USDT</option>
                        <option value="BNBUSDT">BNB/USDT</option>
                        <option value="SOLUSDT">SOL/USDT</option>
                        <option value="MATICUSDT">MATIC/USDT</option>
                    </select>
                    <div class="text-green-400 font-bold" id="currentPrice">$43,250.00</div>
                    <div class="bg-green-600 px-2 py-1 rounded text-sm" id="priceChange">+2.45%</div>
                </div>
            </div>
        </header>

        <div class="flex h-screen">
            <!-- Left Sidebar -->
            <div class="w-64 bg-gray-800 border-r border-gray-700 p-4">
                <h3 class="font-bold mb-4">Live Signals</h3>
                <div class="space-y-3" id="signalsContainer">
                    <div class="signal-item bg-green-900 border border-green-600 p-3 rounded">
                        <div class="font-bold text-green-400">BUY Signal</div>
                        <div class="text-sm">BTC/USDT</div>
                        <div class="text-xs text-gray-400">RSI Oversold + MACD Cross</div>
                    </div>
                    <div class="signal-item bg-red-900 border border-red-600 p-3 rounded">
                        <div class="font-bold text-red-400">SELL Signal</div>
                        <div class="text-sm">ETH/USDT</div>
                        <div class="text-xs text-gray-400">Resistance Break Failure</div>
                    </div>
                    <div class="signal-item bg-blue-900 border border-blue-600 p-3 rounded">
                        <div class="font-bold text-blue-400">HOLD Signal</div>
                        <div class="text-sm">ADA/USDT</div>
                        <div class="text-xs text-gray-400">Consolidation Pattern</div>
                    </div>
                </div>

                <h3 class="font-bold mb-4 mt-6">Watchlist</h3>
                <div class="space-y-2" id="watchlistContainer">
                    <div class="flex justify-between items-center p-2 hover:bg-gray-700 rounded cursor-pointer" onclick="selectSymbol('BTCUSDT')">
                        <span>BTC/USDT</span>
                        <span class="text-green-400">+2.45%</span>
                    </div>
                    <div class="flex justify-between items-center p-2 hover:bg-gray-700 rounded cursor-pointer" onclick="selectSymbol('ETHUSDT')">
                        <span>ETH/USDT</span>
                        <span class="text-red-400">-1.23%</span>
                    </div>
                    <div class="flex justify-between items-center p-2 hover:bg-gray-700 rounded cursor-pointer" onclick="selectSymbol('ADAUSDT')">
                        <span>ADA/USDT</span>
                        <span class="text-green-400">+0.87%</span>
                    </div>
                </div>
            </div>

            <!-- Main Chart Area -->
            <div class="flex-1 p-4">
                <div class="bg-gray-800 rounded-lg p-4 h-full">
                    <!-- Chart Tools -->
                    <div class="chart-tools flex space-x-2 mb-4">
                        <button onclick="selectTool('line')" class="bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm">📏 Line</button>
                        <button onclick="selectTool('rectangle')" class="bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm">⬜ Rectangle</button>
                        <button onclick="selectTool('fibonacci')" class="bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm">🌀 Fibonacci</button>
                        <button onclick="selectTool('support')" class="bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm">📊 Support/Resistance</button>
                        <button onclick="clearDrawings()" class="bg-red-600 hover:bg-red-700 px-3 py-1 rounded text-sm">🗑️ Clear</button>
                    </div>

                    <!-- Chart Container -->
                    <div class="chart-container bg-gray-900 rounded">
                        <canvas id="mainChart"></canvas>
                    </div>

                    <!-- Timeframe Selector -->
                    <div class="flex space-x-2 mt-4">
                        <button onclick="changeTimeframe('1m')" class="bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm">1m</button>
                        <button onclick="changeTimeframe('5m')" class="bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm">5m</button>
                        <button onclick="changeTimeframe('15m')" class="bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm">15m</button>
                        <button onclick="changeTimeframe('1h')" class="bg-blue-600 hover:bg-blue-700 px-3 py-1 rounded text-sm">1h</button>
                        <button onclick="changeTimeframe('4h')" class="bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm">4h</button>
                        <button onclick="changeTimeframe('1d')" class="bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm">1d</button>
                    </div>
                </div>
            </div>

            <!-- Right Sidebar -->
            <div class="w-80 bg-gray-800 border-l border-gray-700 p-4">
                <div class="tabs flex space-x-2 mb-4">
                    <button onclick="showTab('indicators')" class="tab-btn bg-blue-600 px-3 py-1 rounded text-sm">Indicators</button>
                    <button onclick="showTab('alerts')" class="tab-btn bg-gray-700 px-3 py-1 rounded text-sm">Alerts</button>
                    <button onclick="showTab('analysis')" class="tab-btn bg-gray-700 px-3 py-1 rounded text-sm">Analysis</button>
                </div>

                <!-- Indicators Tab -->
                <div id="indicatorsTab" class="tab-content">
                    <h3 class="font-bold mb-4">Technical Indicators</h3>
                    <div class="indicator-panel space-y-2">
                        <div class="flex items-center justify-between p-2 bg-gray-700 rounded">
                            <span>RSI (14)</span>
                            <div class="flex items-center space-x-2">
                                <span class="text-yellow-400">67.5</span>
                                <input type="checkbox" checked onchange="toggleIndicator('rsi')">
                            </div>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-gray-700 rounded">
                            <span>MACD</span>
                            <div class="flex items-center space-x-2">
                                <span class="text-green-400">Bullish</span>
                                <input type="checkbox" checked onchange="toggleIndicator('macd')">
                            </div>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-gray-700 rounded">
                            <span>Bollinger Bands</span>
                            <div class="flex items-center space-x-2">
                                <span class="text-blue-400">Active</span>
                                <input type="checkbox" onchange="toggleIndicator('bb')">
                            </div>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-gray-700 rounded">
                            <span>EMA (20)</span>
                            <div class="flex items-center space-x-2">
                                <span class="text-purple-400">$42,890</span>
                                <input type="checkbox" checked onchange="toggleIndicator('ema20')">
                            </div>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-gray-700 rounded">
                            <span>SMA (50)</span>
                            <div class="flex items-center space-x-2">
                                <span class="text-orange-400">$41,250</span>
                                <input type="checkbox" onchange="toggleIndicator('sma50')">
                            </div>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-gray-700 rounded">
                            <span>Stochastic</span>
                            <div class="flex items-center space-x-2">
                                <span class="text-red-400">Overbought</span>
                                <input type="checkbox" onchange="toggleIndicator('stoch')">
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Alerts Tab -->
                <div id="alertsTab" class="tab-content hidden">
                    <h3 class="font-bold mb-4">Price Alerts</h3>
                    <div class="space-y-4">
                        <div class="bg-gray-700 p-3 rounded">
                            <input type="number" placeholder="Alert Price" class="w-full bg-gray-600 p-2 rounded mb-2">
                            <select class="w-full bg-gray-600 p-2 rounded mb-2">
                                <option>Above Price</option>
                                <option>Below Price</option>
                                <option>RSI Overbought</option>
                                <option>RSI Oversold</option>
                                <option>MACD Cross</option>
                            </select>
                            <button onclick="createAlert()" class="w-full bg-green-600 hover:bg-green-700 p-2 rounded">Create Alert</button>
                        </div>
                        
                        <div class="space-y-2" id="activeAlerts">
                            <div class="bg-yellow-900 border border-yellow-600 p-2 rounded">
                                <div class="flex justify-between items-center">
                                    <span class="text-sm">BTC > $45,000</span>
                                    <button onclick="removeAlert(this)" class="text-red-400 hover:text-red-300">×</button>
                                </div>
                            </div>
                            <div class="bg-blue-900 border border-blue-600 p-2 rounded">
                                <div class="flex justify-between items-center">
                                    <span class="text-sm">ETH RSI < 30</span>
                                    <button onclick="removeAlert(this)" class="text-red-400 hover:text-red-300">×</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Analysis Tab -->
                <div id="analysisTab" class="tab-content hidden">
                    <h3 class="font-bold mb-4">Market Analysis</h3>
                    <div class="space-y-4">
                        <div class="bg-gray-700 p-3 rounded">
                            <h4 class="font-bold text-green-400 mb-2">Overall Sentiment: Bullish</h4>
                            <div class="space-y-2 text-sm">
                                <div class="flex justify-between">
                                    <span>Technical Rating:</span>
                                    <span class="text-green-400">Strong Buy</span>
                                </div>
                                <div class="flex justify-between">
                                    <span>Moving Averages:</span>
                                    <span class="text-green-400">Buy (8/12)</span>
                                </div>
                                <div class="flex justify-between">
                                    <span>Oscillators:</span>
                                    <span class="text-yellow-400">Neutral (3/8)</span>
                                </div>
                            </div>
                        </div>
                        
                        <div class="bg-gray-700 p-3 rounded">
                            <h4 class="font-bold mb-2">Key Levels</h4>
                            <div class="space-y-1 text-sm">
                                <div class="flex justify-between">
                                    <span>Resistance 1:</span>
                                    <span class="text-red-400">$44,500</span>
                                </div>
                                <div class="flex justify-between">
                                    <span>Resistance 2:</span>
                                    <span class="text-red-400">$46,200</span>
                                </div>
                                <div class="flex justify-between">
                                    <span>Support 1:</span>
                                    <span class="text-green-400">$42,100</span>
                                </div>
                                <div class="flex justify-between">
                                    <span>Support 2:</span>
                                    <span class="text-green-400">$40,800</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Alert Notifications -->
    <div id="alertNotifications" class="alert-popup"></div>

    <script>
        let currentChart = null;
        let activeIndicators = ['rsi', 'macd', 'ema20'];
        let selectedTool = null;
        let alerts = [];
        let currentSymbol = 'BTCUSDT';
        let currentTimeframe = '1h';

        // Initialize the application
        function init() {
            // Show login modal by default
            document.getElementById('loginModal').classList.remove('hidden');
        }

        // Pricing functions
        function showPricing() {
            document.getElementById('loginModal').classList.add('hidden');
            document.getElementById('pricingModal').classList.remove('hidden');
        }

        function hidePricing() {
            document.getElementById('pricingModal').classList.add('hidden');
            document.getElementById('loginModal').classList.remove('hidden');
        }

        function selectPlan(plan, amount) {
            document.getElementById('selectedPlan').textContent = plan.charAt(0).toUpperCase() + plan.slice(1);
            document.getElementById('selectedAmount').textContent = '$' + amount + ' USDT';
            document.getElementById('pricingModal').classList.add('hidden');
            document.getElementById('paymentModal').classList.remove('hidden');
        }

        function hidePayment() {
            document.getElementById('paymentModal').classList.add('hidden');
            document.getElementById('pricingModal').classList.remove('hidden');
        }

        function completePurchase() {
            // Simulate payment verification
            document.getElementById('paymentModal').classList.add('hidden');
            document.getElementById('tradingInterface').classList.remove('hidden');
            initChart();
            startRealTimeUpdates();
            showNotification('Payment verified! Welcome to TradingView Pro!', 'success');
        }

        // Chart initialization
        function initChart() {
            const ctx = document.getElementById('mainChart').getContext('2d');
            
            // Generate sample candlestick data
            const data = generateCandlestickData();
            
            currentChart = new Chart(ctx, {
                type: 'line',
                data: {
                    labels: data.labels,
                    datasets: [{
                        label: currentSymbol,
                        data: data.prices,
                        borderColor: '#10B981',
                        backgroundColor: 'rgba(16, 185, 129, 0.1)',
                        borderWidth: 2,
                        fill: true
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            labels: { color: '#fff' }
                        }
                    },
                    scales: {
                        x: {
                            ticks: { color: '#9CA3AF' },
                            grid: { color: '#374151' }
                        },
                        y: {
                            ticks: { color: '#9CA3AF' },
                            grid: { color: '#374151' }
                        }
                    }
                }
            });
        }

        function generateCandlestickData() {
            const labels = [];
            const prices = [];
            let basePrice = 43250;
            
            for (let i = 0; i < 50; i++) {
                const date = new Date();
                date.setHours(date.getHours() - (49 - i));
                labels.push(date.toLocaleTimeString());
                
                basePrice += (Math.random() - 0.5) * 1000;
                prices.push(basePrice);
            }
            
            return { labels, prices };
        }

        // Symbol and timeframe functions
        function changeSymbol() {
            currentSymbol = document.getElementById('symbolSelect').value;
            updateChart();
            updatePrice();
        }

        function selectSymbol(symbol) {
            currentSymbol = symbol;
            document.getElementById('symbolSelect').value = symbol;
            updateChart();
            updatePrice();
        }

        function changeTimeframe(timeframe) {
            currentTimeframe = timeframe;
            // Update active button styling
            document.querySelectorAll('[onclick*="changeTimeframe"]').forEach(btn => {
                btn.className = 'bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm';
            });
            event.target.className = 'bg-blue-600 hover:bg-blue-700 px-3 py-1 rounded text-sm';
            updateChart();
        }

        function updateChart() {
            if (currentChart) {
                const data = generateCandlestickData();
                currentChart.data.labels = data.labels;
                currentChart.data.datasets[0].data = data.prices;
                currentChart.data.datasets[0].label = currentSymbol;
                currentChart.update();
            }
        }

        function updatePrice() {
            const prices = {
                'BTCUSDT': { price: 43250, change: '+2.45%', color: 'text-green-400' },
                'ETHUSDT': { price: 2680, change: '-1.23%', color: 'text-red-400' },
                'ADAUSDT': { price: 0.52, change: '+0.87%', color: 'text-green-400' },
                'DOTUSDT': { price: 7.85, change: '+3.21%', color: 'text-green-400' },
                'LINKUSDT': { price: 15.67, change: '-0.45%', color: 'text-red-400' },
                'BNBUSDT': { price: 315.20, change: '+1.89%', color: 'text-green-400' },
                'SOLUSDT': { price: 98.45, change: '+4.56%', color: 'text-green-400' },
                'MATICUSDT': { price: 1.12, change: '+2.34%', color: 'text-green-400' }
            };
            
            const symbolData = prices[currentSymbol];
            document.getElementById('currentPrice').textContent = '$' + symbolData.price.toLocaleString();
            document.getElementById('priceChange').textContent = symbolData.change;
            document.getElementById('priceChange').className = `px-2 py-1 rounded text-sm ${symbolData.change.startsWith('+') ? 'bg-green-600' : 'bg-red-600'}`;
        }

        // Drawing tools
        function selectTool(tool) {
            selectedTool = tool;
            document.querySelectorAll('[onclick*="selectTool"]').forEach(btn => {
                btn.className = 'bg-gray-700 hover:bg-gray-600 px-3 py-1 rounded text-sm';
            });
            event.target.className = 'bg-blue-600 hover:bg-blue-700 px-3 py-1 rounded text-sm';
            showNotification(`${tool.charAt(0).toUpperCase() + tool.slice(1)} tool selected`, 'info');
        }

        function clearDrawings() {
            showNotification('All drawings cleared', 'info');
        }

        // Indicator functions
        function toggleIndicator(indicator) {
            if (activeIndicators.includes(indicator)) {
                activeIndicators = activeIndicators.filter(i => i !== indicator);
                showNotification(`${indicator.toUpperCase()} indicator removed`, 'info');
            } else {
                activeIndicators.push(indicator);
                showNotification(`${indicator.toUpperCase()} indicator added`, 'success');
            }
        }

        // Alert functions
        function createAlert() {
            const alertData = {
                id: Date.now(),
                symbol: currentSymbol,
                condition: 'Price Alert',
                created: new Date().toLocaleString()
            };
            alerts.push(alertData);
            showNotification('Alert created successfully!', 'success');
        }

        function removeAlert(button) {
            button.closest('.bg-yellow-900, .bg-blue-900').remove();
            showNotification('Alert removed', 'info');
        }

        // Tab functions
        function showTab(tabName) {
            // Hide all tabs
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.add('hidden');
            });
            
            // Show selected tab
            document.getElementById(tabName + 'Tab').classList.remove('hidden');
            
            // Update button styles
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.className = 'tab-btn bg-gray-700 px-3 py-1 rounded text-sm';
            });
            event.target.className = 'tab-btn bg-blue-600 px-3 py-1 rounded text-sm';
        }

        // Chart management
        function addChart() {
            showNotification('New chart added to layout', 'success');
        }

        function showIndicators() {
            showTab('indicators');
        }

        function showAlerts() {
            showTab('alerts');
        }

        // Real-time updates
        function startRealTimeUpdates() {
            setInterval(() => {
                updatePrice();
                updateSignals();
            }, 5000);
        }

        function updateSignals() {
            const signals = ['BUY', 'SELL', 'HOLD'];
            const symbols = ['BTC/USDT', 'ETH/USDT', 'ADA/USDT', 'DOT/USDT'];
            const reasons = ['RSI Oversold', 'MACD Cross', 'Resistance Break', 'Support Hold', 'Volume Spike'];
            
            // Randomly update signals
            if (Math.random() > 0.7) {
                const signal = signals[Math.floor(Math.random() * signals.length)];
                const symbol = symbols[Math.floor(Math.random() * symbols.length)];
                const reason = reasons[Math.floor(Math.random() * reasons.length)];
                
                showNotification(`New ${signal} signal for ${symbol}: ${reason}`, 'info');
            }
        }

        // Notification system
        function showNotification(message, type) {
            const notification = document.createElement('div');
            const colors = {
                success: 'bg-green-600',
                error: 'bg-red-600',
                info: 'bg-blue-600',
                warning: 'bg-yellow-600'
            };
            
            notification.className = `${colors[type]} text-white p-4 rounded-lg mb-2 shadow-lg`;
            notification.textContent = message;
            
            document.getElementById('alertNotifications').appendChild(notification);
            
            setTimeout(() => {
                notification.remove();
            }, 5000);
        }

        // Initialize the application
        init();
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'96c52e9145c590fd',t:'MTc1NDcyMDc4Ni4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
