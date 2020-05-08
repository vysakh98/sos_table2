<template>
<v-container fluid id="top-container">
<v-data-table
class="elevation-1"
:headers="headers">
<template #top>
<div id="headers">
<h1 id="TotalProject">TotalProject</h1>
<h1 id="year1">Year1</h1>
</div>
</template>
<template #no-data>
<tr>
 <td colspan="10" id="personalSelector1">
   <v-app-bar-nav-icon class="personalSelectoricon" @click="Personalcostshow=!Personalcostshow , PersonalcostSpan=!PersonalcostSpan" ></v-app-bar-nav-icon>
   <span>PersonalCost</span>
   <span  v-show="PersonalcostSpan"> <v-chip id="subtotalspan1" class="">Total Personal Cost: €{{personalcostTotal}}</v-chip> </span>
   <span  v-show="PersonalcostSpan"><v-chip id="subtotalspan2" class=""> Year1 Personal Cost: €{{personalcostyear1total}} </v-chip> </span>
 </td>
</tr>
</template>
<template #body.append="{headers}">
<tr v-show="Personalcostshow" :colspan="headers.length">
 <td :colspan="headers.length" id="table-td">
   <Personalcosts v-on:personalcost="personalcost($event)"></Personalcosts>
 </td>
</tr>
<tr>
 <td :colspan="headers.length" class="selector">
   <div class="personalSelector">
   <v-app-bar-nav-icon class="personalSelectoricon" @click="Subcontractingshow=!Subcontractingshow , subcontractingSpan=!subcontractingSpan" ></v-app-bar-nav-icon>
   <span>Subcontracting</span>
   <span class="subtotalspan" v-show="subcontractingSpan"> <v-chip class="">Total Subcontracting Cost: €{{contractingcost}}</v-chip> </span>
   <span class="subtotalspan" v-show="subcontractingSpan"><v-chip class=""> Year1 Subcontracting Cost : €{{year1contractingcost}} </v-chip> </span>
   </div>
 </td>
</tr>
<tr v-show="Subcontractingshow" :colspan="headers.length">
 <td :colspan="headers.length" id="table-td">
   <subContracting v-on:subcontracting="subcontracting($event)"></subContracting>
 </td>
</tr>
<tr>
 <td :colspan="headers.length" class="selector">
   <div class="personalSelector">
   <v-app-bar-nav-icon class="personalSelectoricon" @click="Localofficeshow=!Localofficeshow,
   localofficecostSpan=!localofficecostSpan" ></v-app-bar-nav-icon>
   <span>Local office</span>
    <span  v-show="localofficecostSpan"> <v-chip class="subtotalspan">Total Local Office Cost: €{{localofficeTotal}}</v-chip> </span>
   <span  v-show="localofficecostSpan"><v-chip  class="subtotalspan"> Year1 Local Office Cost: €{{loclaofficeyear1total}} </v-chip> </span>
   </div>
 </td>
</tr>
<tr v-show="Localofficeshow" :colspan="headers.length">
 <td :colspan="headers.length" id="table-td">
   <Localoffice v-on:localofficecost="localofficecost($event)"></Localoffice>
 </td>
</tr>
<tr>
 <td :colspan="headers.length" class="selector">
   <div class="personalSelector">
   <v-app-bar-nav-icon class="personalSelectoricon" @click="projectSuppliesshow=!projectSuppliesshow,projectsuppliesSpan=!projectsuppliesSpan" ></v-app-bar-nav-icon>
   <span>projectSupplies</span>
   <span  v-show="projectsuppliesSpan"> <v-chip class="subtotalspan">Total Project Supplies Cost: €{{suppliescost}}</v-chip> </span>
   <span  v-show="projectsuppliesSpan"><v-chip  class="subtotalspan"> Year1 Local Office Cost: €{{year1suppliescost}} </v-chip> </span>
   </div>
 </td>
</tr>
<tr v-show="projectSuppliesshow" :colspan="headers.length">
 <td :colspan="headers.length" id="table-td">
   <projectSupplies v-on:projectsupplies="supplies($event)"></projectSupplies>
 </td>
</tr>
<tr>
 <td :colspan="headers.length" class="selector">
   <div class="personalSelector">
   <v-app-bar-nav-icon class="personalSelectoricon" @click="projectequipmentMaintenenseshow=!projectequipmentMaintenenseshow,projectequipmentMaintenensesSpan=!projectequipmentMaintenensesSpan" ></v-app-bar-nav-icon>
   <span>project equipment maintenense</span>
    <span  v-show="projectequipmentMaintenensesSpan"> <v-chip class="subtotalspan">Total Equipment Maintenense Cost: €{{maintanenececost}}</v-chip> </span>
   <span  v-show="projectequipmentMaintenensesSpan"><v-chip  class="subtotalspan"> Year1 Equipment Maintenense  Office Cost: €{{year1maintanence}} </v-chip> </span>
   </div>
 </td>
</tr>
<tr v-show="projectequipmentMaintenenseshow" :colspan="headers.length">
 <td :colspan="headers.length" id="table-td">
   <projectequipmentMaintenense v-on:projectequipment="maintanenece($event)"></projectequipmentMaintenense>
 </td>
