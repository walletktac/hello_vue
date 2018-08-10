<template>
    
       <div class="outerWrapper">
           <div class="innerWrapper">
               <div class="photo">

               </div>
               <div class="description">
                   <h2 class="title">lorem ipsum</h2>
                   <p class="description">
                       opsi
                   </p>
               </div>
           </div>
           <div class="close" @click="$emit('closeModal')" />
       </div>
   
</template>
<script>
export default {
  name: 'Modal',
 
};
</script>

<style lang="scss" scoped>
    .outerWrapper{
        background: #f6f6f6 ;
        max-width: 100%;
        position: fixed;
        top:0;
        left:0;
    }
    .innerWrapper{
        display: flex;
        height: 100%;
        padding: 50px;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }
    .photo{
        width: 50%;

    }
    div.description{
        width: 50%;
    }
    .close{
        position: absolute;
        width: 30px;
        height: 30px;
        right: 0px;
        top: 0px;
        cursor: pointer;
        &::before,
        &::after{
            position: absolute;
            top: 30px;
            right: 20px;
            content: '';
            width: 20px;
            height: 2px;
            background: #000;
            display: block;
        }
        &::before{
            transform: rotate(45deg);
        }
        &::after {
            transform: rotate(-45deg);
        }
    }
</style>




