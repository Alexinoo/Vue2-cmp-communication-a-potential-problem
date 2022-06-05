<template>
  <ul>

    <!-- KnowledgeGrid Component 
    
    -We are getting props topics array  from KnowledgeBase

      i.e. props: ['topics'],
    
    
    and then looping  and passing them to KnowledgeElement Component

      v-for="topic in topics"
      :key="topic.id"
      :id="topic.id"
      :topic-name="topic.title"
      :description="topic.description"

    -But we also emit select-topic CUSTOM EVENT BUT THIS IS NOT WHERE THE CUSTOM EVENT IS GENERATED

    -KnowledgeBase component is just listening to it and then emitting it    
    
    -->


    <!-- LISTENING TO PROVIDE AND INJECT - WITH PROPS
    
        - SO FIRST LET'S COMMENT ON THE PROPS BECAUSE WE ARE NOT GETIING IT AS PROPS FROM KNOWLEDGEBASE ANYMORE!!
     -AND WE USE INJECT WHICH WORKS TOGETHER WITH PROVIDE

     -INJECT BASICALLY WORKS LIKE PROP ; 
     
     -TAKES IN AN ARRAY WITH THE DATA YOU WANNA USE IN THIS COMPONENT WHICH IS TOPICS I.E THE KEY TOP[ICS FROM THE PROVIDE IN THE APP.VUE

     -YOU CAN ONLY INJECT WHAT HAS BEEN PROVIDED ON A HIGHER-UP LEVEL I.E. PARENT-CHILD RELATION
    
     -->

    <!-- LISTENING TO PROVIDE AND INJECT - WITH METHODS / FUNCTIONS

-REMOVE CUSTOM EVENT

AND ITS EMITS

    -->



    <knowledge-element
      v-for="topic in topics"
      :key="topic.id"
      :id="topic.id"
      :topic-name="topic.title"
      :description="topic.description"
    ></knowledge-element>
  </ul>
</template>

<script>
export default {
  // props: ['topics'],

  inject: ['topics'],


  // emits: ['select-topic']
};
</script>