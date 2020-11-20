<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    KNN Iris Species Predictor
    </v-app-bar>
      
    <v-main>
     <v-card
         class="12sx"
         max-width="100%"
         
       >
       <div align="center">
       <v-img src="https://s3.amazonaws.com/assets.datacamp.com/blog_assets/Machine+Learning+R/iris-machinelearning.png" width="50%">
       </v-img>

       </div>
       
         <v-card-text>
           <h3>Select values below</h3>
         </v-card-text>
        <div class="sliders-div">
          <v-slider
            v-model="ex1.val"
            :label="ex1.label"
            :thumb-color="ex1.color"
            thumb-label="always"
            :max="8"
            step="0.1"
          ></v-slider>
          <v-slider
            v-model="ex2.val"
            :label="ex2.label"
            :thumb-color="ex2.color"
            thumb-label="always"
            :max="8"
            step="0.1"
          ></v-slider>
          <v-slider
            v-model="ex3.val"
            :label="ex3.label"
            :thumb-color="ex3.color"
            thumb-label="always"
            :max="8"
            step="0.1"
          ></v-slider>
          <v-slider
            v-model="ex4.val"
            :label="ex4.label"
            :thumb-color="ex4.color"
            thumb-label="always"
            :max="3"
            step="0.1"
          ></v-slider>

        </div>
        <div align="center">
              <v-btn color="primary" @click="btnclick">SUBMIT</v-btn>
          
        </div>
       </v-card>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data () {
      return {
        ex1: { label: 'Sepal Length', val: 0, color: 'red' },
        ex2: { label: 'Sepal Width', val: 0, color: 'red' },
        ex3: { label: 'Petal Length', val: 0, color: 'red' },
        ex4: { label: 'Petal Width', val: 0, color: 'red' },
      }
    },
    methods:{
    btnclick(){
      let jsonData = {
        "sepal_length": this.ex1.val,
        "sepal_width": this.ex2.val,
        "petal_length": this.ex3.val,
        "petal_width": this.ex4.val
      }
      fetch('http://knn-iris-ml.herokuapp.com/predict', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(jsonData),
      })
      .then(response => response.json())
      .then(data => {
        this.$swal.fire('Results',
                      `Species Predicted: ${data.prediction}  (Probability: ${data.probability})`,
                      'info');
      })
      .catch((error) => {
        console.error('Error:', error);
      });
      
      
    }
  }
  }
</script>

<style>
.sliders-div {
  padding: 10px;
}
</style>
