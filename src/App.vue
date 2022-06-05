<template>
  <div>

    <!-- Rendering Active component -->

    <!--

      - We are passing topic-title and text that we are getting from internal data after the activeTopic is triggered which is initially set to null

      - When the activateTopic() is triggered , we set the activeTopic to one of the id's in the topic array

      -If activeTopic is null , we don't pass anything to the ActiveElement , and therefore nothing will be displayed until it is set to something

      -But if we have an activeTopic , then we pass topic-title and text values to the ActiveElement


      -->
    <active-element :topic-title="activeTopic && activeTopic.title" :text="activeTopic && activeTopic.fullText">
    </active-element>


    <!-- Rendering Knowledge Base component  -->


    <!-- 

      -The activateTopic is triggered on the knowledge-base component where we are listening for a custom-event which comes with an ID tha will help us identify which id from the topics Array was passed

      -Also note that we are passing/feeding the entire topics array as a value to the topics prop on the KnowledgeBase Component
    
     -->


    <!--  PROVIDE + INJECT TO THE RESCUE -- WITH PROPS


    -So can we pass the topics to the KnowledgeGrid without passing through the KnowledgeBase

    -So let's remove them from here

        1.  :topics="topics" --REMOVED FROM  <knowledge-base 

        2. And then  let us explore another future that Vue offers

      -WHICH IS PROVIDE AND INJECT WHICH IS A PATTERN WE CAN USE 

      -WE DO THIS BY PROVIDING A PROVIDE OBJECT ANY WHERE IN OUR CONFIG OBJECT

      -AND THEN PASS OUR TOPICS ARRAY

            provide : {
               topics: [
                                {
                                  id: 'basics',
                                  title: 'The Basics',
                                  description: 'Core Vue basics you have to know',
                                  fullText:
                                    'Vue is a great framework and it has a couple of key concepts: Data binding, events, components and reactivity - that should tell you something!',
                                },
                                {
                                  id: 'components',
                                  title: 'Components',
                                  description:
                                    'Components are a core concept for building Vue UIs and apps',
                                  fullText:
                                    'With components, you can split logic (and markup) into separate building blocks and then combine those building blocks (and re-use them) to build powerful user interfaces.',
                                },
                              ],
            }

            -BUT providing is just HALF OF THE STORY , WE NEED TO USE THE PROVIDED DATA SOMEWHERE

            -AND THAT IN OUR CASE WOULD TAKE PLACE IN OUR KNOWLEDGE GRID BECAUSE THAT IS WHERE WE NEED THE TOPICS

            -AND THIS WORKS!!!!!!!!!!!!!!!!!!!!!!!


            -BUT THE PROBLEM IS ; WE ARE MANANGING TOPICS ARRAY TWICE ( IN OUR DATA AND THEN AGAIN IN OUR OUR PROVIDER )WHICH WILL BE HARD TO MANAGE


            -THIS WORKS IN THIS CASE BUT THIS IS CODE DUPLICATION I.E CHANGES DONE IN THE TOPICS DATA PROPERTY WILL NOT BE REFLECTED IN THE PROVIDERS

            -AND IT TURNS OUT WE CAN DO THAT ; SO INSTEAD WE CONVERT PROVIDE TO A METHOD

            -AND IN HERE WE RETURN OUR OBJECT SO THAT IT CAN WORK A LITTLE BIT LIKE DATA AND PROVIDES KEYS OF OUR CHOICE BUT LET'S STICK TO TOPICS FOR NOW

            -BUT NOW WE CAN USE this.topics to refer to the topics from the data property

            e.g.

            provide(){

                return {
                  topics : this.topics
                }
              }
            }

            -topics key can be anything but let's use it for now


            -LET'S SIMULATE TOPICS CHANGES  BY MOUNTING mounted() and set a setTimeout() and reach out to this topics and push a new topic to this array-AND THIS WORKS

      -->


    <!--  PROVIDE + INJECT TO THE RESCUE -- WITH FUNCTIONS / METHODS

    -WE COULD REMOVE @select-topic="activateTopic" FROM KNOWLEDGEBASE

    - FOR REFERENCE  <knowledge-base @select-topic="activateTopic"></knowledge-base>

    -AND THEN GO TO KNOWLEDGEBASE COMPONENT AND REMOVE IT THERE

    -Then we add selectTopic  to our provider 
    
    -which points to a function in this case activateTopic - DO NOT EXECUTE
    
    -that will be a function to be executed when the event click occurs on Learn More..

    -Then Go to KnowledegElement componnt and inject it there



    -->


    <knowledge-base ></knowledge-base>
  </div>
</template>

<script>
export default {
  data() {
    return {
      topics: [
        {
          id: 'basics',
          title: 'The Basics',
          description: 'Core Vue basics you have to know',
          fullText:
            'Vue is a great framework and it has a couple of key concepts: Data binding, events, components and reactivity - that should tell you something!',
        },
        {
          id: 'components',
          title: 'Components',
          description:
            'Components are a core concept for building Vue UIs and apps',
          fullText:
            'With components, you can split logic (and markup) into separate building blocks and then combine those building blocks (and re-use them) to build powerful user interfaces.',
        },
      ],
      activeTopic: null,
    };
  },

provide(){

  return {
    topics : this.topics ,
    selectTopic: this.activateTopic
  }
},

mounted(){

  setTimeout(()=>{

    this.topics.push({

      id: 'events',
      title: 'Events',
      description:
        'Events are important in Vue',
      fullText:
        'Events allow you to trigger code on demand!',

    })

  }, 5000)
},


  methods: {
    activateTopic(topicId) {
      this.activeTopic = this.topics.find((topic) => topic.id === topicId);
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
section {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 2rem auto;
  max-width: 40rem;
  padding: 1rem;
  border-radius: 12px;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
}

li {
  border-radius: 12px;
  border: 1px solid #ccc;
  padding: 1rem;
  width: 15rem;
  margin: 0 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h2 {
  margin: 0.75rem 0;
  text-align: center;
}

button {
  font: inherit;
  border: 1px solid #c70053;
  background-color: #c70053;
  color: white;
  padding: 0.75rem 2rem;
  border-radius: 30px;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #e24d8b;
  border-color: #e24d8b;
}
</style>