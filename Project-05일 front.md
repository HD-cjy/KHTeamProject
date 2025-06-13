## 필요 api정리
#### 컬럼에 들어간 필요 데이터
TODO_ 
1. 물품번호카테고리   -- 만들어야함. (Static ) 
2. ~~~댓글테이블(정보성) -foeginkey: 물품테이블~~~
   거래 후기로 변경 
3. 역노선  테이블-- 만들어야함.  

#### front.jsp
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SecondMarket - Local Secondhand Marketplace</title>
<meta name="description"
	content="Buy and sell used items locally using subway line locations">
<!--     <link rel="stylesheet" href="style.css"> -->
<style>
/* Basic Reset & Body */
body {
	margin: 0;
	font-family: sans-serif; /* A fallback for Inter font */
	min-height: 100vh;
	background-color: #f9fafb; /* bg-gray-50 */
}

.inter-font-class {
	/* If you want to use the Inter font, you would link it here */
	/* e.g., @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap'); */
	/* font-family: 'Inter', sans-serif; */
	
}

/* Container */
.container {
	max-width: 1200px; /* mx-auto, a common max-width */
	margin-left: auto;
	margin-right: auto;
	padding-left: 1rem; /* px-4 */
	padding-right: 1rem; /* px-4 */
}

/* Header */
header {
	border-bottom: 1px solid #e5e7eb; /* border-b */
	background-color: white;
	box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05); /* shadow-sm */
	padding-top: 1rem; /* py-4 */
	padding-bottom: 1rem; /* py-4 */
}

header .flex {
	display: flex;
	align-items: center; /* items-center */
	justify-content: space-between; /* justify-between */
}

header .text-2xl {
	font-size: 1.5rem; /* text-2xl */
	font-weight: 700; /* font-bold */
	color: #2563eb; /* text-blue-600 */
}

/* Search and Filters in Header */
header .space-x-4>*:not(:first-child) {
	margin-left: 1rem; /* space-x-4 */
}

header .flex-1 {
	flex: 1;
}

header .max-w-2xl {
	max-width: 42rem; /* max-w-2xl */
}

header .mx-8 {
	margin-left: 2rem; /* mx-8 */
	margin-right: 2rem; /* mx-8 */
}

header .relative {
	position: relative;
}

header .search-input {
	width: 100%;
	padding: 0.5rem 1rem 0.5rem 2.5rem; /* pl-10 */
	border: 1px solid #d1d5db; /* border */
	border-radius: 0.375rem; /* rounded-md */
	box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05); /* shadow-sm */
	outline: none;
}

header .search-input:focus {
	border-color: #60a5fa; /* focus:border-blue-500 */
	box-shadow: 0 0 0 3px rgba(96, 165, 250, 0.5);
	/* focus:ring-blue-200 */
}

header .absolute {
	position: absolute;
}

header .left-3 {
	left: 0.75rem;
}

header .top-1_2 {
	top: 50%;
}

header .transform {
	transform: translateY(-50%);
}

header .text-gray-400 {
	color: #9ca3af;
}

header .h-4 {
	height: 1rem;
}

header .w-4 {
	width: 1rem;
}

header .subway-line-select {
	width: 8rem; /* w-32 */
	padding: 0.5rem 1rem;
	border: 1px solid #d1d5db;
	border-radius: 0.375rem;
	background-color: white;
	box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
	appearance: none; /* Remove default select arrow */
	background-image:
		url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24' viewBox='0 0 24 24' fill='none' stroke='currentColor' stroke-width='2' stroke-linecap='round' stroke-linejoin='round' class='lucide lucide-chevron-down'%3E%3Cpath d='m6 9 6 6 6-6'%3E%3C/path%3E%3C/svg%3E");
	/* Custom arrow */
	background-repeat: no-repeat;
	background-position: right 0.75rem center;
	background-size: 1em;
}

/* Buttons */
.button {
	display: inline-flex;
	align-items: center;
	justify-content: center;
	padding: 0.5rem 1rem;
	font-weight: 500;
	border-radius: 0.375rem;
	cursor: pointer;
	transition: background-color 0.2s ease-in-out, border-color 0.2s
		ease-in-out;
}

.button.outline {
	background-color: white;
	border: 1px solid #d1d5db; /* border */
	color: #374151; /* text-gray-800 */
}

