<template>
  <div id="app">
    <div class="container-fluid">
        <div class="row bg-dark">
            <div class="col-lg-12">
              <p class="text-center text-light display-4 pt-2">REAL ESTATE OFFERS &nbsp; <i class="fas fa-home"></i></p>
            </div>
        </div>
      </div>
      <div class="container">
        <div class="row mt-3">
          <div class="col-lg-6">
            <h3 class="text-info">All available estates: </h3>
          </div>
          <div class="col-lg-6">
             <button class="btn btn-info float-right" @click="showAddF=true; showDetailsF=false;">
               Add new estate&nbsp;&nbsp;<i class="fas fa-plus"></i>
             </button>
          </div>
       </div>
        <hr class="bg-info">
        <div class="alert alert-danger" v-if="errorMsg">{{ errorMsg }}</div>
        <div class="alert alert-success" v-if="successMsg">{{ successMsg }}</div>
      
      
        
          <div class="col-lg-12 table-responsive-xl">
            <table class="table table-bordered table-striped ">
              <thead>
                <tr class="text-center bg-info text-light">
                  <!-- <th>ID</th> -->
                  <th scope="col" style="background-color:orange; color:black;">Id</th>
                  <th scope="col">City</th>
                  <th scope="col">Street</th>
                  <th scope="col">Property</th>
                  <th scope="col">Apartment</th>
                  <th scope="col">Price</th>
                  <th scope="col">Type</th>
                  <th scope="col">Description</th>
                  <th scope="col">Edit</th>
                  <th scope="col">Delete</th>
                  <th scope="col">See more details</th>
                </tr>
              </thead>
              <tbody> 
              <tr class="text-center" v-for="advertisement in advertisements" :key="advertisement.id">
                  <!-- <td>{{ advertisement.id }}</td> -->
                  <td scope="row" style="background-color:orange; color:black;">{{ advertisement.id }}</td>
                  <td>{{ advertisement.city }}</td>
                  <td>{{ advertisement.street }}</td>
                  <td>{{ advertisement.property }}</td>
                  <td>{{ advertisement.apartment }}</td>
                  <td>{{ advertisement.price }}</td>
                  <td>{{ advertisement.type }}</td>
                  <td>{{ advertisement.description }}</td>
                  <td><a href="#" class="text-succes" @click="showEditF=true; selectAd(advertisement); showDetailsF=false;"><i class="fas fa-edit"></i></a></td>
                  <td><a href="#" class="text-danger" @click="showDeleteF=true; selectAd(advertisement); showDetailsF=false;" ><i class="fas fa-trash-alt"></i></a></td>
                  <td><a href="#" @click=" showDetailsF=true; selectAd(advertisement);" > <i class="fas fa-eye"></i></a></td>
              </tr>
                
              </tbody>
            </table>

         </div>
        </div>
     
    
