<style>
  /* Modal styles */
  .modal {
    display: none; /* Hidden by default */
    position: fixed; /* Stay in place */
    z-index: 1000; /* Sit on top */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    background-color: rgba(0, 0, 0, 0.8); /* Black background with opacity */
    display: flex; /* Flexbox for centering */
    justify-content: center; /* Horizontally center */
    align-items: center; /* Vertically center */
  }

  .modal-content-wrapper {
    position: relative;
    max-width: 90%; /* Limit the size of the popup */
    max-height: 90%; /* Ensure the image fits within the viewport */
    background: #fff;
    border-radius: 8px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.25);
    overflow: hidden;
  }

  .modal-content {
    display: block;
    width: 100%;
    height: auto;
  }

  #modalCaption {
    margin: 15px auto;
    text-align: center;
    color: #333;
    font-size: 1rem;
    padding: 0.5rem 1rem;
  }

  .close {
    position: absolute;
    top: 10px;
    right: 10px;
    color: #000;
    font-size: 24px;
    font-weight: bold;
    background: #fff;
    border: 2px solid #ddd;
    border-radius: 50%;
    width: 32px;
    height: 32px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  }

  .close:hover {
    background-color: #f1f1f1;
  }
</style>

<script>
  // Function to open the modal
  function openModal(imageSrc, captionText) {
    const modal = document.getElementById("imageModal");
    const modalImg = document.getElementById("modalImage");
    const modalCaption = document.getElementById("modalCaption");

    modal.style.display = "flex"; // Ensure the modal uses flexbox for centering
    modalImg.src = imageSrc;
    modalCaption.textContent = captionText;
  }

  // Function to close the modal
  function closeModal() {
    const modal = document.getElementById("imageModal");
    modal.style.display = "none";
  }
</script>