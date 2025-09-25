<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DepEd Student Report Card Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#2563eb',
                        secondary: '#64748b',
                        accent: '#f59e0b',
                        background: '#f8fafc',
                        foreground: '#0f172a',
                        muted: '#f1f5f9',
                        border: '#e2e8f0'
                    }
                }
            }
        }
    </script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
        }
        
        .card {
            transition: all 0.3s ease;
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
        }
        
        .grade-card {
            background: linear-gradient(135deg, #f8fafc 0%, #e2e8f0 100%);
        }
        
        .login-container {
            min-height: 100vh;
            background: linear-gradient(135deg, #2563eb 0%, #1e40af 100%);
        }
        
        .floating-label {
            transition: all 0.3s ease;
        }
        
        input:focus + .floating-label,
        input:not(:placeholder-shown) + .floating-label {
            transform: translateY(-24px);
            font-size: 0.75rem;
            color: #2563eb;
        }
        
        /* Logo Animation */
        .logo {
            transition: transform 0.3s ease;
        }
        
        .logo:hover {
            transform: scale(1.05);
        }
    </style>
</head>
<body class="bg-background text-foreground">
    
    <div id="loginScreen" class="login-container flex items-center justify-center p-4">
        <div class="bg-white rounded-xl shadow-2xl p-8 max-w-md w-full">
            <!-- PLACEHOLDER: Login Logo Section -->
            <div class="text-center mb-8">
                <div class="flex justify-center mb-4">
                   
                    <img src="shs.png" alt="Custom Logo" class="logo w-16 h-16 object-contain">
                </div>
                <h1 class="text-2xl font-bold text-foreground">Barretto Senior High School</h1>
                <p class="text-secondary mt-2">Access your report card securely</p>
            </div>
            
            <form id="loginForm" class="space-y-6">
                <div class="relative">
                    <input type="text" id="studentId" placeholder=" " class="w-full px-4 py-3 border border-border rounded-lg focus:outline-none focus:ring-2 focus:ring-primary peer">
                    <label for="studentId" class="floating-label absolute left-4 top-3 text-secondary pointer-events-none">Student ID</label>
                </div>
                
                <div class="relative">
                    <input type="password" id="password" placeholder=" " class="w-full px-4 py-3 border border-border rounded-lg focus:outline-none focus:ring-2 focus:ring-primary peer">
                    <label for="password" class="floating-label absolute left-4 top-3 text-secondary pointer-events-none">Password</label>
                </div>
                
                <div class="flex items-center justify-between">
                    <div class="flex items-center">
                        <input type="checkbox" id="remember" class="h-4 w-4 text-primary focus:ring-primary border-border rounded">
                        <label for="remember" class="ml-2 block text-sm text-secondary">Remember me</label>
                    </div>
                    <a href="#" class="text-sm text-primary hover:underline">Forgot password?</a>
                </div>
                
                <button type="submit" class="w-full bg-primary text-white py-3 px-4 rounded-lg font-medium hover:bg-blue-700 transition-colors focus:outline-none focus:ring-2 focus:ring-primary focus:ring-offset-2">
                    Sign In
                </button>
            </form>
            
            <p class="text-center text-secondary text-sm mt-6">
                This system provides secure access to your academic records.
            </p>
        </div>
    </div>
    
    <div id="dashboardScreen" class="hidden min-h-screen">
       
        <header class="bg-white shadow-sm border-b border-border">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between h-16 items-center">
                    <div class="flex items-center">
                        
                        <!-- Palitan mo ang src dito para sa iyong logo (local o URL) -->
                        <img src="shs.png" alt="Custom Logo" class="logo w-10 h-10 object-contain mr-3">
                        <span class="text-xl font-semibold text-foreground">Barretto Senior High School</span>
                    </div>
                    
                    <div class="flex items-center">
                        <button id="logoutBtn" class="bg-muted text-secondary px-4 py-2 rounded-lg text-sm font-medium hover:bg-gray-100 transition-colors">
                            <i class="fas fa-sign-out-alt mr-2"></i>Logout
                        </button>
                    </div>
                </div>
            </div>
        </header>
      
        <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <!-- Welcome Section -->
            <div class="mb-8">
                <h1 class="text-2xl font-bold text-foreground">Welcome, <span id="studentName">Maria Clara</span>!</h1>
                <p class="text-secondary mt-1">Here's your academic performance for this semester.</p>
            </div>
            
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
                <div class="card bg-white rounded-xl p-6 border border-border">
                    <div class="flex items-center">
                        <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                            <i class="fas fa-chart-line text-primary text-xl"></i>
                        </div>
                        <div class="ml-4">
                            <h3 class="text-sm font-medium text-secondary">Overall Average</h3>
                            <p id="overallAvg" class="text-2xl font-bold text-foreground">100.0%</p>
                        </div>
                    </div>
                </div>
                
                <div class="card bg-white rounded-xl p-6 border border-border">
                    <div class="flex items-center">
                        <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
                            <i class="fas fa-trophy text-green-600 text-xl"></i>
                        </div>
                        <div class="ml-4">
                            <h3 class="text-sm font-medium text-secondary">Highest Grade</h3>
                            <p id="highestGrade" class="text-2xl font-bold text-foreground">100%</p>
                        </div>
                    </div>
                </div>
                
                <div class="card bg-white rounded-xl p-6 border border-border">
                    <div class="flex items-center">
                        <div class="w-12 h-12 bg-amber-100 rounded-lg flex items-center justify-center">
                            <i class="fas fa-book-open text-amber-600 text-xl"></i>
                        </div>
                        <div class="ml-4">
                            <h3 class="text-sm font-medium text-secondary">Subjects</h3>
                            <p id="numSubjects" class="text-2xl font-bold text-foreground">7</p>
                        </div>
                    </div>
                </div>
            </div>
            
         
            <div class="bg-white rounded-xl shadow-sm border border-border overflow-hidden">
                <div class="px-6 py-5 border-b border-border">
                    <h2 class="text-lg font-medium text-foreground">Academic Report - October 1, 2025</h2>
                </div>
                
                <div id="reportCardBody" class="divide-y divide-border">
                    <!-- Grades will be populated dynamically here -->
                </div>
                
                <div class="px-6 py-4 bg-muted border-t border-border">
                    <div class="flex justify-between items-center">
                        <span class="font-medium text-foreground">Semester Average</span>
                        <span id="semesterAvg" class="font-bold text-primary text-lg">100.0%</span>
                    </div>
                </div>
            </div>
            
            <div class="mt-8 grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="bg-white rounded-xl p-6 border border-border">
                    <h3 class="font-medium text-foreground mb-4">Performance Trend</h3>
                    <div class="h-48 bg-muted rounded-lg flex items-center justify-center">
                        <p class="text-secondary">Graphical representation of grades over time</p>
                    </div>
                </div>
                
                <div class="bg-white rounded-xl p-6 border border-border">
                    <h3 class="font-medium text-foreground mb-4">Teacher's Comments</h3>
                    <div class="bg-blue-50 p-4 rounded-lg border border-blue-100">
                        <p class="text-sm text-foreground">
                            "Excellent performance across all subjects! Keep maintaining this outstanding level."
                        </p>
                        <p class="text-xs text-secondary mt-2">- Overall Faculty Comment</p>
                    </div>
                </div>
            </div>
        </main>
        
        
        <footer class="bg-white border-t border-border mt-12">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
                <div class="flex flex-col md:flex-row justify-between items-center">
                    <p class="text-sm text-secondary mt-2 md:mt-0">© 2025 School Name. All rights reserved.</p>
                </div>
            </div>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const loginForm = document.getElementById('loginForm');
            const loginScreen = document.getElementById('loginScreen');
            const dashboardScreen = document.getElementById('dashboardScreen');
            const logoutBtn = document.getElementById('logoutBtn');
            const studentNameEl = document.getElementById('studentName');
            
            
            const students = {
                '2021001': { 
                    password: 'password123', 
                    name: 'Juan Dela Cruz',
                    grades: [
                        { subject: 'Filipino sa Piling Larang', teacher: 'Mr. Banagan', grade: 80 },
                        { subject: 'Understanding Culture, Society and Politics', teacher: 'Ms. Echon', grade: 92 },
                        { subject: 'Contact Center Services', teacher: 'Ms. Balois', grade: 90 },
                        { subject: 'English for Academics & Professional Purporses', teacher: 'Mr. Manuel', grade: 96 },
                        { subject: 'Practical Research 2', teacher: 'Mr. Biag', grade: 87 },
                        { subject: 'Personal Development', teacher: 'Ms. Ortiz', grade: 96 },
                        { subject: 'Physical Education and Health 3', teacher: 'Ms. Damaso', grade: 90 }
                    ]
                },
                '123': { 
                    password: 'my', 
                    name: 'RJ Ildefonso',
                    grades: [
                        { subject: 'Filipino sa Piling Larang', teacher: 'Mr. Banagan', grade: 80 },
                        { subject: 'Understanding Culture, Society and Politics', teacher: 'Ms. Echon', grade: 92 },
                        { subject: 'Contact Center Services', teacher: 'Ms. Balois', grade: 90 },
                        { subject: 'English for Academics & Professional Purporses', teacher: 'Mr. Manuel', grade: 96 },
                        { subject: 'Practical Research 2', teacher: 'Mr. Biag', grade: 87 },
                        { subject: 'Personal Development', teacher: 'Ms. Ortiz', grade: 96 },
                        { subject: 'Physical Education and Health 3', teacher: 'Ms. Damaso', grade: 90 }
                    ]
                }
            };
            
       
            function calculateStats(grades) {
                const numSubjects = grades.length;
                const total = grades.reduce((sum, g) => sum + g.grade, 0);
                const overallAvg = (total / numSubjects).toFixed(1) + '%';
                const highestGrade = Math.max(...grades.map(g => g.grade)) + '%';
                const semesterAvg = overallAvg; // Same as overall for now
                
               
                document.getElementById('overallAvg').textContent = overallAvg;
                document.getElementById('highestGrade').textContent = highestGrade;
                document.getElementById('numSubjects').textContent = numSubjects;
                document.getElementById('semesterAvg').textContent = semesterAvg;
                
                
                const reportCardBody = document.getElementById('reportCardBody');
                reportCardBody.innerHTML = '';
                grades.forEach(grade => {
                    const row = `
                        <div class="px-6 py-4 flex justify-between items-center">
                            <div>
                                <h3 class="font-medium text-foreground">${grade.subject}</h3>
                                <p class="text-sm text-secondary">${grade.teacher}</p>
                            </div>
                            <div class="grade-card px-4 py-2 rounded-full">
                                <span class="font-bold text-foreground">${grade.grade}%</span>
                            </div>
                        </div>
                    `;
                    reportCardBody.innerHTML += row;
                });
            }
            
          
            loginForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                const studentId = document.getElementById('studentId').value.trim();
                const password = document.getElementById('password').value.trim();
                
                if (students[studentId] && students[studentId].password === password) {
                    // Successful login
                    const student = students[studentId];
                    studentNameEl.textContent = student.name;
                    calculateStats(student.grades); // Auto-calculate and update
                    loginScreen.classList.add('hidden');
                    dashboardScreen.classList.remove('hidden');
                } else {
                    // Error message (walang reveal ng credentials)
                    alert('Invalid Student ID or Password. Please try again.');
                }
            });
            
           
            logoutBtn.addEventListener('click', function() {
                loginScreen.classList.remove('hidden');
                dashboardScreen.classList.add('hidden');
                loginForm.reset();
            });
        });
    </script>
</body>
</html>
