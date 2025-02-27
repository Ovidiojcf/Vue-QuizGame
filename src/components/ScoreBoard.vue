<script>
export default {

}
</script>



<template>
  <section class="score">
    Player <span>{{ }}  </span>  x  <span>
       {{ }}
    </span> Computer
  </section>
</template>


<style>
  section.score{
    border-bottom: 1px solid rgb(49, 72, 253);
    padding: 24px;
    font-size: 18px;

    span{
      padding: 8px;
      font-weight: bold;
      border: 1px solid black;
    }
  }
</style>
