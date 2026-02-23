# Adv-prs-7
<!DOCTYPE html>
<html>
<head>
<title>Advanced Product Recommendation</title>
<style>
body{font-family:Arial;margin:0;background:#f2f4f8;}
header{background:#1e40af;color:white;padding:15px;text-align:center;}
.container{padding:20px;}
.controls{display:flex;flex-wrap:wrap;gap:10px;margin-bottom:15px;}
input,select{padding:8px;}
.filterBox{margin-bottom:15px;background:white;padding:10px;border-radius:8px;}
.products{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:20px;}
.card{background:white;padding:15px;border-radius:10px;box-shadow:0 0 8px rgba(0,0,0,0.1);}
.card img{width:100%;height:180px;object-fit:cover;border-radius:8px;}
.price{color:green;font-weight:bold;}
button{width:100%;padding:8px;background:#2563eb;color:white;border:none;border-radius:5px;cursor:pointer;}
button:hover{background:#1e3a8a;}
</style>
</head>
<body>

<header>
<h2>Smart Product Recommendation System</h2>
</header>

<div class="container">

<div class="controls">
<input type="text" id="search" placeholder="Search..." onkeyup="displayProducts()">

<select id="categoryFilter" onchange="displayProducts()">
<option value="All">All Categories</option>
<option value="Electronics">Electronics</option>
<option value="Beauty">Beauty</option>
<option value="Home">Home Appliances</option>
<option value="Sports">Sports</option>
<option value="Medicine">Medicine</option>
</select>
</div>

<div id="separateFilters" class="filterBox"></div>

<div class="products" id="productList"></div>

</div>

<script>

const products = [

/* Electronics */
{name:"iPhone 14",category:"Electronics",brand:"Apple",price:70000,image:"https://m.media-amazon.com/images/I/61bK6PMOC3L._SL1500_.jpg",link:"https://www.amazon.in/"},
{name:"Samsung Galaxy S23",category:"Electronics",brand:"Samsung",price:65000,image:"https://m.media-amazon.com/images/I/71goZuIha-L._SL1500_.jpg",link:"https://www.amazon.in/"},
{name:"HP Laptop",category:"Electronics",brand:"HP",price:50000,image:"https://m.media-amazon.com/images/I/71vFKBpKakL._SL1500_.jpg",link:"https://www.amazon.in/"},

/* Beauty */
{name:"Lakme Face Cream",category:"Beauty",brand:"Lakme",skin:"Dry",price:299,image:"https://m.media-amazon.com/images/I/61X6LxFhPZL._SL1500_.jpg",link:"https://www.amazon.in/"},
{name:"Dove Shampoo",category:"Beauty",brand:"Dove",skin:"Oily",price:350,image:"https://m.media-amazon.com/images/I/61W0u5t1MFL._SL1500_.jpg",link:"https://www.amazon.in/"},

/* Home */
{name:"LG Refrigerator",category:"Home",brand:"LG",price:25000,image:"https://m.media-amazon.com/images/I/61z6f9XJ5HL._SL1500_.jpg",link:"https://www.amazon.in/"},
{name:"IFB Washing Machine",category:"Home",brand:"IFB",price:18000,image:"https://m.media-amazon.com/images/I/71Vn1bR3vOL._SL1500_.jpg",link:"https://www.amazon.in/"},

/* Sports */
{name:"Cosco Football",category:"Sports",brand:"Cosco",price:799,image:"https://m.media-amazon.com/images/I/71Qd4+3xR-L._SL1500_.jpg",link:"https://www.amazon.in/"},
{name:"Yonex Racket",category:"Sports",brand:"Yonex",price:1500,image:"https://m.media-amazon.com/images/I/61F6L9t6pQL._SL1500_.jpg",link:"https://www.amazon.in/"},

/* Medicine */
{name:"Dolo 650",category:"Medicine",type:"Tablet",price:30,image:"https://m.media-amazon.com/images/I/51vN6R9xTQL._SL1000_.jpg",link:"https://www.amazon.in/"},
{name:"Vitamin C Syrup",category:"Medicine",type:"Syrup",price:120,image:"https://m.media-amazon.com/images/I/61nJf7pPZAL._SL1500_.jpg",link:"https://www.amazon.in/"}
];

function displayProducts(){

const search=document.getElementById("search").value.toLowerCase();
const category=document.getElementById("categoryFilter").value;
const filterBox=document.getElementById("separateFilters");

filterBox.innerHTML="";

/* Show Separate Filters */

if(category==="Electronics"){
filterBox.innerHTML=`
<b>Electronics Filters:</b>
<select id="brandFilter" onchange="displayProducts()">
<option value="All">All Brands</option>
<option value="Apple">Apple</option>
<option value="Samsung">Samsung</option>
<option value="HP">HP</option>
</select>
`;
}

if(category==="Beauty"){
filterBox.innerHTML=`
<b>Beauty Filters:</b>
<select id="skinFilter" onchange="displayProducts()">
<option value="All">All Skin Type</option>
<option value="Dry">Dry</option>
<option value="Oily">Oily</option>
</select>
`;
}

if(category==="Medicine"){
filterBox.innerHTML=`
<b>Medicine Filters:</b>
<select id="typeFilter" onchange="displayProducts()">
<option value="All">All Type</option>
<option value="Tablet">Tablet</option>
<option value="Syrup">Syrup</option>
</select>
`;
}

/* Filtering Logic */

let filtered=products.filter(product=>{

let matchSearch=product.name.toLowerCase().includes(search);
let matchCategory=category==="All"||product.category===category;
let matchDynamic=true;

if(document.getElementById("brandFilter")){
let brand=document.getElementById("brandFilter").value;
if(brand!=="All") matchDynamic=product.brand===brand;
}

if(document.getElementById("skinFilter")){
let skin=document.getElementById("skinFilter").value;
if(skin!=="All") matchDynamic=product.skin===skin;
}

if(document.getElementById("typeFilter")){
let type=document.getElementById("typeFilter").value;
if(type!=="All") matchDynamic=product.type===type;
}

return matchSearch&&matchCategory&&matchDynamic;

});

const productList=document.getElementById("productList");
productList.innerHTML="";

filtered.forEach(product=>{
productList.innerHTML+=`
<div class="card">
<img src="${product.image}">
<h3>${product.name}</h3>
<p class="price">₹${product.price}</p>
<a href="${product.link}" target="_blank">
<button>Buy Now</button>
</a>
</div>
`;
});

}

displayProducts();

</script>

</body>
</html>
