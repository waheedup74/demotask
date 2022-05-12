<template>
    <div>
   <!-- Modal -->
   <modal name="addCol" class="model">
      <div class="modelContent">
      <h3>Add Coloum</h3>
      <p>Title:</p>
      <input type="text" v-model="columnTitle">
      
      <button @click="addColumn">Add</button>
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
        props: ['columnDate'],
         data() {
            return {
                
                columnTitle: ''
            }
        },
        mounted() {
          console.log(this.cardData);
        },
        methods:{

            addColumn(){

             axios.post('/demos/column', {
              title: this.columnTitle,
                  }).then((response) => {
                      console.log(response.data);
                this.$emit('column', response.data);

                  }).catch((error) => {
                      console.log(error);
                  })
                this.$modal.hide('addCol');

            },
            hide(){
                this.$modal.hide('addCol');

            }             
        }

      }


  </script>