</tr>
<tr>
 <td :colspan="headers.length" class="selector">
   <div class="personalSelector">
   <v-app-bar-nav-icon class="personalSelectoricon" @click="Travleshow=!Travleshow,
   TravleshowSpan=!TravleshowSpan" ></v-app-bar-nav-icon>
   <span>Travel</span>
   <span  v-show="TravleshowSpan"> <v-chip class="subtotalspan">Total Travel Cost: €{{travelcost}}</v-chip> </span>
   <span  v-show="TravleshowSpan"><v-chip  class="subtotalspan"> Year1 Travel Cost: €{{yaer1travelcost}} </v-chip> </span>
   </div>
 </td>
</tr>
<tr v-show="Travleshow" :colspan="headers.length">
 <td :colspan="headers.length" id="table-td">
   <Travel v-on:Travel="travel($event)"></Travel>
 </td>
</tr>
<tr>
 <td :colspan="headers.length" class="selector">
   <div class="personalSelector">
   <v-app-bar-nav-icon class="personalSelectoricon" @click="Meeting_and_workshopsshow=!Meeting_and_workshopsshow,MeetingndworkshopsSpan=!MeetingndworkshopsSpan"></v-app-bar-nav-icon>
   <span>Meeting and workshops</span>
   <span  v-show="MeetingndworkshopsSpan"> <v-chip class="subtotalspan">Total Meeting And Workshops  Cost: €{{workshopscostTotal}}</v-chip> </span>
   <span  v-show="MeetingndworkshopsSpan"><v-chip  class="subtotalspan"> Year1 Meeting And Workshops  Cost: €{{workshopscostyear1total}} </v-chip> </span>
   </div>
 </td>
</tr>
<tr v-show="Meeting_and_workshopsshow" :colspan="headers.length">
 <td :colspan="headers.length" id="table-td">
   <meetingandworkShops v-on:workshopscost="workshopscost($event)"></meetingandworkShops>
 </td>
</tr>
<tr>
<td>subtotal-eligible-cost</td>
<td></td>
<td></td>
<td></td>
<td><v-chip color="blue">€{{subtotalEligibleCost}}</v-chip></td>
<td></td>
<td></td>
<td></td>
<td ><v-chip color="blue year1">€{{subtotalEligibleCostyear1}}</v-chip></td>
<td></td>
<td></td>
</tr>
<tr>
<td>indirect-cost</td>
<td></td>
<td></td>
<td></td>
<td><v-chip color="blue">€{{indirectCost}}</v-chip></td>
<td></td>
<td></td>
<td></td>
<td ><v-chip color="blue year1">€{{indirectcostYear1}}</v-chip></td>
<td></td>
<td></td>
</tr>
<tr>
<td>total-project-budjet</td>
<td></td>
<td></td>
<td></td>
<td><v-chip color="blue">€{{totalprojectBudjet}}</v-chip></td>
<td></td>
<td></td>
<td></td>
<td><v-chip color="blue year1">€{{totalprojectBudjetYear1}}</v-chip></td>
<td></td>
<td></td>
</tr>
<tr>
<td>tota-sos-funding-requested</td>
<td></td>
<td></td>
<td></td>
<td><v-chip color="blue">€70000</v-chip></td>
<td></td>
<td></td>
<td></td>
<td><v-chip color="blue year1">€26578</v-chip></td>
<td></td>
<td></td>
</tr>
<tr>
<td>percentage-co-financing</td>
<td></td>
<td></td>
<td></td>
<td><v-chip color="blue">52%</v-chip></td>
<td></td>
<td></td>
<td></td>
<td><v-chip color="blue year1">52%</v-chip></td>
<td></td>
<td></td>
</tr>
</template>
</v-data-table>
</v-container>
</template>


