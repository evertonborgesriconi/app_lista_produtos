<template>
  <header>
   <h1>Projeto Vue.js 3</h1>
  </header>
</template>

<script>
export default {
  name: "HeaderTop",
};
</script>


<style scoped>
header {
  
  background-color: #bf5b5b;
  padding-top:20px;
  width: 100%;
  height: 100px;
  text-align: center;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);

}

/* Style the header links */
header h1 {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  float: center;
  color: rgb(5, 4, 4);
  text-align: center;
  font-size: 40px;
 
}

@media screen and (max-width: 500px) {
  .header a {
    float: none;
    display: block;
    text-align: left;
  }
  .header-right {
    float: none;
  }
}
</style>
