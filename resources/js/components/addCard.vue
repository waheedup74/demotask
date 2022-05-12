<template>
    <div>
   <!-- Modal -->
   <modal :name="'addCard'+colId" class="model">
      <div class="modelContent">

      <p>Title:</p>
      <input type="text" v-model="cardTitle">
      <p>Description:</p>
      <textarea rows="5" cols="50" v-model="cardDescription"></textarea>
      <br>
      <button @click="addCard">Add</button>
      </div>
       <button class="closeModel" @click="hide">X</button>
     </modal>

</div>
</template>
<script>
    import Vue from 'vue'
    import Vmodal from 'vue-js-modal/dist/ssr.nocss'

    import 'vue-js-modal/dist/styles.css'
    // Vue.use(Vmodal);
    export default {
        components: {
            Vmodal,
        },
        props: ['id'],
         data() {
            return {
                colId: this.id,
                cardTitle: '',
                cardDescription: ''
            }
        },
        mounted() {
        },
        methods:{

            addCard(){

            this.$modal.hide('addCard'+this.colId);

             axios.post('/demos/card', {

              title: this.cardTitle,
              description: this.cardDescription,
              column_id: this.colId

                }).then((response) => {
                    console.log(response.data);
                   this.$emit('card', response.data);
                  }).catch((error) => {
                      console.log(error);
                  })

            },

            hide(){
                this.$modal.hide('addCard'+this.colId);

            }             
        }

      }


  </script>