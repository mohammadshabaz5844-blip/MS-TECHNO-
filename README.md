<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MS TECHNO</title>

<style>
body{
margin:0;
font-family:Arial;
background:#f4f6f9;
}

header{
background:linear-gradient(135deg,#0b1f3a,#1e88e5);
color:white;
text-align:center;
padding:20px;
}

.logo{
font-size:28px;
font-weight:bold;
letter-spacing:2px;
}

.admin{
background:white;
margin:10px;
padding:15px;
border-radius:10px;
box-shadow:0 2px 10px rgba(0,0,0,.1);
}

input,button{
width:100%;
padding:10px;
margin-top:10px;
}

button{
background:#1e88e5;
color:white;
border:none;
border-radius:5px;
cursor:pointer;
}

.products{
display:grid;
grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
gap:15px;
padding:15px;
}

.card{
background:white;
border-radius:10px;
padding:10px;
text-align:center;
box-shadow:0 2px 10px rgba(0,0,0,.1);
}

.card img{
width:100%;
border-radius:10px;
}

.price{
color:#1e88e5;
font-weight:bold;
}

.btn{
display:inline-block;
margin-top:5px;
padding:8px;
background:#1e88e5;
color:white;
text-decoration:none;
border-radius:5px;
font-size:13px;
}

.btn-del{
background:red;
}

.btn-edit{
background:orange;
}
</style>
</head>

<body>

<header>
<div class="logo">MS TECHNO</div>
<p>Smart Business Store</p>
</header>

<!-- ADMIN PANEL -->
<div class="admin">
<h3>Add / Edit Product</h3>

<input type="text" id="name" placeholder="Product Name">
<input type="text" id="price" placeholder="Price (৳)">
<input type="file" id="image">

<button onclick="addProduct()">Add Product</button>
</div>

<!-- PRODUCTS -->
<div class="products" id="products"></div>

<!-- PAYMENT INFO -->
<div style="text-align:center;padding:20px;">
<h2>Payment Methods</h2>
<p>:contentReference[oaicite:2]{index=2} | :contentReference[oaicite:3]{index=3} | Cash on Delivery</p>
</div>

<script>

let products = JSON.parse(localStorage.getItem("msbiz")) || [];

window.onload = render;

function addProduct(){
let name = document.getElementById("name").value;
let price = document.getElementById("price").value;
let image = document.getElementById("image").files[0];

if(!name || !price || !image){
alert("সব ফিল্ড পূরণ করো");
return;
}

let reader = new FileReader();

reader.onload = function(e){

products.push({
name,
price,
image: e.target.result
});

save();
render();
};

reader.readAsDataURL(image);

document.getElementById("name").value="";
document.getElementById("price").value="";
document.getElementById("image").value="";
}

function deleteProduct(index){
products.splice(index,1);
save();
render();
}

function editProduct(index){
let p = products[index];

let newName = prompt("Edit Name", p.name);
let newPrice = prompt("Edit Price", p.price);

if(newName && newPrice){
products[index].name = newName;
products[index].price = newPrice;
save();
render();
}
}

function save(){
localStorage.setItem("msbiz", JSON.stringify(products));
}

function render(){

let box = document.getElementById("products");
box.innerHTML="";

products.forEach((p,index)=>{

box.innerHTML += `
<div class="card">
<img src="${p.image}">
<h3>${p.name}</h3>
<p class="price">৳${p.price}</p>

<a class="btn" href="https://wa.me/8801XXXXXXXXX">WhatsApp</a>
<a class="btn" href="https://m.me/yourpage">Messenger</a>

<br>

<button class="btn btn-edit" onclick="editProduct(${index})">Edit</button>
<button class="btn btn-del" onclick="deleteProduct(${index})">Delete</button>
</div>
`;

});

}

</script>

</body>
</html>
