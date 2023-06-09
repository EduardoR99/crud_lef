<template>
    <div class="navbar_container">
        <RouterLink to="/" class="icon_navbar">
            <img src="../assets/images/parceria.png" alt="">
        </RouterLink>
        <div class="text_navbar">
            <div>Company </div>
            <div class="text_colored">Register</div>
        </div>

        <RouterLink to="/companieslist" class="companies_list">
            <div>companies </div>
            <div class="text_colored">List</div>
        </RouterLink>

    </div>
</template>
<script>

</script>
<style scoped>
.navbar_container {
    display: flex;
    align-items: center;
    font-weight: 700;
    position: relative;
}

.icon_navbar img {
    width: 65px;
    margin-top: .5rem;
    margin-left: .5rem;
    border-radius: 50%;
}

.icon_navbar {
    margin-right: 1.3rem;
}

.text_navbar {
    display: flex;
    color: #ccc;
    font-size: 22px;
}
.text_colored {
    margin-left: .3rem;
    background: linear-gradient(to bottom, #fd5949, #285AEB);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;

}
.companies_list {
    position: absolute;
    padding-right: 1rem;
    top: 0;
    right: 0;
    color: #ccc;
    display: flex;
    align-items: center;
    border: none;
    outline: none;
}
</style>