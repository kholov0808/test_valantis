<template >
    <div class="post" v-for="poduct in poducts ">
        <div><strong>id: </strong>{{poduct.id  }}</div>
        <div><strong>name: </strong>{{poduct.title  }}</div>
        <div><strong>price: </strong>{{poduct.price  }}</div>
        <div><strong>brand :</strong>{{poduct.body  }}</div>
    </div>
</template>
<script>
export default {
    name:"product-list",
    props:{
        poducts:{
            type:Array,
            requerid:true
        }
    }
}
</script>
<style >
.post{
  padding: 8px;
  margin-top: 12px;
  border: 2px solid lightseagreen;
}
</style>