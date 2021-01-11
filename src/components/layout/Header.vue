<template>
    <header>
        <router-link to="/">Home Page</router-link>
        <router-link to="/TodoList">TodoList Page</router-link>
    </header>
</template>

<script>
export default {
    name:"Header"
}
</script>

<style scoped>
header {
    padding: 20px;
    background: #000000;
    text-align: center;
}

a {
    color: #ffffff;
    text-decoration: none;
    margin: 10px;
}

a.router-link-exact-active {
  border-bottom: 3px solid #ffffff;
}

a:hover {
    border-bottom: 3px solid #ffffff;
}
</style>