<!-- ADD -->
    <div id="overlay" v-if="showAddF">
      <div class="modal-dialog">
         <div class="modal-content">
            <div class="modal-header">
               <h5 class="modal-title">Add Your advertisement</h5>
                <button type="button" class="close" @click="showAddF=false">
                  <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                  <div class="form-group">
                     <input type="text" name="city" class="form-control form-control-lg" placeholder="City" v-model="newAd.city" >
                     <!-- v-model="newAd.city" -->
                  </div>
                    <div class="form-group">
                     <input type="text" name="street" class="form-control form-control-lg" placeholder="Street" v-model="newAd.street">
                  </div>
                    <div class="form-group">
                     <input type="text" name="property" class="form-control form-control-lg" placeholder="Property" v-model="newAd.property">
                  </div>
                     <div class="form-group">
                     <input type="text" name="apartment" class="form-control form-control-lg" placeholder="Apartment" v-model="newAd.apartment">
                  </div>
                    <div class="form-group">
                     <input type="text" name="price" class="form-control form-control-lg" placeholder="Price" v-model="newAd.price">
                  </div>
                    <div class="form-group">
                     <input type="text" name="type" class="form-control form-control-lg" placeholder="Type" v-model="newAd.type">
                  </div>
                    <div class="form-group">
                     <input type="text" name="description" class="form-control form-control-lg" placeholder="Description" v-model="newAd.description">
                  </div>
                  <div class="form-group">
                     <button class="btn btn-info btn-block btn-lg" @click="showAddF=false; addAd(); clearF();"><i class="fas fa-plus"></i> &nbsp; Add advertisement</button>
                  </div>
              </form>
            </div>
         </div>
      </div>
 </div>



    <!-- EDIT -->
    <div id="overlay" v-if="showEditF">
      <div class="modal-dialog">
         <div class="modal-content">
            <div class="modal-header">
               <h5 class="modal-title">Edit advertisement</h5>
                <button type="button" class="close" @click="showEditF=false">
                  <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <div class="modal-body p-4">
              <form action="#" method="post">
                 <div class="form-group">
                     <input type="text" name="id" class="form-control form-control-lg"  v-model="currentAdvertisement.id">
                  </div>
                  <div class="form-group">
                     <input type="text" name="city" class="form-control form-control-lg"  v-model="currentAdvertisement.city">
                     <!-- v-model="currentAdvertisement.city" -->
                  </div>
                    <div class="form-group">
                     <input type="text" name="street" class="form-control form-control-lg" v-model="currentAdvertisement.street">
                  </div>
                    <div class="form-group">
                     <input type="text" name="property" class="form-control form-control-lg" v-model="currentAdvertisement.property">
                  </div>
                    <div class="form-group">
                     <input type="text" name="price" class="form-control form-control-lg" v-model="currentAdvertisement.price">
                  </div>
                    <div class="form-group">
                     <input type="text" name="type" class="form-control form-control-lg" v-model="currentAdvertisement.type">
                  </div>
                    <div class="form-group">
                     <input type="text" name="description" class="form-control form-control-lg" v-model="currentAdvertisement.description">
                  </div>
                  <div class="form-group">
                     <button class="btn btn-info btn-block btn-lg" @click="showEditF=false; updateAd(); clearF();"><i class="far fa-edit"></i> &nbsp; Update advertisement</button>
                  </div>
              </form>
            </div>
         </div>
      </div>
    </div>


    <!-- DELETE -->
    <div id="overlay" v-if="showDeleteF">
      <div class="modal-dialog">
         <div class="modal-content">
            <div class="modal-header">
               <h5 class="modal-title">Delete advertisement</h5>
                <button type="button" class="close" @click="showDeleteF=false">
                  <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <div class="modal-body p-4">
              <h4 class="text-danger">Are you sure?</h4>
              <h5>You are deleting this advertisement!</h5>
              <hr>
              <button class="btn btn-danger btn-lg" @click="showDeleteF=false; deleteAd(); clearF();"><i class="fas fa-trash"></i> &nbsp; Yes</button> &nbsp;&nbsp;&nbsp;&nbsp;
              <button class="btn btn-success btn-lg" @click="showDeleteF=false"><i class="fas fa-undo"></i> &nbsp; No</button>
            </div>
         </div>
      </div>
    </div>



    <!-- DETAILS -->
    <div class="details" v-if="showDetailsF" :style="{ backgroundImage: `url('${backgroundran()}')` }">
      <div class="modal-dialog">
         <div class="modal-content">
            <div class="modal-header">Details:
               
                <button type="button" class="close" @click="showDetailsF=false">
                </button>
            </div>
            <div class="modal-body p-4">
              
              <hr>


              <ul class="text-center listdetails">
                  
                  <li> <b>City:</b> {{ currentAdvertisement.city }}</li>
                  <li> <b>Street:</b> {{ currentAdvertisement.street }}</li>
                  <li> <b>Property:</b> {{ currentAdvertisement.property }}</li>
                  <li> <b>Apartment:</b> {{ currentAdvertisement.apartment }}</li>
                  <li> <b>Price:</b> {{ currentAdvertisement.price }}</li>
                  <li> <b>Type:</b> {{ currentAdvertisement.type }}</li>
                  <li> <b>Description:</b> {{ currentAdvertisement.description }}</li>
                  <li> <b>Opinion:</b> Residents love this area very much <i class="fas fa-check-circle"></i></li>
                  <li> <b>Environment:</b> Quiet <i class="fas fa-check-circle"></i></li>
                  <li> <b>Close to the center:</b>&nbsp;<i class="fas fa-check-circle"></i></li>
              </ul>


              <hr>

              
              <button class="btn btn-success btn-warning" @click=" showDetailsF=false;" ><i class="fas fa-undo"></i> &nbsp;Return</button>
            </div>
         </div>
      </div>
    </div>


    
     <div class="container-fluid">
        <div class="row bg-secondary footerr">
            <div class="col-lg-12">
              <p class="text-center text-dark display-16 pt-8 ">Szymon Wojaczek &#174; </p>
            </div>
        </div>
      </div>



