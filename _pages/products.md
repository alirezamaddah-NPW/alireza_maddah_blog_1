---
permalink: /products/
title: "محصولات"
---

<div class="products" dir="rtl">
  <p>به صفحه محصولات ما خوش آمدید. در اینجا می‌توانید ۱۹ محصول برتر ما را مشاهده کنید. هر محصول با توضیحات مختصر ارائه شده است.</p>
  
  <div class="product-grid">
    {% for product in site.data.products %}
    <div class="product-item">
      <img src="{{ site.baseurl }}/assets/images/{{ product.image }}" alt="{{ product.alt }}">
      <p class="caption">محصول {{ forloop.index }}: {{ product.description }}</p>
    </div>
    {% endfor %}
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
    grid-template-columns: repeat(3, 1fr); /* Change to 3 columns */
    gap: 2.0rem;
    margin-top: 2rem;
  }

  .product-item {
    text-align: center; /* Center-align the content inside the product item */
  }

  .product-item img {
    width: 100%; /* Ensure the image takes full width of the container */
    max-width: 400px; /* Set a maximum width to avoid overly large images */
    height: auto; /* Maintain aspect ratio */
    object-fit: contain; /* Ensures the entire image is visible without cropping */
    margin: 0 auto; /* Center the image horizontally */
    background-color: #f9f9f9; /* Optional: Adds a subtle background */
    border: 1px solid #ddd;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .caption {
    margin-top: 0.5rem;
    font-size: 0.9rem;
    color: #555;
    text-align: center; /* Center-align the caption under the image */
  }
</style>

<script>
  // Function to convert English numbers to Persian
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
  });
</script>