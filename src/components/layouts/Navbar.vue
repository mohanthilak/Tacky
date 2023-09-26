<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <h1 class="navbar-brand">{{ brandName }}</h1>
      <p class="navbar-text">{{ tagLine }} <span class="navbar-subtag">{{ tagLine2 }}</span></p>
      <p>Just DRAG & DROP tasks to switch between stages of progress. </p>
    </nav>
</template>
  
<script>
    export default {
        name: 'Navbar',
        props: {
            brandName: String,
            tagLine: String,
            tagLine2: String,
        }
    };
</script>
<style>
.navbar {
    border-bottom: 2px solid black;
    padding: 2px 50px;
}
.navbar .navbar-brand {
    font-size: 40px;
    margin-top: 2px;
    margin-bottom: 2px;
}
.navbar .navbar-text {
    margin-top: 5px;
    margin-bottom: 12px;
    font-weight: 500;
}
.navbar .navbar-text .navbar-subtag{
    font-weight: 400;
}
</style>