</div>



</template>




<script>
import axios from 'axios';
import anime from 'animejs/lib/anime.es.js';



var randomNumber = Math.floor(Math.random()*6+1);


export default {

  data() {
    return {

     background: require('@/assets/m'+randomNumber+'.jpg'),
     errorMsg: "",
     successMsg: "",
     showAddF: false,
     showEditF: false,
     showDeleteF: false,
     showDetailsF: false,
     advertisements: [],
     newAd: {city: "",street: "",property: "",apartment: "",price: "",type: "",description: ""},
     currentAdvertisement: {}

    }
    
  },


  methods: {
      getAllAd() {



         axios.get('http://localhost:3000/SzymonWojaczek').then((response) => {
        if(response.data.error) {
            this.errorMsg = response.data.message;

          }
          else {
             this.advertisements = response.data;
            
            //console.log(this.advertisements);
        
            
          }


        });

      },
    addAd() {


    axios.post('http://localhost:3000/SzymonWojaczek', this.newAd).then((response) =>{

          this.newAd = {city: "",street: "",property: "",apartment: "",price: "",type: "",description: ""};

        if(response.data.error) {
            this.errorMsg = "ERROR "; 
           

          }
          else {
            this.successMsg = "SUCCESS ";
           // console.log(this.advertisements);
            this.getAllAd();
         
          }


        });

      },
  
   updateAd() {
            let id = this.currentAdvertisement.id;
            // console.log(this.currentAdvertisement.id);
            axios.patch('http://localhost:3000/SzymonWojaczek/'+id, this.currentAdvertisement).then((response) =>{
                 
                 this.currentAdvertisement = {};

        if(response.data.error) {
            this.errorMsg = "ERROR "; 
           

          }
          else {
             this.successMsg = "SUCCESS ";
             console.log(this.advertisements);
             this.getAllAd();
         
          }


        });

      },
       deleteAd() {
            
            // console.log(this.currentAdvertisement.id);
            let id = this.currentAdvertisement.id;
            

            axios.delete('http://localhost:3000/SzymonWojaczek/'+id).then((response) =>{

              this.currentAdvertisement = {};

        if(response.data.error) {

            this.errorMsg = "ERROR "; 
           
        }
          else {
             this.successMsg = "SUCCESS ";
             this.getAllAd();
         
          }
     });
   },


       selectAd(advertisement) {
         this.currentAdvertisement = advertisement;
       },
       clearF() {
         this.errorMsg="";
         this.successMsg="";
       },
       backgroundran(){

         anime({
              targets: '.details',
              opacity:[0,1],
             translateY: [-500,0]
            });
         randomNumber = Math.floor(Math.random()*6+1);
         let background = require('@/assets/m'+randomNumber+'.jpg');

         return background;
       }
 
      
   },


    
  mounted: function() {
    
    this.getAllAd(); 
    
    
  },


}
</script>


<style lang="scss">

.table {
-webkit-box-shadow: 5px 5px 29px 5px rgba(0,0,0,0.15); 
box-shadow: 5px 5px 29px 5px rgba(0,0,0,0.15);
}

 #overlay{
   position: fixed;
   top: 0;
   bottom: 0;
   left: 0;
   right: 0;
   background: rgba(0,0,0,0.6);
   overflow: scroll;
    
 }

 @media(max-width: 1024px){

   .table{
     font-size:8px;
   }

 }

.listdetails{
  list-style-type:none;
 
}
.listdetails li{
   padding: 2%;
   border-top: 2px solid black;
}
.listdetails li:last-child{
   padding: 2%;
   border-bottom: 2px solid black;
}

.listdetails li b{
   margin-right: 1%;
}

.modal-dialog{
  opacity:0.85;
}
.footerr{
  margin-top:100px;
}


</style>
