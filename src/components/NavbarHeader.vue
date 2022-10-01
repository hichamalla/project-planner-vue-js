<script>

  export default{
    name:'NavbarHeader'
  }
</script>
<template>
     
    <nav class="main-nav">
      <RouterLink to="/">Home</RouterLink> | 
      <RouterLink to="/newproject">new project</RouterLink> | 
      <RouterLink to="/about">About</RouterLink>
    </nav>


</template>
<style>
   .main-nav {
    text-align: center;
    margin: 40px auto;
  }
  .main-nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;
  }
  a.router-link-active {
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
  }
</style>