<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>积分签到系统</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#3B82F6',
                        secondary: '#10B981',
                        accent: '#8B5CF6',
                        dark: '#1E293B',
                        light: '#F8FAFC'
                    },
                    fontFamily: {
                        inter: ['Inter', 'sans-serif'],
                    },
                }
            }
        }
    </script>
    <style type="text/tailwindcss">
        @layer utilities {
            .content-auto {
                content-visibility: auto;
            }
            .text-shadow {
                text-shadow: 0 2px 4px rgba(0,0,0,0.1);
            }
            .card-hover {
                @apply transition-all duration-300 hover:shadow-lg hover:-translate-y-1;
            }
            .btn-primary {
                @apply bg-primary text-white px-6 py-2 rounded-lg font-medium transition-all duration-300 hover:bg-primary/90 hover:shadow-md active:scale-95;
            }
            .btn-secondary {
                @apply bg-secondary text-white px-6 py-2 rounded-lg font-medium transition-all duration-300 hover:bg-secondary/90 hover:shadow-md active:scale-95;
            }
            .btn-outline {
                @apply border border-primary text-primary px-6 py-2 rounded-lg font-medium transition-all duration-300 hover:bg-primary/10 active:scale-95;
            }
            .btn-danger {
                @apply bg-red-500 text-white px-6 py-2 rounded-lg font-medium transition-all duration-300 hover:bg-red-600 hover:shadow-md active:scale-95;
            }
        }
    </style>
</head>
<body class="font-inter bg-light text-dark min-h-screen flex flex-col">
    <!-- 导航栏 -->
    <nav id="navbar" class="fixed w-full z-50 transition-all duration-300 bg-white/90 backdrop-blur-sm shadow-sm">
        <div class="container mx-auto px-4 py-3 flex items-center justify-between">
            <div class="flex items-center space-x-2">
                <i class="fa fa-trophy text-primary text-2xl"></i>
                <span class="text-xl font-bold text-primary">积分签到系统</span>
            </div>
            <div class="hidden md:flex items-center space-x-8">
                <a href="#home" class="font-medium hover:text-primary transition-colors">首页</a>
                <a href="#check-in" class="font-medium hover:text-primary transition-colors">每日签到</a>
                <a href="#shop" class="font-medium hover:text-primary transition-colors">积分商城</a>
                <a href="#ranking" class="font-medium hover:text-primary transition-colors">积分排行</a>
            </div>
            <div class="flex items-center space-x-4">
                <span id="user-points" class="hidden md:flex items-center bg-primary/10 text-primary px-3 py-1 rounded-full text-sm">
                    <i class="fa fa-diamond mr-1"></i>
                    <span id="points-value">0</span> 积分
                </span>
                <button id="login-btn" class="btn-outline hidden md:block">
                    <i class="fa fa-user-circle mr-1"></i>登录
                </button>
                <button id="admin-login-btn" class="btn-outline hidden md:block">
                    <i class="fa fa-cog mr-1"></i>管理
                </button>
                <button id="mobile-menu-btn" class="md:hidden text-dark">
                    <i class="fa fa-bars text-xl"></i>
                </button>
            </div>
        </div>
        <!-- 移动端菜单 -->
        <div id="mobile-menu" class="hidden md:hidden bg-white shadow-md">
            <div class="container mx-auto px-4 py-2 flex flex-col space-y-3">
                <a href="#home" class="py-2 font-medium hover:text-primary transition-colors">首页</a>
                <a href="#check-in" class="py-2 font-medium hover:text-primary transition-colors">每日签到</a>
                <a href="#shop" class="py-2 font-medium hover:text-primary transition-colors">积分商城</a>
                <a href="#ranking" class="py-2 font-medium hover:text-primary transition-colors">积分排行</a>
                <button id="mobile-login-btn" class="btn-outline my-2">
                    <i class="fa fa-user-circle mr-1"></i>登录
                </button>
                <button id="mobile-admin-login-btn" class="btn-outline my-2">
                    <i class="fa fa-cog mr-1"></i>管理
                </button>
                <span id="mobile-user-points" class="hidden bg-primary/10 text-primary px-3 py-1 rounded-full text-sm self-start">
                    <i class="fa fa-diamond mr-1"></i>
                    <sp
