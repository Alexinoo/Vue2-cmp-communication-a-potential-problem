<template>
  <section>
    <h2>Select a Topic</h2>


    <!-- PROPS DRILLING----
      
      -We are getting props topics from App.vue

      -Then we are forwarding topics array which was forwarded from App.Vue to KnowledgeGrid Component    
    
    -Then we are declaring that we are going to emit select-topic  custom event to the App.vue

    -Therefore KnowledgeBase Componet acts as just a pass through and does not really have it's own logic

    -We have a slight problem here because KnowledgeBase has nothing to do with 

    :topics="topics" @select-topic="$emit('select-topic', $event)"
    
     -->


    <!--  Provide + Inject to the Rescue - WITH PROPS


    -We can solve this by first removing 

        1.  :topics="topics" --REMOVED FROM  <knowledge-grid 

        2. And then   props: ['topics'],

      -And then find a way to pass topics array to KnowledgeGrid in a different way because we need the Topics there

      -->

    <!--  Provide + Inject to the Rescue - WITH PROPS

  -AND THEN REMOVE FROM EMITS
    -->

    <!-- EMITTING - WITH METHODS / FUNCTIONS

-REMOVE CUSTOM EVENT

AND ITS EMITS

    -->

    <knowledge-grid>
    </knowledge-grid>
  </section>
</template>

<script>
export default {
  // props: ['topics'],
  // emits: ['select-topic'],
};
</script>