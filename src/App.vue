<template>
  <div id="app">
      <h1 class="perttyText ">
        FIRST PROJECT
      </h1>
      <hr>

      <div class="section1">
         <div class="perttyText2 "> Section 1  :</div>
         <div class="changeNumber">
            <button class="buttons" @click="changeNumber('+')">+</button>
            <span class="perttyText">{{ num }}</span>
            <button class="buttons" @click="changeNumber('-')">-</button>
         </div>
         <div class="mathOperation" >
            <button class="buttons" @click="squareRoot()" > square root </button>
            <button class="buttons" @click="powerOfThree()"> power of three </button>
            <button class="buttons" @click="changSign()"> changSign </button>
            <button class="buttons" @click="reset()"> reset </button>
         </div>
      </div>

      <hr>
      <div class="section2">
         <span class="perttyText2 ">Section 2 :</span>

         <div class="formSection">
            <img src="@/assets/premium_photo-1661576416945-21d2f4608e26.avif" alt="weightlifting">
            <div>
               <form  @submit.prevent="addRecord()" class="myForm">
                  <label  class="perttyText2" for="Record">enter your Record : </label>
                  <input  id="Record" min="0" type="number" v-model="numberOfRecords"  />
                  <button class="buttons buttonsForm" >Add Record</button>
               </form>
            </div>
         </div>

         <div class=" tables">
            <table class="tabelRecords">
               <thead>
                  <tr >
                     <th id="theadRow">Rows</th>
                     <th id="theadRecord">Records</th>
                  </tr>
               </thead>
               <tbody>
                  <tr v-for="(record, i) in records" :key="i">
                     <td>{{ i + 1 }}</td>
                     <td>{{ record }}</td>
                  </tr>
               </tbody>
            </table>
            <div class="Avg">
                 <div>Average: {{ average }}</div>
            </div>
         </div>
      </div>
      <hr>
      <div class="section3">
         <span class="perttyText2 ">Section 3 :</span>
         
         <div>
            <h1 class="perttyText">Products</h1>
            <div v-if="!showProducts">
               <div class="loader">
                  <div class="lds-ellipsis">
                     <div>
                     </div>
                     <div>
                     </div>
                     <div>
                     </div>
                     <div>
                     </div>
                     </div>
               </div>
            </div>
            <div class="products" v-else>
               <div  v-for="i in products" :key="i">
                  <div class="card">
                     <div class="card-image">
                        <img :src="i.image" alt="">
                     </div>
                     <div class="card-content">
                        <p class="title"> {{ i.title }}</p>
                        <p class="subtitle">{{ i.price }}</p>
                     </div>
                  </div>
               </div>
            </div>
         </div>      
      </div>


      <hr>
      <div class="section4">
         <span class="perttyText2 ">Section 4 :</span>
          <div class="boxAnim">
               <div id="anim" :class="{ 'anim': showAnim }" ></div>
               <button class="buttons" @click="toggleSituation()" >Change Situation</button>
          </div>
      </div>

      <hr>
      <div class="section3">
         <span class="perttyText2 ">Section 5 :</span>
         
         <div>
            <h1 class="perttyText">:style=" "</h1>

            <div class="test" :style="{fontSize : testPluse + 'px' , color : testPluse>=24 ? 'purple' : '#1A5D1A'}">  <!-- , backgroundColor: testPluse>20 ? 'pink' :'rgb(250, 227, 146)' -->
               this is test 123
               
               <button class="buttons buttonTest" @click="plus()" >{{ testPluse }}</button>
            </div>
            
            
         </div>
     
      </div>
      
  </div>  
</template>

<script>

