<!-- HeaderNav.svelte -->
<script>
    // Bạn có thể thêm logic xử lý tại đây nếu cần thiết
</script>

<div class="header-nav">
    <nav>
        <a href="/home">Home</a>
        <a href="/portfolio">Portfolio</a>
        <a href="/product">Product</a>
    </nav>
</div>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap");

    /* CSS cho component HeaderNav */
    .header-nav {
        font-family: "Poppins", sans-serif;
        background-color: #001f3f;
        padding: 10px;
        text-align: center;
    }

    nav {
        display: flex;
        justify-content: flex-start; /* Chuyển từ space-around sang flex-start để căn trái */
    }

    a {
        color: white;
        text-decoration: none;
        padding: 10px 20px;
        border-radius: 5px;
        transition: background-color 0.3s ease;
        border: 1px solid #fff; /* Thêm border */
        margin-right: 10px; /* Thêm margin-right để phân chia rõ ràng */
    }

    a:last-child {
        margin-right: 0; /* Loại bỏ margin-right của mục cuối cùng để tránh khoảng trắng thừa */
    }

    a:hover {
        background-color: #003366; /* Màu đậm hơn cho trạng thái hover */
    }
</style>
