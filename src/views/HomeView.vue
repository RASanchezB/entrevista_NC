<script>
import HeaderItem from '../components/HeaderItem.vue';
import FooterItem from '../components/FooterItem.vue';
import axios from 'axios'

export default {
  name: "Home",
  components:{
    HeaderItem,
    FooterItem,
  },
  data(){
    return{
      listado: [],
    }
  },
  async mounted(){
    listado = await axios.get('http://localhost:8081/api/members', {}, {
      auth: {
        username: 'sarah',
        password: 'connor'
      }
    })
    .then(response => (
      this.$data.listado = response
    ))
  },
  methods:{
    updateTable(){
    },
    resetButton(){
      console.log("Reset");
    },
    submitButton(){
      let fname = document.getElementById('fname').value
      let lname = document.getElementById('lname').value
      let addr = document.getElementById('address').value
      let ssn = document.getElementById('ssn').value
      
    },

  }

}

</script>

<template>
  <div class="background">
    <HeaderItem/>
    <div class="container">
      <div class="column">
        <form>
          <label for="fname">First name:</label><br>
          <input type="text" id="fname" name="fname"><br>
          <label for="lname">Last name:</label><br>
          <input type="text" id="lname" name="lname"><br>
          <label for="address">Address:</label><br>
          <input type="text" id="address" name="address"><br>
          <label for="ssn">SSN:</label><br>
          <input type="text" id="ssn" name="ssn"><br>
          <div class="column">
            <input type="submit" value="Reset" @click="resetButton()">
            <input type="submit" value="Submit" @click="submitButton()">
          </div>
        </form>
      </div>

      <div class="column">
        <table id="table">
          <tr>
            <th>First Name</th>
            <th>Last name</th>
            <th>Address</th>
            <th>SSN</th>
          </tr>
        </table>>
      </div>
    </div>
    <FooterItem />
  </div>
</template>

<style>
.container{
  background-color: red;
  align-content: center;
  position: relative;
  height: 70%;
  margin-top: 40px;
  
}
table, th, td {
  border: 1px solid;
  color: black;
}
th, td{
  padding: 7px;
  width:  5%;
  height: 5%;
  object-fit: cover;
}
.column {
  float: left;
  width: 50%;
  align-content: center;
  background-color: white;
  height: 90%;
  justify-content: center;
}
form{
  color: black;
  margin-left: 20%;
}
label{
  color: black;
}
.background{
  width: 100%;
  height: 100%;
  position:absolute;
  top:0px;
  right:0px;
  bottom:0px;
  left:0px;
}
#FooterItem{
  bottom: 0%;
}
</style>
