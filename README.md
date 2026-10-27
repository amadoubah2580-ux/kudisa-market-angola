# kudisa-market-angola
Market place en Angola : alimentation, construction, téléphones et autres produits.
<!DOCTYPE html>

<html lang="fr">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1">

<meta name="theme-color" content="#087443">

<title>Kudisa Market Angola</title>

<style>

:root{--green:#087443;--light:#f3f6f4}

*{box-sizing:border-box}

body{margin:0;font-family:Arial,sans-serif;background:var(--light);color:#202820}

header{background:var(--green);color:white;padding:24px 16px;text-align:center}

header h1{margin:0;font-size:30px}

header p{margin:8px 0 0}

main{max-width:1000px;margin:auto;padding:16px}

h2{font-size:22px}

.search{width:100%;padding:13px;border:1px solid #ccc;border-radius:10px;font-size:16px}

.categories{display:flex;gap:8px;overflow-x:auto;padding:12px 0}

.categories button{border:1px solid #d4ded7;background:white;padding:10px 13px;border-radius:20px;white-space:nowrap}

.categories button.active{background:var(--green);color:white}

.products{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px}

.card{background:white;border-radius:12px;overflow:hidden;box-shadow:0 2px 7px #00000012}

.card img{width:100%;height:135px;object-fit:cover;display:block;background:#e4e9e5}

.details{padding:11px}

.details h3{font-size:16px;margin:0 0 7px}

.price{font-size:17px;font-weight:bold;color:var(--green);margin:8px 0}

.note{font-size:12px;color:#666;margin:5px 0 10px}

.action{display:block;text-align:center;text-decoration:none;color:white;padding:10px 5px;border-radius:8px;margin-top:7px;font-size:13px;font-weight:bold}

.whatsapp{background:#16864a}

.call{background:#244c39}

footer{text-align:center;padding:25px 12px;color:#555;font-size:13px}

@media(min-width:650px){.products{grid-template-columns:repeat(3,minmax(0,1fr))}.card img{height:190px}}

</style>

</head>

<body>

<header>

  <h1>🛍️ Kudisa Market</h1>

  <p>Achetez et vendez facilement en Angola</p>

  <p>Alimentation · Construction · Téléphones · Maison</p>

</header>

<main>

  <h2>Découvrez nos produits</h2>

  <input class="search" id="search" placeholder="🔎 Rechercher un produit..." aria-label="Rechercher un produit">

  <div class="categories" id="categories">

    <button class="active" data-category="Tous">Tout</button>

    <button data-category="Alimentation">🥬 Alimentation</button>

    <button data-category="Construction">🧱 Construction</button>

    <button data-category="Téléphones">📱 Téléphones</button>

    <button data-category="Vêtements">👕 Vêtements</button>

    <button data-category="Maison">🪑 Maison</button>

  </div>

  <div class="products" id="products"></div>

  <p class="note">Les prix et produits ci-dessous sont des exemples. Confirmez le prix et la disponibilité avec le vendeur.</p>

</main>

<footer>

  Kudisa Market Angola © 2026<br>

  Commandes par WhatsApp ou téléphone

</footer>

<script>

const phone = "244975219390";

const products = [

  {

    name:"Légumes frais",

    category:"Alimentation",

    price:2500,

    unit:"lot",

    image:"https://images.unsplash.com/photo-1540420773420-3366772f4999?auto=format&fit=crop&w=600&q=80"

  },

  {

    name:"Sac de ciment",

    category:"Construction",

    price:6500,

    unit:"sac",

    image:"https://images.unsplash.com/photo-1513467655676-561b7d489a88?auto=format&fit=crop&w=600&q=80"

  },

  {

    name:"Téléphone portable",

    category:"Téléphones",

    price:85000,

    unit:"unité",

    image:"https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?auto=format&fit=crop&w=600&q=80"

  },

  {

    name:"T-shirt",

    category:"Vêtements",

    price:7000,

    unit:"unité",

    image:"https://images.unsplash.com/photo-1521572163474-6864f9cf17ab?auto=format&fit=crop&w=600&q=80"

  },

  {

    name:"Chaise de maison",

    category:"Maison",

    price:18000,

    unit:"unité",

    image:"https://images.unsplash.com/photo-1503602642458-232111445657?auto=format&fit=crop&w=600&q=80"

  },

  {

    name:"Riz",

    category:"Alimentation",

    price:12000,

    unit:"sac",

    image:"https://images.unsplash.com/photo-1586201375761-83865001e31c?auto=format&fit=crop&w=600&q=80"

  }

];

let selectedCategory = "Tous";

function renderProducts(){

  const query = document.getElementById("search").value.toLowerCase().trim();

  const list = products.filter(p =>

    (selectedCategory === "Tous" || p.category === selectedCategory) &&

    p.name.toLowerCase().includes(query)

  );

  document.getElementById("products").innerHTML = list.length

    ? list.map((p) => {

      const message = encodeURIComponent(

        "Bonjour Kudisa Market, je souhaite commander : " + p.name +

        ". Prix affiché : " + p.price.toLocaleString("fr-FR") +

        " Kz par " + p.unit + ". Est-ce disponible ?"

      );

      return `

        <article class="card">

          <img src="${p.image}" alt="${p.name}" loading="lazy">

          <div class="details">

            <h3>${p.name}</h3>

            <div>${p.category}</div>

            <div class="price">${p.price.toLocaleString("fr-FR")} Kz</div>

            <div class="note">Prix d'exemple · par ${p.unit}</div>

            <a class="action whatsapp" href="https://wa.me/${phone}?text=${message}" target="_blank" rel="noopener">Commander WhatsApp</a>

            <a class="action call" href="tel:+${phone}">📞 Appeler le vendeur</a>

          </div>

        </article>`;

    }).join("")

    : "<p>Aucun produit trouvé. Essayez une autre recherche.</p>";

}

document.getElementById("search").addEventListener("input", renderProducts);

document.getElementById("categories").addEventListener("click", function(event){

  const button = event.target.closest("button[data-category]");

  if(!button) return;

  selectedCategory = button.dataset.category;

  document.querySelectorAll("#categories button").forEach(b =>

    b.classList.toggle("active", b === button)

  );

  renderProducts();

});

renderProducts();

</script>

</body>

</html>