export default {
   data() {
      return {
         num: 15,
         numberOfRecords : 0,
         records :[],
         average:0,
         products: [],
         showProducts: false,
         showAnim : true,
         testPluse : 14,

      }
   },
   methods: {
      changeNumber(input) {
         if (input === '+') {
         this.num++;
         } else if (input === '-') {
         this.num--;
         }
      },
      squareRoot(){
         this.num = Math.sqrt(this.num);
      },
      powerOfThree(){
         this.num = this.num ** 3;
      },
      changSign(){
         this.num = this.num * -1 ;
      },
      reset(){
         this.num = 15;
      },
      addRecord() {
        this.records.push(this.numberOfRecords);
    },
    toggleSituation(){
         this.showAnim = !this.showAnim;
    },
    plus(){
       this.testPluse ++
    }

   },
   watch: {
      numberOfRecords(newValue) {
         let sum = 0;
         if (this.records.length > 0) {
            for (let i = 0; i < this.records.length; i++) {
               sum += parseInt(this.records[i]);
            }
            sum +=parseInt(newValue);
            this.average = parseInt(sum / (this.records.length + 1));
            console.log(sum); 
            console.log(this.records); 
            
         }
      }
   },
 mounted() {
    setTimeout(() => {
      this.products = [
        {
          title: 'محصول کت گلیمی 6055 ( پیش فروش 5 )',
          price: '۸۹۹.۰۰۰ تومان ',
          image: 'https://api.elinorboutique.com/storage/dac04d73-6ab9-4867-b69c-f99e0730fc2c/variety-24717.webp'
        },
        {
          title: 'شومیز ساده 6729',
          price: '۲۹۹.۰۰۰ تومان ',
          image: 'https://api.elinorboutique.com/storage/8462759a-dfe9-4457-be95-4a8c8bb634ca/product-2965.webp'
        },
        {
          title: 'شومیز 5401',
          price: '۶۶۹.۰۰۰ تومان ',
          image: 'https://api.elinorboutique.com/storage/0fe48d23-347c-4aaa-b569-8f8c71d764f7/variety-25140.webp'
        }
      ];
      this.showProducts = true;
    }, 5000)
  },


}
</script>

<style>
   #app
   {
      width: 1200px;
      background-color: #FFF2F2;
      margin: auto;
      padding: 20px;
      
   }
   .perttyText{
      color: #7286D3;
      text-shadow: 2px 2px 0 #ffffff, 4px 4px 0 #E5E0FF;
      text-align: center;
      margin-bottom: 60px;
      font-size: 34px;
   }
    .perttyText2{
      color: #7286D3;
      text-shadow: 2px 2px 0 #ffffff, 4px 4px 0 #E5E0FF;
      font-size: 24px;
      
   }
   hr{
      color: #E5E0FF;
   }
   .buttons {

       color: #7286D3;
       background-color: #E5E0FF;
       margin: 20px;
       font-size: 24px;
       border: 2px solid #7286D3;
       border-radius: 6px;
   }
   .buttons:hover{
      background-color: #8ea6e96e;
      transition: 0.5s;
      cursor: pointer;
   }
   .changeNumber{
      font-size: 30px;
      font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
      text-align: center;
   }
   .changeNumber button{
      width: 50px;
      height: 50px;
   }
   .mathOperation{
      display: flex;
      justify-content: center;
      padding-top: 50px;
   }
   .mathOperation button{
      width: 300px;
      padding: 10px;
     
      
   }

   .formSection{
      background: #E5E0FF;
      width: 500px;
      text-align:  center;
      margin: auto;
      padding: 30px;
      border-radius: 9px;display: flex;
      width: 700px;
      height: 250px;
   }
   .formSection img{
      width : 48%;
      border-radius: 90px;      
   }
   .myForm{
      
      height:250px;
      width: 300px;
      margin-left: 50px;
      padding-left: 10px;
      display: flex;
      flex-direction: column;
      justify-content: center;
   }
   #Record{
      padding: 7px;
      margin: 20px;
      width: 230px;
      border-radius: 4px;
      border: 2px solid #7286D3;
   }
   .myForm label{
      text-align: left;
      padding-left:22px;
   }
   .buttonsForm{
      background: #7286D3;
      color:#FFF2F2 ;
      width: 244px;
      
   }

   .tables{
      display: flex;
      justify-content: center;
      margin: 100px;
   }
   .tabelRecords{
      border: 2px solid #7286D3;
      padding: 20px; 
      width:400px;
      margin: 0px 30px 0px 0px;
      border-radius: 10px;
   }
   .tabelRecords th{
      border-bottom: 2px solid #7286D3;
      padding:10px  20px;
      color: #FFF2F2;
      background-color: #7286D3;
   }
   .tabelRecords td{
      border-bottom: 1px solid #7286D3;
      padding:10px  20px;
      color: #2d3e80;
      text-align: center;
      background-color: #E5E0FF;
      font-size: 16px;

   }
   #theadRow{
      width:50px;
   }
   .Avg {
      border: 2px solid #7286D3;
      width: 300px;
      border-radius: 10px;
      height: 90px;
      text-align: center;
      color: #7286D3;
      font-size: 24px;
      align-items: center;
   }
   .Avg div{
      margin-top: 33px;
   }


