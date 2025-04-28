<template>
    <footer>
        <p>Kohaydev &copy; 2025</p>
    </footer>
</template>

<script>
    export default {
        name: 'Footer'
    }
</script>

<style scoped>
    footer {
        background-color: #9E42EC;
        height: 150px;
        width: 100%;    
        display: flex;
        align-items: center;
        justify-content: center;
    }

    footer p {
        text-align: center;
        color: #fff;
        font-style: italic;
    }
</style>