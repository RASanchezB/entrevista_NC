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
      url: 'http://localhost:8081/api/members',
      authUrl: 'http://localhost:8081/auth',
      username: 'sarah',
      password: 'connor',
      token: "",
      temp: []

    }
  },
  async mounted(){
    //Se consigue el token
    try{
      await axios.post(this.$data.authUrl, {     
          username: this.$data.username,
          password: this.$data.password     
      })
      .then(response => (
        this.$data.token= (response.data.token)
      ))
    }catch(error){
      console.log(error)
    }


    try{
      await axios.get(this.$data.url, {
        headers:{
          Authorization: `Bearer ${this.$data.token}` 
        }
      }).then(response =>{
        this.$data.listado = response
      })
    }catch(error){
      console.log(error)
    }
    this.updateTable()

  },
  computed:{
    isDisabled() {
      let ssnumber = document.getElementById('ssn')?.value || ''
      this.$data.temp = this.$data.listado.data?.map((res)=>{
        return res.ssn
      })
      if(this.$data.temp?.includes(ssnumber)){
        return true;
      }else{
        return false;
      }
    },
  },
  methods:{
    updateTable(){
      for(var i = 0; i < this.$data.listado.data.length; i++){
        // Nueva linea
        var newRow = table.insertRow(table.length);
        // Nueva celda
        var cell1 = newRow.insertCell(0);
        cell1.innerHTML = this.$data.listado.data[i].firstName; 
        var cell2 = newRow.insertCell(1);
        cell2.innerHTML = this.$data.listado.data[i].lastName;
        var cell3 = newRow.insertCell(2);
        cell3.innerHTML = this.$data.listado.data[i].address;
        var cell4 = newRow.insertCell(3);     
        cell4.innerHTML = this.$data.listado.data[i].ssn;
        
      }
    },
    resetButton(){
      document.getElementById("fname").value = "";
      document.getElementById("lname").value = "";
      document.getElementById("address").value = "";
      document.getElementById("ssn").value = "";
    },
    async submitButton(){
      let fName = document.getElementById('fname').value
      let lName = document.getElementById('lname').value
      let addr = document.getElementById('address').value
      let ssnumber = document.getElementById('ssn').value

      
      // Llenar la tabla sin update
      var newRow = table.insertRow(table.length);
      var cell1 = newRow.insertCell(0);
      cell1.innerHTML = fName; 
      var cell2 = newRow.insertCell(1);
      cell2.innerHTML = lName;
      var cell3 = newRow.insertCell(2);
      cell3.innerHTML = addr
      var cell4 = newRow.insertCell(3);     
      cell4.innerHTML = ssnumber;
      //subir a api
      try{
        await axios.post(this.$data.url, {
            firstName: fName,
            lastName: lName,
            address: addr,
            ssn: ssnumber,
          },{
            headers:{
              Authorization: `Bearer ${this.$data.token}` 
            }
          }).then(response =>{
            console.log(response);
          })
        }catch(error){
          console.log(error)
        }
      
    },
    
    

  }

}

</script>

<template>
  <div class="background">
    <meta http-equiv="refresh" content="100" >
    <HeaderItem/>
    <div class="container">
      <div class="column">
        <form>
          <label for="fname">First name:</label><br>
          <input type="text" id="fname" name="fname" required><br>
          <label for="lname">Last name:</label><br>
          <input type="text" id="lname" name="lname" required><br>
          <label for="address">Address:</label><br>
          <input type="text" id="address" name="address" required><br>
          <label for="ssn">SSN: (###-##-####)</label><br>
          <input type="text" id="ssn" name="ssn" required pattern="^(?!(000|666|9))\d{3}-(?!00)\d{2}-(?!0000)\d{4}$"  ><br>
          <div class="column">
            <input type="submit" value="Reset" @click="resetButton()">
            <input type="submit" value="Submit" @click="submitButton()" :disabled="isDisabled">
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
