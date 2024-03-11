<template >
   <div class ="navbar">
      <div>
        <h1>Valantis</h1>
      </div>
      
      <div class="btn">        
        <button class="btns">Product</button>
        <button class="btns">корзина</button>
      </div>
    </div>
</template>
<script>
export default {
    name:"navbar",
    
}
</script>
<style > 

.btn{
  display: flex;
  margin-left: auto; 
  
}
.btns{
  background: none;
  border: 2px solid lightseagreen;
  padding: 10px;
  margin-left: 8px;
  font-size: 18px;
  border-radius: 5px;

}
</style>