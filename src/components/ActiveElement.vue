<template>
  <section>

    <!--  ActiveElement component
    
    - Getting props from Parent component i.e. topicTitle and text wrapped in App.vue
    
    -Output them in the sreen
    
    
    -->
    <h2>{{ topicTitle }}</h2>
    <p>{{ text }}</p>
  </section>

</template>



<script>
export default {
  props: ['topicTitle', 'text'],
};
</script>