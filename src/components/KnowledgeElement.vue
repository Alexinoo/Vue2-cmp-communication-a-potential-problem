<template>
  <li>

    <!-- KnowledgeElement Component

  -We are getting the following props from the Knowledge props : id , topic and description
      i.e.  props: ['id', 'topicName', 'description'],

  -This is where the CUSTOM-EVENT select-topic is generated after a click event and then we pass an ID and also include it in the emits[] - just to let other developers know that we are going to emit a custom event
   
      i.e. emits: ['select-topic'],
 -->




    <h3>{{ topicName }}</h3>
    <p>{{ description }}</p>
    <button @click="selectTopic(id)">Learn More</button>
  </li>
</template>

<script>
export default {

  inject : ['selectTopic'] ,
  props: ['id', 'topicName', 'description'],
  emits: ['select-topic'],
};
</script>