.button.outline:hover {
	background-color: #f3f4f6; /* hover:bg-gray-50 */
}

.button.ghost {
	background-color: transparent;
	border: none;
	color: #374151; /* text-gray-800 */
}

.button.ghost:hover {
	background-color: #f3f4f6; /* hover:bg-gray-50 */
}

.button.small {
	padding: 0.25rem 0.75rem; /* size="sm" */
}

.button svg.mr-2 {
	margin-right: 0.5rem;
}

/* Dropdown Menu */
.dropdown-menu {
	position: relative;
	display: inline-block;
}

.dropdown-content {
	display: none;
	position: absolute;
	background-color: white;
	min-width: 160px;
	box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
	z-index: 1;
	border-radius: 0.375rem;
	right: 0; /* align="end" */
	padding: 0.5rem 0;
}

.dropdown-content .dropdown-item {
	color: black;
	padding: 0.5rem 1rem;
	text-decoration: none;
	display: block;
}

.dropdown-content .dropdown-item:hover {
	background-color: #f3f4f6;
}

.dropdown-menu.active .dropdown-content {
	display: block;
}

/* Main Content */
main {
	padding-top: 2rem; /* py-8 */
	padding-bottom: 2rem; /* py-8 */
}

main .flex.gap-8 {
	display: flex;
	gap: 2rem; /* gap-8 */
}

main .flex-shrink-0 {
	flex-shrink: 0;
}

main .flex-1 {
	flex: 1;
}

main .mb-6 {
	margin-bottom: 1.5rem;
}

main .text-2xl {
	font-size: 1.5rem; /* text-2xl */
}

main .font-bold {
	font-weight: 700;
}

main .mb-2 {
	margin-bottom: 0.5rem;
}

main .text-gray-600 {
	color: #4b5563;
}

/* Product Grid */
.product-grid {
	display: grid;
	grid-template-columns: repeat(1, minmax(0, 1fr)); /* grid-cols-1 */
	gap: 1.5rem; /* gap-6 */
}

@media ( min-width : 768px) { /* md */
	.product-grid {
		grid-template-columns: repeat(2, minmax(0, 1fr)); /* md:grid-cols-2 */
	}
}

@media ( min-width : 1024px) { /* lg */
	.product-grid {
		grid-template-columns: repeat(3, minmax(0, 1fr)); /* lg:grid-cols-3 */
	}
}

@media ( min-width : 1280px) { /* xl */
	.product-grid {
		grid-template-columns: repeat(4, minmax(0, 1fr)); /* xl:grid-cols-4 */
	}
}

/* Product Card */
.product-card {
	background-color: white;
	border: 1px solid #e5e7eb;
	border-radius: 0.5rem; /* rounded-lg */
	overflow: hidden;
	box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0
		rgba(0, 0, 0, 0.06); /* shadow-md */
	display: flex;
	flex-direction: column;
}

.product-card-image {
	width: 100%;
	height: 180px; /* object-cover, h-48 */
	object-fit: cover;
}

.product-card-content {
	padding: 1rem; /* p-4 */
	flex-grow: 1;
	display: flex;
	flex-direction: column;
}

.product-card-title {
	font-weight: 600; /* font-semibold */
	font-size: 1.125rem; /* text-lg */
	margin-bottom: 0.5rem; /* mb-2 */
	line-height: 1.25; /* leading-tight */
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}

.product-card-price {
	font-weight: 700; /* font-bold */
	font-size: 1.25rem; /* text-xl */
	color: #1f2937; /* text-gray-900 */
	margin-bottom: 0.5rem; /* mb-2 */
}

.product-card-location {
	display: flex;
	align-items: center;
	color: #6b7280; /* text-gray-500 */
	font-size: 0.875rem; /* text-sm */
	margin-top: auto; /* Push to bottom */
}

.product-card-location svg {
	margin-right: 0.25rem; /* mr-1 */
	height: 1rem; /* h-4 */
	width: 1rem; /* w-4 */
}

/* Product Filters */
.product-filters {
	background-color: white;
	border: 1px solid #e5e7eb;
	border-radius: 0.5rem; /* rounded-lg */
	padding: 1.5rem; /* p-6 */
	width: 250px; /* fixed width for sidebar */
	box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0
		rgba(0, 0, 0, 0.06);
}

.product-filters h3 {
	font-size: 1.125rem; /* text-lg */
	font-weight: 600; /* font-semibold */
	margin-bottom: 1rem; /* mb-4 */
	color: #1f2937;
}

