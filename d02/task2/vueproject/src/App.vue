<template>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet"
    integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous" />

  <div class="container">
    <div class="row">
      <div class="col-12">
        <headercomponent/>
      </div> <!--header component-->
    </div>
    <div class="row">
      <div class="col-4">
        <linkscomponent/>
      </div> <!--link component-->
      <div class="col-8">
        <bodycomponent/>
      </div><!--body component--> 
    </div>
    <div class="row">
        <div class="col-12">
          <footercomponent/>
        </div><!--footer component-->          
    </div>
  </div>
</template>

<script>
import headercomponent from './components/headercomponent.vue'
import linkscomponent from './components/linkscomponent.vue'
import bodycomponent from './components/bodycomponent.vue'
import footercomponent from './components/footercomponent.vue'

export default {
  name: "App",
  components: {
    headercomponent,
    linkscomponent,
    bodycomponent,
    footercomponent,
  },
};
</script>

<style>
#app {}
</style>
