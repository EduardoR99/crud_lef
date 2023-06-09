<script>
export default {
    name: 'Footer'
}
</script>
<template>
    <footer>
        <p>Copyright - Eduardo Rodrigues - Todos os Direitos Reservados</p>
    </footer>
</template>
<style scoped>
footer {
    margin-top: 3rem;
    display: flex;
    justify-content: center;
    color: #ccc;
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 50px; 
    display: flex;
    justify-content: center;
    align-items: center;
}

footer p {
    margin: 1rem;
}
</style>

