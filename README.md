
<style>
.farshad {
  background:#030916;
  color:#fff;
  overflow:hidden;
  font-family:Arial,sans-serif;
}
.farshad * {box-sizing:border-box}
.farshad-hero {
  min-height:580px;
  position:relative;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  text-align:center;
  padding:75px 20px;
  isolation:isolate;
  background:
    radial-gradient(ellipse at 50% 55%,#063c78 0%,#071a37 35%,#030916 75%);
}
.farshad-hero:before {
  content:"";
  position:absolute;
  width:330px;height:330px;
  border-radius:50%;
  background:linear-gradient(130deg,#fff,#00aaff 25%,#063b9e 55%,#75eaff 75%,#07152c);
  box-shadow:0 0 65px #008cff88, inset -22px -25px 50px #00112e;
  filter:blur(.3px);
  z-index:-1;
  opacity:.85;
  animation:farshadFloat 7s ease-in-out infinite;
}
.farshad-hero:after {
  content:"";
  position:absolute;
  width:440px;height:440px;
  border:1px solid #48baff55;
  border-radius:50%;
  transform:rotateX(70deg);
  box-shadow:0 0 30px #009dff55;
  z-index:-1;
}
.farshad-eyebrow {
  letter-spacing:5px;
  color:#8bdcff;
  font-size:11px;
  font-weight:bold;
}
.farshad-hero h1 {
  font-size:clamp(43px,10vw,90px);
  line-height:.95;
  letter-spacing:-5px;
  margin:24px 0;
  font-weight:900;
  text-shadow:0 4px 30px #009dff88;
}
.farshad-hero h1 span {
  color:transparent;
  -webkit-text-stroke:1px #a9e7ff;
}
.farshad-hero p {
  color:#c2d8ee;
  max-width:430px;
  line-height:1.8;
  font-size:14px;
}
.farshad-btn {
  display:inline-block;
  padding:16px 29px;
  border-radius:40px;
  margin-top:20px;
  background:linear-gradient(110deg,#007bff,#54d8ff);
  color:#001126!important;
  text-decoration:none!important;
  font-size:12px;
  font-weight:900;
  letter-spacing:2px;
  box-shadow:0 0 30px #008dff66;
  transition:.3s;
}
.farshad-btn:hover {
  transform:translateY(-5px) scale(1.04);
  box-shadow:0 0 45px #009dff;
}
.farshad-section {
  padding:55px 18px;
  max-width:1200px;
  margin:auto;
}
.farshad-heading {
  text-align:center;
  font-size:clamp(25px,5vw,40px);
  letter-spacing:-1px;
}
.farshad-sub {
  color:#81a9ce;
  text-align:center;
  font-size:13px;
  margin:12px 0 35px;
}
.farshad-grid {
  display:grid;
  grid-template-columns:repeat(2,minmax(0,1fr));
  gap:14px;
}
.farshad-card {
  min-width:0;
  padding:10px;
  border:1px solid #3986c944;
  border-radius:17px;
  background:linear-gradient(145deg,#102945aa,#071222dd);
  transition:transform .25s,border-color .25s;
}
.farshad-card:hover {
  transform:translateY(-6px);
  border-color:#42bfff;
}
.farshad-card img {
  display:block;
  width:100%;
  aspect-ratio:1/1;
  object-fit:contain;
  border-radius:12px;
  background:#10243c;
}
.farshad-card h3 {
  font-size:14px;
  line-height:1.4;
  margin:14px 0 8px;
}
.farshad-price {
  color:#72caff;
  font-weight:bold;
  font-size:14px;
}
.farshad-buy {
  display:block;
  text-align:center;
  margin-top:13px;
  padding:12px 5px;
  border:1px solid #36aaff;
  border-radius:9px;
  color:#fff!important;
  text-decoration:none!important;
  font-size:11px;
  font-weight:bold;
  letter-spacing:1px;
}
.farshad-buy:hover {background:#087edb}
.farshad-footer {
  text-align:center;
  border-top:1px solid #17416a;
  padding:35px 15px;
  color:#8eacc8;
  font-size:12px;
}
@keyframes farshadFloat {
  0%,100% {transform:translateY(0) rotate(0deg)}
  50% {transform:translateY(-22px) rotate(12deg)}
}
@media(min-width:750px) {
  .farshad-grid {grid-template-columns:repeat(4,minmax(0,1fr));gap:20px}
  .farshad-hero {min-height:690px}
}
@media(prefers-reduced-motion:reduce) {
  .farshad-hero:before {animation:none}
  .farshad-card,.farshad-btn {transition:none}
}
</style>

<div class="farshad">
  <section class="farshad-hero">
    <div class="farshad-eyebrow">WELCOME TO THE NEXT DIMENSION</div>
    <h1>FARSHAD<br><span>FUTURE.</span></h1>
    <p>Discover the next generation of technology, style and innovation. Your future shopping experience starts here.</p>
    <a class="farshad-btn" href="/collections/all">EXPLORE COLLECTION</a>
  </section>

  <section class="farshad-section">
    <h2 class="farshad-heading">THE FUTURE COLLECTION</h2>
    <p class="farshad-sub">Handpicked technology. Extraordinary experiences.</p>

    <div class="farshad-grid">
      {% for product in collections.all.products limit:8 %}
        <article class="farshad-card">
          <a href="{{ product.url }}">
            {% if product.featured_image %}
              <img
                src="{{ product.featured_image | image_url: width: 600 }}"
                alt="{{ product.featured_image.alt | escape }}"
                loading="lazy"
                width="600"
                height="600">
            {% endif %}
          </a>
          <h3>{{ product.title | escape }}</h3>
          <div class="farshad-price">{{ product.price | money }}</div>
          <a class="farshad-buy" href="{{ product.url }}">DISCOVER PRODUCT</a>
          {% if product.available %}
            <form action="/cart/add" method="post">
              <input type="hidden" name="id" value="{{ product.selected_or_first_available_variant.id }}">
              <input type="hidden" name="quantity" value="1">
              <button class="farshad-buy" type="submit" style="width:100%;background:#087edb;cursor:pointer">ADD TO CART</button>
            </form>
          {% endif %}
        </article>
      {% else %}
        <p>Our collection is arriving soon. Stay tuned.</p>
      {% endfor %}
    </div>
  </section>

  <section class="farshad-section" style="text-align:center">
    <h2 class="farshad-heading">NOT JUST SHOPPING.</h2>
    <h2 class="farshad-heading" style="color:#4abfff">AN EXPERIENCE.</h2>
    <p class="farshad-sub">Welcome to a world without limits.</p>
    <a class="farshad-btn" href="/collections/all">SHOP FARSHAD</a>
  </section>

  <footer class="farshad-footer">
    FARSHAD © {{ 'now' | date: '%Y' }}<br>
    BEYOND ORDINARY. BEYOND LIMITS.
  </footer>
</div>
