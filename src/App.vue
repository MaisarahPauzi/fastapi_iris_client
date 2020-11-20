<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    HL Bank Special Survey
    </v-app-bar>
      
    <v-main>
     <v-card
         class="12sx"
         max-width="100%"
       >
       
       
         <v-card-text>
           <h3>Please answer the questions Below</h3>
           <div class="formfiels">

           </div>
           
          <v-text-field
            v-model="email_address"
            label="Email Address"
            placeholder="Please enter you email address"
          ></v-text-field>

          <v-text-field
            v-model="age"
            label="Age"
            placeholder="What is your current age?"
          ></v-text-field>

          <p>Gender</p>

          <v-radio-group v-model="gender">
          <v-radio
            :label="`Male`"
            :value="`MALE`"
          ></v-radio>
          <v-radio
            :label="`Female`"
            :value="`FEMALE`"
          ></v-radio>
        </v-radio-group>

          <p>Marital Status</p>

         <v-radio-group v-model="maritalStatus">
          <v-radio
            :label="`Single`"
            :value="`SINGLE`"
          ></v-radio>
          <v-radio
            :label="`Married`"
            :value="`MARRIED`"
          ></v-radio>
        </v-radio-group>

        <v-text-field
            v-model="nationality"
            label="Nationality"
            placeholder="What is your nationality? (e.g MALAYSIA)"
          ></v-text-field>

          <v-select
          v-model="ethnic"
          :items="ethnic_choice"
          label="Ethnic"
        ></v-select>

        <v-select
          v-model="occupation"
          :items="occupation_group_choice"
          label="Occupation Sector"
        ></v-select>

        <p>Did you use Internet Banking?</p>
        <v-radio-group v-model="IB">
          <v-radio
            :label="`Yes`"
            :value="`Y`"
          ></v-radio>
          <v-radio
            :label="`No`"
            :value="`N`"
          ></v-radio>
        </v-radio-group>
        <p>Did you use Mobile Banking?</p>
        <v-radio-group v-model="MB">
          <v-radio
            :label="`Yes`"
            :value="`Y`"
          ></v-radio>
          <v-radio
            :label="`No`"
            :value="`N`"
          ></v-radio>
        </v-radio-group>
         </v-card-text>

         
        <div>
         
        </div>
        <div align="center">
              By submitting this form, you agree to our Terms &amp; Condition <br><br>
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
        email_address: '',
        ethnic:'',
        occupation:'',
        nationality:'MALAYSIA',
        age:0,
        IB:'Y',
        MB:'Y',
        gender: 'MALE',
        customer_type: 'MASS',
        maritalStatus: 'SINGLE',
        ethnic_choice: [
          'MALAY','CHINESE','INDIAN','OTHERS','FOREIGNER WITH PR STATUS','EURASIAN', 'No Description'
        ],
        occupation_group_choice : [
          'PROFESSIONALS',
          'LEGISLATORS', 
          'SENIOR OFFICIALS AND MANAGERS',
          'NON-EMPLOYED / NON-GAINFULLY EMPLOYED',
          'CLERICAL', 
          'SECRETARIAL AND ADMINISTRATIVE RELATED',
          'SALES WORKERS RELATED',
          'TECHNICIANS', 
          'SEMI-SKILLED AND ASSOCIATE PROFESSIONALS',
          'ENTREPRENEURS AND BUSINESS OWNERS',
          'RS RELATED',
          'ATHLETIC, ARTISTIC, CRAFT, CULTURE AND DESIGNER','ELEMENTARY OCCUPATIONS','EXEBB CONVERSION','UNIFORMED AND ARMED FORCES'   
        ]
      }
    },
    methods:{
    btnclick(){
      let jsonData = {
          "Email_Address": this.email_address,
          "Customer_Type": "MASS",
          "Age":this.age,
          "Gender":this.gender,
          "MaritalStatus":this.maritalStatus,
          "Nationality":this.nationality,
          "Ethnic": this.ethnic,
          "Occupation_Group": this.occupation,
          "IB":this.IB,
          "MB":this.MB
      }
      fetch('http://localhost:8000/predict', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(jsonData),
      })
      .then(response => response.json())
      .then(data => {
        console.log(data)
      })
      .catch((error) => {
        console.error('Error:', error);
      });
      this.$swal('Thank You!')
      
    }
  }
  }
</script>

<style>
.formfiels {
  padding: 20px;
}
</style>