.product-filters .filter-group {
	margin-bottom: 1.5rem; /* mb-6 */
}

.product-filters .filter-group label {
	display: block;
	font-weight: 500; /* font-medium */
	margin-bottom: 0.5rem; /* mb-2 */
	color: #374151;
}

.product-filters .filter-group select, .product-filters .filter-group input[type="range"]
	{
	width: 100%;
	padding: 0.5rem;
	border: 1px solid #d1d5db;
	border-radius: 0.375rem;
	box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
}

.product-filters .filter-group .range-value {
	font-size: 0.875rem;
	color: #6b7280;
	margin-top: 0.25rem;
}

/* Toaster (Toast Notifications) */
#toaster-container {
	position: fixed;
	top: 1rem;
	right: 1rem;
	z-index: 1000;
}

.toast {
	background-color: #333;
	color: white;
	padding: 0.75rem 1.25rem;
	border-radius: 0.375rem;
	margin-bottom: 0.5rem;
	opacity: 0;
	transition: opacity 0.3s ease-in-out;
}

.toast.show {
	opacity: 1;
}
</style>
</head>
<body class="inter-font-class">
	<header class="border-b bg-white shadow-sm">
		<div class="container mx-auto px-4 py-4">
			<div class="flex items-center justify-between">
				<a href="/" class="text-2xl font-bold text-blue-600">SecondMarket</a>
				<div class="flex items-center space-x-4 flex-1 max-w-2xl mx-8">
					<div class="relative flex-1">
						<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
							viewBox="0 0 24 24" fill="none" stroke="currentColor"
							stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
							class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 h-4 w-4">
							<circle cx="11" cy="11" r="8"></circle>
							<path d="m21 21-4.3-4.3"></path></svg>
						<input type="text" placeholder="상품명으로 검색..."
							class="search-input pl-10">
					</div>
					<select class="subway-line-select w-32">
						<option value="all">전체</option>
					</select>
				</div>
				<div class="flex items-center space-x-4">
					<a href="/register">
						<button class="button outline small">
							<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
								viewBox="0 0 24 24" fill="none" stroke="currentColor"
								stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
								class="h-4 w-4 mr-2">
								<path d="M12 5v14"></path>
								<path d="M5 12h14"></path></svg>
							판매하기
						</button>
					</a> <a href="/favorites">
						<button class="button ghost small">
							<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
								viewBox="0 0 24 24" fill="none" stroke="currentColor"
								stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
								class="h-4 w-4">
								<path
									d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"></path></svg>
						</button>
					</a> <a href="/chat">
						<button class="button ghost small">
							<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
								viewBox="0 0 24 24" fill="none" stroke="currentColor"
								stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
								class="h-4 w-4">
								<path d="M7.9 20A9 9 0 1 0 4 16.1L2 22Z"></path></svg>
						</button>
					</a>
					<div class="dropdown-menu">
						<button class="button ghost small dropdown-trigger">
							<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24"
								viewBox="0 0 24 24" fill="none" stroke="currentColor"
								stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
								class="h-4 w-4">
								<path d="M19 21v-2a4 4 0 0 0-4-4H9a4 4 0 0 0-4 4v2"></path>
								<circle cx="12" cy="7" r="4"></circle></svg>
						</button>
						<div class="dropdown-content">
							<a href="/mypage" class="dropdown-item">마이페이지</a> <a
								href="/login" class="dropdown-item">로그인</a>
						</div>
					</div>
				</div>
			</div>
		</div>
	</header>

	<main class="container mx-auto px-4 py-8">
		<div class="flex gap-8">
			<aside class="flex-shrink-0">
				<div class="product-filters"></div>
			</aside>
			<div class="flex-1">
				<div class="mb-6">
					<h1 class="text-2xl font-bold mb-2">최근 등록된 상품</h1>
					<p class="text-gray-600">지하철역 기반으로 가까운 상품을 찾아보세요</p>
				</div>
				<div
					class="product-grid grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
				</div>
			</div>
		</div>
	</main>

	<div id="toaster-container"></div>

	<script src="script.js"></script>
</body>
</html>
```


[https://www.toptal.com/developers/gitignore](https://www.toptal.com/developers/gitignore)
깃 이그노어:   java , Eclisps, meaven 작업후 저장하기 .