<script>
import Personalcosts from '@/components/Personalcosts.vue'
import subContracting from '@/components/subContracting.vue'
import Localoffice from '@/components/localofficeCost.vue'
import projectSupplies  from '@/components/projectSupplies.vue'
import projectequipmentMaintenense  from '@/components/projectequipmentMaintanense.vue'
import meetingandworkShops  from '@/components/meetingandworkShops.vue'
import Travel  from '@/components/Travel.vue'
export default{
  data(){
  return{
  personalcostTotal:0,
  personalcostyear1total:0,
  localofficeTotal:0,
  loclaofficeyear1total:0,
  workshopscostTotal:0,
  workshopscostyear1total:0,
  travelcost:0,
  yaer1travelcost:0,
  contractingcost:0,
  year1contractingcost:0,
  suppliescost:0,
  year1suppliescost:0,
  maintanenececost:0,
  year1maintanence:0,
  Personalcostshow:false,
  Subcontractingshow:false,
  Localofficeshow:false,
  projectSuppliesshow:false,
  Travleshow:false,
  projectequipmentMaintenenseshow:false,
  Meeting_and_workshopsshow:false,
  PersonalcostSpan:true,
  subcontractingSpan:true,
  localofficecostSpan:true,
  projectsuppliesSpan:true,
  TravleshowSpan:true,
  MeetingndworkshopsSpan:true,
  projectequipmentMaintenensesSpan:true,
  headers:[{text:'Budget categories',value:'',sortable:false},
  {text:'Units',value:'',sortable:false},
  {text:'No_of Units',value:'',sortable:false},
  {text:'Unit_value',value:'',sortable:false},
  {text:'Total_cost','value':'',sortable:false},
  {text:'Units',value:'',sortable:false},
  {text:'No_of Units',value:'',sortable:false},
  {text:'Unit_value',value:'',sortable:false},
  {text:'Total_cost',value:'',sortable:false},
  {text:'Detailed Explanation and justification',value:'',sortable:false},
  {text:'',value:'',sortable:false}],
  }
  },
  components:{
  'Personalcosts':Personalcosts,
  'subContracting':subContracting,
  'Localoffice':Localoffice,
  'projectSupplies':projectSupplies,
  'projectequipmentMaintenense':projectequipmentMaintenense ,
  'Travel':Travel,
  'meetingandworkShops':meetingandworkShops
  },
  methods:{
  personalcost(e){
  console.log(e)
  this.personalcostTotal=e.subtotal
  this.personalcostyear1total=e.year1sum
  },
  localofficecost(e){
  this.localofficeTotal=e.subtotal
  this.loclaofficeyear1total=e.year1sum
  },
  workshopscost(e){
  this.workshopscostTotal=e.subtotal
  this.workshopscostyear1total=e.year1sum
  },
  maintanenece(e){
  this.maintanenececost=e.subtotal
  this.year1maintanence=e.year1sum
  },
  supplies(e){
  this.suppliescost=e.subtotal
  this.year1suppliescost=e.year1sum
  },
  subcontracting(e){
  this.contractingcost=e.subtotal
  this.year1contractingcost=e.year1sum
  },
  travel(e){
   this.travelcost=e.subtotal
   this.yaer1travelcost=e.year1sum
  }
  },
computed:{
 subtotalEligibleCost(){
  return this.personalcostTotal+this.localofficeTotal+this.workshopscostTotal+this.travelcost+this.contractingcost+this.suppliescost+this.maintanenececost
 },
 subtotalEligibleCostyear1(){
 return this.personalcostyear1total+this.loclaofficeyear1total+this.workshopscostyear1total+this.yaer1travelcost+this.year1contractingcost+this.year1suppliescost+this.year1maintanence
 },
 indirectCost(){
  return Math.round((this.personalcostTotal+this.localofficeTotal+this.workshopscostTotal+this.travelcost+this.contractingcost+this.suppliescost+this.maintanenececost)*0.7)
 },
 indirectcostYear1(){
  return Math.round((this.personalcostyear1total+this.loclaofficeyear1total+this.workshopscostyear1total+this.yaer1travelcost+this.year1contractingcost+this.year1suppliescost+this.year1maintanence)*0.7)
 },
 totalprojectBudjet(){
  return Math.round((this.personalcostTotal+this.localofficeTotal+this.workshopscostTotal+this.travelcost+this.contractingcost+this.suppliescost+this.maintanenececost)+((this.personalcostTotal+this.localofficeTotal+this.workshopscostTotal+this.travelcost+this.contractingcost+this.suppliescost+this.maintanenececost)*0.7))
 },
 totalprojectBudjetYear1(){
  return Math.round((this.personalcostyear1total+this.loclaofficeyear1total+this.workshopscostyear1total+this.yaer1travelcost+this.year1contractingcost+this.year1suppliescost+this.year1maintanence)+((this.personalcostyear1total+this.loclaofficeyear1total+this.workshopscostyear1total+this.yaer1travelcost+this.year1contractingcost+this.year1suppliescost+this.year1maintanence)*0.7))
 }
}
}

</script>


<style>
.subtotalspan{
  border-radius:15px;
  margin-left:20px;
  padding:5px 5px;
  font-size:1.5em;
}
#subtotalspan1{
  border-radius:15px;
  margin-left:20px;
  padding:5px 5px;
  font-size:1.0em;
}
#subtotalspan2{
  border-radius:15px;
  margin-left:20px;
  padding:5px 5px;
  font-size:1.0em;
}
#year1{
}
#personalSelector1{
padding-left:0px;
font-size:1.5em;
color:black;
}
#TotalProject{
  background-color:grey;
  color:white;
  padding-left:20%;
  width:46.6%;
  display:inline-block;
  border-right:2px solid black;
}
#year1{
  color:white;
  width:53.4%;
  padding-left:20%;
  background-color:grey;
  display:inline-block;
}
#table-td{
  padding-left:0px;
  padding-right:0px;
  border:1px solid black;

}

#top-container th{
  width:800px;
}
#top-container td{
}

#top-container th:nth-child(9){
  width:900px !important;
}

.elevation-1{
  border:1px solid black;
}
.selector{
  padding-left:0px;
  padding-right:0px;
}
.personalSelector span{
font-size:1.5em;
padding-left:5px;
color:black;
}
.personalSelectoricon{
  padding-bottom:5px;
  margin-right:0px;
}
.year1{
  margin-left:15px;
}
</style>