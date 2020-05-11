<template>
<v-container fluid id="top-container">
<v-data-table class="elevation-1"
hide-default-header="true" 
hide-default-footer="true"
>
<template #top>
<div id="top-table-no-data" class="display-1">Project Budjet (Threatend Species Grant)</div>
<v-btn id="addTop" class="white--text" @click="dialog=true" v-on="on"><v-icon class="black--text">add</v-icon></v-btn>
</template>
<template #no-data>
<div class="project">
<p >Project Name:<span v-if="form1">{{ProjectName}}</span><span v-if="form2">{{ProjectName2}}</span></p>
<p>Project Code:<span v-if="form1">{{ProjectCode}}</span><span v-if="form2">{{ProjectCode2}}</span></p>
<p>Lead Organization:<span v-if="form1">{{LeadOrganization}}</span><span v-if="form2">{{LeadOrganization2}}</span></p>
</div>
</template>
<template #body.append>
<v-data-table
class="elevation-1"
:headers="headers"
 hide-default-footer="true">
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
<td>Subtotal-Eligible-Cost</td>
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
<td>Indirect-Cost</td>
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
<td>Total-Project-Budjet</td>
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
<td>Total-Sos-Funding-Requested</td>
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
<td>Percentage-Co-Financing</td>
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
</template>
</v-data-table>
<v-dialog
      v-model="dialog"
      max-width="390"
    >
    <v-card class="card">
    <v-toolbar>
    <v-tabs fixed-tabs background-color="grey" dark>
    <v-tab  @click="form1=true,form2=false"> New Project </v-tab>
    <v-tab  @click="form2=true,form1=false"> Projects </v-tab>
    </v-tabs> 
    </v-toolbar>
    <v-form v-show="form1" class="form" ref="form1">
    <v-text-field v-model="ProjectName" label="Project Name" :rules="Rules.ProjectNamerule" required></v-text-field>
    <v-text-field class="input" label="Project Code" v-model="ProjectCode" :rules="Rules.ProjectCodeule" required></v-text-field>
    <v-text-field class="input" v-model="LeadOrganization" :rules="Rules.LeadOrganizationrule" label="Lead Organization"></v-text-field>
    <v-btn  color="success" id="submitbtn" class="mr-4" @click="submit">Submit</v-btn>
    </v-form>
    <v-form v-show="form2" class="form" ref="form2">
    <v-select label="Project Code" v-model="ProjectCode2" :items="Pcodes" @change="selector" :rules=" Rules.ProjectCode2 " required></v-select>
    <v-card>
    <v-card-text>
    <p class=" card-text text--primary">Project Name: {{ProjectName2}}</p>
    <p class=" card-text text--primary">Lead Organization: {{LeadOrganization2}}</p>
    </v-card-text>
    </v-card>
    <v-btn  color="success" id="submitbtn2" class="mr-4" @click="submit2">Submit</v-btn>
    </v-form>
    </v-card>
    </v-dialog>
</v-container>
</template>


<script>
import _ from 'underscore'
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
  form1:true,
  from2:false,
  ProjectName:'',
  ProjectCode:'',
  LeadOrganization:'',
  ProjectName2:'',
  ProjectCode2:'',
  LeadOrganization2:'',
  dialog:false,
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
  errmsg:'',
   
  Projects:[{Projectnames:'sos', ProjectCodes:1,LeadOrganizations:'jkl'},
            {Projectnames:'pos', ProjectCodes:2,LeadOrganizations:'jfj'}],
  Pcodes:[1,2],


  Rules:{
  ProjectNamerule:[()=> !this.Pnamerule(this.ProjectName) || 'Project name already registerd ' ],
  ProjectCodeule:[()=> !this.Pcoderule(this.ProjectCode) || 'Project code already registerd'],
  LeadOrganizationrule:[()=> !this.Porganizationrule(this.LeadOrganization) || 'Organization already registerd'],
  ProjectCode2:[v=> !!v || 'required']
  },

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
  },
  submit(){
  if(this.$refs.form1.validate()){
  console.log('sucess')
  }
  else{
  console.log('failed')
  console.log(_.isMatch(this.Projects[0], {Projectnames:'s'}))
  }
  },
  submit2(){
  if(this.$refs.form2.validate()){
  console.log('sucess')
  }
  else{
  console.log('failed')
  }
  },
  Pnamerule(v){
  for(var i=0;i<this.Projects.length;i++){
  if(v ===_.property('Projectnames')(this.Projects[i])){
  return true
  }
  }
  },
  Porganizationrule(v){
  for(var i=0;i<this.Projects.length;i++){ 
  if(v ===_.property('LeadOrganizations')(this.Projects[i])){
  return true
  }
  }
  },
  Pcoderule(v){
  for(var i=0;i<this.Projects.length;i++){ 
  if(parseInt(v) ===_.property('ProjectCodes')(this.Projects[i])){
  return true
  }
  }
  },
  selector(){
  let Pname2=_.where(this.Projects, {ProjectCodes:this.ProjectCode2})
  this.ProjectName2=Pname2[0].Projectnames
  this.LeadOrganization2=Pname2[0].LeadOrganizations
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
.card-text{
  font-size:1.5em;
}
#submitbtn{
margin-left:150px;
margin-bottom:10px;
}
#submitbtn2{
  margin-left:150px;
  margin-top:5px;
margin-bottom:5px;
}
.form{
padding:10px;
}
#addTop{
  position:absolute;
  top:14px;
  right:2%;
}
.project{
  
  font-size:1.5em;
  width:100%;

}
.project p{
color:black;
margin-bottom:5px !important;
width:50%;
}
#top-table-no-data{
  text-align:center;
  color:white;
  background-color:grey;
  width:100%;
  padding-left:0px;
  padding-right:0px;
}
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
.project span{
  font-size:1em;
  margin-left:10px;
}
.project{
  text-align:centre;
}
</style>