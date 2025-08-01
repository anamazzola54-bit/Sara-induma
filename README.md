<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sara Induma</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #fff0f2;
      text-align: center;
    }
    header {
      background-color: #f9d2dc;
      padding: 20px;
      position: relative;
    }
    header img {
      position: absolute;
      top: 10px;
      left: 10px;
      height: 60px;
    }
    header h1 {
      font-size: 40px;
      margin: 0;
    }
    .subtitle {
      background-color: #ffdce5;
      padding: 10px;
      font-size: 20px;
    }
    nav {
      background-color: #f5a8bb;
      padding: 10px;
    }
    nav button {
      margin: 5px;
      padding: 10px 20px;
      background-color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
    .cart-button {
      position: absolute;
      top: 20px;
      right: 20px;
      background: none;
      border: none;
      font-size: 24px;
      cursor: pointer;
    }
    .section {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      margin: 20px;
    }
    .product {
      border: 1px solid #ccc;
      border-radius: 10px;
      padding: 15px;
      margin: 10px;
      width: 200px;
      background-color: white;
    }
    form {
      margin: 20px auto;
      padding: 20px;
      background: #fff;
      border-radius: 10px;
      width: 300px;
      display: none;
    }
    form input, form select {
      margin: 10px 0;
      padding: 8px;
      width: 100%;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    #cart {
      display: none;
      background-color: #fff;
      padding: 20px;
      margin: 20px;
      border-radius: 10px;
    }
  </style>
</head>
<body>
  <header>
    <img src="https://chat.openai.com/share/logo.jpg" alt="Logo">
    <h1>Sara Induma</h1>
    <button class="cart-button" onclick="toggleCart()">🛒</button>
  </header>
  <div class="subtitle">Ropa confiable siempre</div>
  <nav>
    <button onclick="showSection('polleras')">Polleras</button>
    <button onclick="showSection('vestidos')">Vestidos</button>
    <button onclick="toggleInfo()">Info</button>
    <button onclick="pedirContraseña()">Agregar prenda</button>
  </nav>

  <div id="info" style="display:none; margin:20px;">
    <h3>Envíos:</h3>
    <p>Vía Cargo, OCA y Correo Argentino</p>
    <h3>Cómo pagar:</h3>
    <p>Contactarse al 1123456789</p>
  </div>

  <div class="section" id="polleras" style="display:none;"></div>
  <div class="section" id="vestidos" style="display:none;"></div>

  <form id="formulario">
    <h3>Cargar Producto</h3>
    <input type="text" id="nombre" placeholder="Nombre">
    <input type="text" id="imagen" placeholder="URL de imagen">
    <select id="categoria">
      <option value="polleras">Pollera</option>
      <option value="vestidos">Vestido</option>
    </select>
    <input type="text" id="talles" placeholder="Talles (ej: S,M,L)">
    <input type="text" id="colores" placeholder="Colores (ej: rojo, azul)">
    <input type="number" id="precio" placeholder="Precio">
    <button type="button" onclick="agregarProducto()">Agregar</button>
  </form>

  <div id="cart"></div>

  <script>
    let carrito = [];

    function showSection(seccion) {
      document.getElementById('polleras').style.display = 'none';
      document.getElementById('vestidos').style.display = 'none';
      document.getElementById(seccion).style.display = 'flex';
    }

    function toggleInfo() {
      const info = document.getElementById('info');
      info.style.display = info.style.display === 'none' ? 'block' : 'none';
    }

    function pedirContraseña() {
      const pass = prompt("Contraseña para agregar prenda:");
      if (pass === "1415") {
        document.getElementById('formulario').style.display = 'block';
      } else {
        alert("Contraseña incorrecta.");
      }
    }

    function agregarProducto() {
      const nombre = document.getElementById('nombre').value;
      const imagen = document.getElementById('imagen').value;
      const categoria = document.getElementById('categoria').value;
      const talles = document.getElementById('talles').value;
      const colores = document.getElementById('colores').value;
      const precio = parseFloat(document.getElementById('precio').value);

      const div = document.createElement('div');
      div.className = 'product';
      div.innerHTML = `
        <img src="${imagen}" alt="${nombre}" style="width:100%; height:150px; object-fit:cover;"><br>
        <strong>${nombre}</strong><br>
        Talles: ${talles}<br>
        Colores: ${colores}<br>
        Precio: $${precio}<br>
        <button onclick="agregarAlCarrito('${nombre}', ${precio})">Agregar al carrito</button>
      `;
      document.getElementById(categoria).appendChild(div);
    }

    function agregarAlCarrito(nombre, precio) {
      const cantidad = prompt("¿Cuántos querés?");
      if (!cantidad || isNaN(cantidad) || cantidad <= 0) return;
      carrito.push({ nombre, precio, cantidad: parseInt(cantidad) });
      alert("Producto agregado al carrito");
    }

    function toggleCart() {
      const cart = document.getElementById('cart');
      if (cart.style.display === 'none') {
        let html = '<h2>Carrito</h2>';
        let total = 0;
        carrito.forEach(item => {
          html += `<p>${item.nombre} x${item.cantidad} - $${item.precio * item.cantidad}</p>`;
          total += item.precio * item.cantidad;
        });
        html += `<h3>Total: $${total}</h3>`;
        cart.innerHTML = html;
        cart.style.display = 'block';
      } else {
        cart.style.display = 'none';
      }
    }
  </script>
</body>
</html>
