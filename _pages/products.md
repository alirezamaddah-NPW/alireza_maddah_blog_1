---
permalink: /products/
title: "محصولات"
---

<div class="products" dir="rtl">
  <p>به صفحه محصولات ما خوش آمدید. در اینجا می‌توانید ۱۹ محصول برتر ما را مشاهده کنید. هر محصول با توضیحات مختصر ارائه شده است.</p>
  
  <div class="product-grid">
    {% for product in site.data.products %}
    <div class="product-item">
      <img src="{{ site.baseurl }}/assets/images/{{ product.image }}" alt="{{ product.alt }}" class="product-image" onclick="openModal('{{ site.baseurl }}/assets/images/{{ product.image }}', '{{ product.description }}')">
      <p class="caption" onclick="openModal('{{ site.baseurl }}/assets/images/{{ product.image }}', '{{ product.description }}')">محصول {{ forloop.index }}: {{ product.description }}</p>
    </div>
    {% endfor %}
  </div>
</div>

<!-- Modal for displaying enlarged image -->
<div id="imageModal" class="modal">
  <span class="close" onclick="closeModal()">&times;</span>
  <img class="modal-content" id="modalImage">
  <div id="modalCaption"></div>
</div>

<style>
  .products {
    text-align: right;
    margin: 2rem auto;
    font-family: Arial, sans-serif;
  }

  .product-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr); /* Two products per row */
    gap: 2.0rem;
    margin-top: 2rem;
  }

  .product-item {
    text-align: center; /* Center-align the content inside the product item */
  }

  .product-item img {
    width: 100%; /* Make the image as large as possible */
    max-width: 500px; /* Set a maximum width for the image */
    height: auto; /* Maintain aspect ratio */
    object-fit: cover; /* Ensure uniform image size */
    margin: 0 auto; /* Center the image horizontally */
    background-color: #f9f9f9; /* Optional: Adds a subtle background */
    border: 1px solid #ddd;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    cursor: pointer; /* Indicate the image is clickable */
  }

  .caption {
    margin-top: 0.5rem;
    font-size: 0.9rem;
    color: #555;
    text-align: center; /* Center-align the caption under the image */
    cursor: pointer; /* Indicate the caption is clickable */
  }

  /* Modal styles */
  .modal {
    display: none; /* Hidden by default */
    position: fixed; /* Stay in place */
    z-index: 1000; /* Sit on top */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    overflow: auto; /* Enable scroll if needed */
    background-color: rgba(0, 0, 0, 0.8); /* Black background with opacity */
  }

  .modal-content {
    margin: auto;
    display: block;
    max-width: 90%; /* Limit the size of the enlarged image */
    max-height: 90%; /* Ensure the image fits within the viewport */
  }

  #modalCaption {
    margin: 15px auto;
    text-align: center;
    color: #fff;
    font-size: 1.2rem;
  }

  .close {
    position: absolute;
    top: 10px;
    right: 25px;
    color: #fff;
    font-size: 35px;
    font-weight: bold;
    cursor: pointer;
  }

  .close:hover,
  .close:focus {
    color: #bbb;
    text-decoration: none;
    cursor: pointer;
  }
</style>

<script>
  // Function to open the modal
  function openModal(imageSrc, captionText) {
    const modal = document.getElementById("imageModal");
    const modalImg = document.getElementById("modalImage");
    const modalCaption = document.getElementById("modalCaption");

    modal.style.display = "block";
    modalImg.src = imageSrc;
    modalCaption.textContent = captionText;
  }

  // Function to close the modal
  function closeModal() {
    const modal = document.getElementById("imageModal");
    modal.style.display = "none";
  }

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