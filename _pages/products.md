---
permalink: /products/
title: "محصولات"
---

<div class="products" dir="rtl">
  <p>به صفحه محصولات ما خوش آمدید. در اینجا می‌توانید ۱۹ محصول برتر ما را مشاهده کنید. هر محصول با توضیحات مختصر ارائه شده است.</p>
  
  <div class="product-grid">
    {% for product in site.data.products %}
    <div class="product-item">
      <img class="product-img" src="{{ site.baseurl }}/assets/images/{{ product.image }}" alt="{{ product.alt }}" tabindex="0">
      <p class="caption">محصول {{ forloop.index }}: {{ product.description }}</p>
    </div>
    {% endfor %}
  </div>
</div>

<!-- Popup Modal for Image Preview -->
<div id="image-modal" class="image-modal" tabindex="-1" aria-hidden="true">
  <div class="modal-content">
    <button class="close-modal" aria-label="بستن">&times;</button>
    <img id="modal-img" src="" alt="">
  </div>
</div>

<style>
.products {
  text-align: right;
  margin: 2rem auto;
  font-family: Arial, sans-serif;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2.0rem;
  margin-top: 2rem;
}

.product-item {
  text-align: center;
}

.product-item img {
  width: 100%;
  max-width: 400px;
  height: auto;
  object-fit: contain;
  margin: 0 auto;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  cursor: zoom-in;
  transition: box-shadow .2s;
}
.product-item img:focus {
  outline: 2px solid #0078d7;
  box-shadow: 0 0 0 4px #0078d755;
}

.caption {
  margin-top: 0.5rem;
  font-size: 0.9rem;
  color: #555;
  text-align: center;
}

/* Modal Styles */
.image-modal {
  display: none;
  position: fixed;
  z-index: 9999;
  left: 0; top: 0;
  width: 100vw; height: 100vh;
  background: rgba(0,0,0,0.8);
  justify-content: center;
  align-items: center;
  transition: opacity 0.2s;
}
.image-modal.active {
  display: flex;
  animation: fadeIn .2s;
}
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

.image-modal .modal-content {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  background: transparent;
  border-radius: 12px;
  padding: 0;
  box-shadow: 0 6px 24px rgba(0,0,0,.3);
  max-width: 90vw;
  max-height: 90vh;
}

#modal-img {
  max-width: 90vw;
  max-height: 80vh;
  border-radius: 8px;
  background: #fff;
  box-shadow: 0 4px 10px rgba(0,0,0,0.2);
  object-fit: contain;
  display: block;
}

/* Close button inside modal-content, top-right of image */
.close-modal {
  position: absolute;
  top: 8px;
  right: 8px;
  background: #fff;
  color: #222;
  border: none;
  border-radius: 50%;
  width: 36px; height: 36px;
  font-size: 2rem;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
  z-index: 2;
  transition: background .1s;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
}
.close-modal:hover,
.close-modal:focus {
  background: #f2f2f2;
  outline: 2px solid #0078d7;
}

/* Responsive grid for mobile/tablet */
@media (max-width: 900px) {
  .product-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media (max-width: 600px) {
  .product-grid {
    grid-template-columns: 1fr;
  }
  .image-modal .modal-content {
    max-width: 98vw;
    max-height: 80vh;
  }
  #modal-img {
    max-width: 96vw;
    max-height: 65vh;
  }
}
</style>

<script>
// Convert English numbers to Persian
function toPersianNumber(num) {
  const persianDigits = ['۰', '۱', '۲', '۳', '۴', '۵', '۶', '۷', '۸', '۹'];
  return num.toString().replace(/\d/g, (digit) => persianDigits[digit]);
}

// Convert all captions with numbers
document.addEventListener("DOMContentLoaded", function () {
  const captions = document.querySelectorAll(".caption");
  captions.forEach((caption) => {
    caption.innerHTML = caption.innerHTML.replace(/\d+/g, (number) => toPersianNumber(number));
  });

  // Popup Image Modal Logic
  const modal = document.getElementById('image-modal');
  const modalImg = document.getElementById('modal-img');
  const closeBtn = document.querySelector('.close-modal');
  let lastFocusedElement = null;

  function openModal(src, alt) {
    modalImg.src = src;
    modalImg.alt = alt;
    modal.classList.add('active');
    modal.setAttribute('aria-hidden', 'false');
    lastFocusedElement = document.activeElement;
    closeBtn.focus();
    document.body.style.overflow = 'hidden';
  }

  function closeModal() {
    modal.classList.remove('active');
    modalImg.src = '';
    modalImg.alt = '';
    modal.setAttribute('aria-hidden', 'true');
    document.body.style.overflow = '';
    if (lastFocusedElement) lastFocusedElement.focus();
  }

  // Click/tap on image opens modal
  document.querySelectorAll('.product-img').forEach(img => {
    img.addEventListener('click', function () {
      openModal(this.src, this.alt);
    });
    // Keyboard accessibility: Enter/Space
    img.addEventListener('keydown', function (e) {
      if (e.key === "Enter" || e.key === " ") {
        e.preventDefault();
        openModal(this.src, this.alt);
      }
    });
  });

  // Close modal by button
  closeBtn.addEventListener('click', closeModal);

  // Close modal by clicking outside image (on the dark overlay)
  modal.addEventListener('click', function (e) {
    if (e.target === modal) closeModal();
  });

  // Close modal with Escape key
  window.addEventListener('keydown', function (e) {
    if (modal.classList.contains('active') && (e.key === "Escape" || e.key === "Esc")) {
      closeModal();
    }
  });
});
</script>