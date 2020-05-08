<template>
<div id="second-table">
<v-data-table
:headers="headers"
:items="items">
<template #top>
<div class="top-div"><p class="display-1 white--text">Subcontracting
<span>
<v-tooltip bottom>
<template #activator="{ on }">
<v-btn id="add" class="white--text" @click="add" v-on="on"><v-icon class="black--text">add</v-icon></v-btn>
</template>
<span>add row</span>
</v-tooltip>
</span>
</p></div>
</template>
<template #item.Subcontracting="{item}">
  <td v-if="editable && editindex==items.indexOf(item)">
     <v-text-field class="tx1" v-model="Subcontracting"></v-text-field>
  </td>
  <td id="td1" v-else>{{item.Subcontracting}}</td>
</template>
<template #item.Units="{item}">
  <td v-if="editable && editindex==items.indexOf(item)">
     <v-text-field class="tx1" v-model="Units"></v-text-field>
  </td>
  <td id="td2" v-else>{{item.Units}}</td>
</template>
<template #item.Total_No_of_Units="{item}">
  <td v-if="editable && editindex==items.indexOf(item)">
     <v-text-field class="tx1" v-model="Total_No_of_Units" type="number"></v-text-field>
  </td>
  <td id="td3" v-else>{{item.Total_No_of_Units}}</td>
</template>
<template #item.Total_Unit_value="{item}">
  <td v-if="editable && editindex==items.indexOf(item)">
     <v-text-field class="tx1" v-model="Total_Unit_value" type="number"></v-text-field>
  </td>
  <td id="td4"  v-else>{{item.Total_Unit_value}}</td>
</template>
<template #item.Total_Total_cost="{item}">
<td v-if="editable && editindex==items.indexOf(item)"></td>
<td id="td5" v-else><v-chip color="blue">€{{item.Total_Total_cost}}</v-chip></td>
</template>
<template #item.year1_Units="{item}">
  <td v-if="editable && editindex==items.indexOf(item)">
     <v-text-field class="tx1" v-model="year1_Units"></v-text-field>
  </td>
  <td id="td2" v-else>{{item.year1_Units}}</td>
</template>
<template #item.Year1_No_of_Units="{item}">
  <td v-if="editable && editindex==items.indexOf(item)">
     <v-text-field class="tx1" v-model="Year1_No_of_Units" type="number"></v-text-field>
  </td>
  <td id="td6" v-else>{{item.Year1_No_of_Units}}</td>
</template>
<template #item.Year1_Unit_value="{item}">
  <td v-if="editable && editindex==items.indexOf(item)">
     <v-text-field class="tx1" v-model="Year1_Unit_value" type="number"></v-text-field>
  </td>
  <td id="td7" v-else>{{item.Year1_Unit_value}}</td>
</template>
<template #item.Year1_Total_cost="{item}">
<td v-if="editable && editindex==items.indexOf(item)"></td>
<td id="td8" v-else><v-chip color="blue">€{{item.Year1_Total_cost}}</v-chip></td>
</template>
<template  #item.Detailed_Explanation="{item}">
  <td v-if="editable && editindex==items.indexOf(item)">
     <v-text-field id="txt" @keydown="save($event,item,item.Total_Total_cost,item.Year1_Total_cost)" v-model="Detailed_Explanation"></v-text-field>
  </td>
  <td id="td" v-else>{{item.Detailed_Explanation}}</td>