.section3{
   margin-bottom: 80px;
}

.products{
   display: flex;  
   justify-content: space-around;
}
  .card {
  border: 1px solid #8EA7E9;
  background-color: #E5E0FF;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 10px;
  width: 300px;
}

.card-image img {
  max-width: 100%;
  height: auto;
}

.title {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 5px;
   color: #48568f;
   text-align: right;
}

.subtitle {
  font-size: 18px;
  color: #7286D3;
}

.loader{
   align-items: center;
   text-align: center;
   width: 200px;
   margin: auto;
}

.lds-ellipsis {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ellipsis div {
  position: absolute;
  top: 33px;
  width: 13px;
  height: 13px;
  border-radius: 50%;
  background: #7286D3;
  animation-timing-function: cubic-bezier(0, 1, 1, 0);
}
.lds-ellipsis div:nth-child(1) {
  left: 8px;
  animation: lds-ellipsis1 0.6s infinite;
}
.lds-ellipsis div:nth-child(2) {
  left: 8px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(3) {
  left: 32px;
  animation: lds-ellipsis2 0.6s infinite;
}
.lds-ellipsis div:nth-child(4) {
  left: 56px;
  animation: lds-ellipsis3 0.6s infinite;
}
@keyframes lds-ellipsis1 {
  0% {
    transform: scale(0);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes lds-ellipsis3 {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(0);
  }
}
@keyframes lds-ellipsis2 {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(24px, 0);
  }
}




/******************** */

#anim {
  width: 100px;
  height: 100px;
  background-color: #7286D3;
  border-radius: 10px;
  position: relative;
}

.anim{
   animation-name: move, color, rotate;
  animation-iteration-count: 3, 5, infinite;
  animation-duration: 3s, 3s, 3s;
  animation-timing-function: ease, ease, linear; 
}
@keyframes move {
  0%   { left: 0px; }
  50%  { left: 200px; }
  100% { left: 0px; }
}

@keyframes color {
  0%   { background-color: #7286D3; }
  50%  { background-color: #E5E0FF; }
  100% { background-color: #7286D3; }
}

@keyframes rotate {
    from { transform:rotate(0deg); }
    to { transform:rotate(360deg); }
}


.boxAnim{
   width: 800px;
   margin:60px auto;
   display: flex;
   justify-content: space-between;
}

.boxAnim button{
   align-items: right;
   width: 250px;
   height: 50px;
}




.test{
   border :2px solid #7286D3;
   width: 400px;
   height: 200px;
   margin: auto;
   border-radius: 19px;
   padding: 40px;
   box-sizing: border-box;
   position: relative;

}

.buttonTest{
   width: 90px;
   position: absolute;
   bottom: 0px;
   right: 0px;
}























</style>