</template>
<template #item.Actions="{item}">
<v-tooltip bottom>
<template #activator="{ on }">
<v-icon id="del" @click="deleteitem(item)"  v-on="on">delete</v-icon>
</template>
<span>delete</span>
</v-tooltip>
<v-tooltip bottom>
<template #activator="{ on }">
<v-icon id="edit" @click="edit(item)" v-on="on">edit</v-icon>
</template>
<span>edit</span>
</v-tooltip>
</template>
<template #body.append>
<tr>
<td>Subtotal</td>
<td></td>
<td></td>
<td></td>
<td id="Totalsum"><v-chip color="blue">€{{Totalsum}}</v-chip></td>
<td></td>
<td></td>
<td></td>
<td id="year1sum"><v-chip color="blue">€{{year1sum}}</v-chip></td>
<td></td>
<td></td>
</tr>
</template>
</v-data-table>
</div>
</template>
<script>
export default{
	data(){
	return{
	submitStatus:'',
	count:-1,
	editindex:null,
	editable:false,
	Total_No_of_Units:'',
	Total_Unit_value:'',
	Total_Total_cost:'',
	Year1_No_of_Units:'',
	Year1_Unit_value:'',
	Year1_Total_cost:'',
	Units:'',
	year1_Units:'',
	Subcontracting:'',
	Detailed_Explanation:'',
	Totalsum:0,
	year1sum:0,


	headers:[{text:'',value:'Subcontracting',sortable:false},
  {text:'',value:'Units',sortable:false},
  {text:'',value:'Total_No_of_Units',sortable:false},
  {text:'',value:'Total_Unit_value',sortable:false},
  {text:'',value:'Total_Total_cost',sortable:false},
  {text:'',value:'year1_Units',sortable:false},
  {text:'',value:'Year1_No_of_Units',sortable:false},
  {text:'',value:'Year1_Unit_value',sortable:false},
  {text:'',value:'Year1_Total_cost',sortable:false},
  {text:'',value:'Detailed_Explanation',sortable:false},
  {text:'',value:'Actions',sortable:false}],

  items:[]

	}
},
methods:{
add(){
  this.count=this.count+1
  this.editindex=this.count
  this.submitStatus='post'
  this.editable=true
  this.items.push({Subcontracting:'', Units:'',Total_No_of_Units:'',Total_Unit_value:'',Total_Total_cost:''
  ,year1_Units:'',Year1_No_of_Units:'',Year1_Unit_value:'',Year1_Total_cost:'',Detailed_Explanation:'',Actions:''})
  },
edit(item){
  let editindex = this.items.indexOf(item)
  this.editindex=editindex
  this.submitStatus='edit'
  this.editable=true
	},
deleteitem(item){
   this.count=this.count-1
   const index = this.items.indexOf(item)
   this.Totalsum=this.Totalsum-this.items[index].Total_Total_cost
   this.year1sum=this.year1sum-this.items[index].Year1_Total_cost
   this.items.splice(index, 1)
   this.$emit('subcontracting',{subtotal:this.Totalsum,year1sum:this.year1sum})
},
save(e,item,totalcost,year1cost){
  console.log(totalcost)
  console.log(year1cost)
  if(e.keyCode === 13 || e.keyCode== 9){
  const index=this.items.indexOf(item)
  this.items[index].Total_No_of_Units=this.Total_No_of_Units
  this.items[index].Total_Unit_value=this.Total_Unit_value
  this.items[index].Year1_No_of_Units=this.Year1_No_of_Units
  this.items[index].Year1_Unit_value=this.Year1_Unit_value
  this.items[index].Detailed_Explanation=this.Detailed_Explanation
  this.items[index].Subcontracting=this.Subcontracting
  this.items[index].Units=this.Units
  this.items[index].year1_Units=this.year1_Units

  if(this.items[index].Total_No_of_Units=='' || this.items[index].Total_Unit_value=='' )
  {
   this.Total_Total_cost=0
   this.items[index].Total_Total_cost=this.Total_Total_cost
  }
  else{
   this.Total_Total_cost=(this.Total_No_of_Units*this.Total_Unit_value)
   this.items[index].Total_Total_cost=this.Total_Total_cost
  }
   if(this.items[index].Year1_No_of_Units=='' || this.items[index].Year1_Unit_value=='' ){
     this.Year1_Total_cost=0
     this.items[index].Year1_Total_cost=this.Year1_Total_cost
   }
   else{
    this.Year1_Total_cost=(this.Year1_No_of_Units*this.Year1_Unit_value)
     this.items[index].Year1_Total_cost=this.Year1_Total_cost
   }


  if(this.submitStatus==='post'){
  this.Totalsum=this.Totalsum+this.items[index].Total_Total_cost
  this.year1sum=this.year1sum+this.items[index].Year1_Total_cost
  this.$emit('subcontracting',{subtotal:this.Totalsum,year1sum:this.year1sum})
  }

  if(this.submitStatus==='edit'){
  if(totalcost==0){
  console.log('enterd')
  this.Totalsum=this.Totalsum+this.items[index].Total_Total_cost
  this.$emit('subcontracting',{subtotal:this.Totalsum,year1sum:this.year1sum})
  }
  else{
  console.log('enterd2')
  this.Totalsum=(this.Totalsum-totalcost)
  this.Totalsum=this.Totalsum+this.items[index].Total_Total_cost
  this.$emit('subcontracting',{subtotal:this.Totalsum,year1sum:this.year1sum})
  }
  if(year1cost==0){
  console.log('enterd')
  this.year1sum=this.year1sum+this.items[index].Year1_Total_cost
  this.$emit('subcontracting',{subtotal:this.Totalsum,year1sum:this.year1sum})
  }
  else{
   console.log('enterd4')
  this.year1sum=(this.year1sum-year1cost)
  this.year1sum=this.year1sum+this.items[index].Year1_Total_cost
  this.$emit('subcontracting',{subtotal:this.Totalsum,year1sum:this.year1sum})
  }
  }
   this.editable=false

  this.Total_No_of_Units=''
  this.Total_Unit_value=''
  this.Year1_No_of_Units=''
  this.Year1_Unit_value=''
  this.Detailed_Explanation=''
  this.Year1_Total_cost=''
  this.Total_Total_cost=''
  this.Personalcosts=''
  this.year1_Units=''
  this.Units=''

  }
}
},
computed:{
}
}
</script>

<style scopped>
#second-table th:nth-child(1){
width:300px !important;
}
.top-div{
  height:50px;
  background-color:grey;
}
#add{
position:absolute;
left:93%;
margin-top:5px;
}
.heading{
	font-size:2.5em;
}
#edit{
  margin-left:2px;
}
#td{
	width:450px !important;
}
#Totalsum{
	padding-left:30px;
}
#year1sum{
	padding-left:32px;
}
.tx1{
	width:50px;
}
#txt{
	width:100px;
}

</style>