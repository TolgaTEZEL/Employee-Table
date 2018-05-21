<template>

<div  > 
  
	<h1>Fsm  İnsan Kaynaklarıabcbas </h1>			
  
  <br/>
<br/>
<label style = "float:left" > Ad: </label>
<input id="i2" type= "text" maxlength="20"  required style = "float:left;width:200px;height:15px;font-size:14px;margin-left:27px;" /> 

<br/>
<br/>
<label style = "float:left" > Soyad: </label>
<input id="i3" type= "text" required style = "float:left;width:200px;height:15px;font-size:14px;margin-left:5px;"/> 
<br/>
<br/>

<label style = "float:left" > Departman: </label>
<select id="i4" required style = "float:left;width:200px;height:20px;font-size:14px;margin-left:5px;">
   <option value="sc">Seçiniz</option>
  <option value="Tekniker">Tekniker</option>
  <option value="Mühendis">Mühendis</option>
  <option value="Memur">Memur</option>
  <option value="Uzman">Uzman</option>
</select>
<br/>
<br/>
<label style = "float:left" > Maaş: </label>
<input id="i5" type= "number" required pattern="[0-9]{3,4}"  required style = "float:left;width:200px;height:15px;font-size:14px;margin-left:25px;" /> 
<br/>
<br/>

<button v-on:click="add()"  required style = "float:left;width:50px;height:25px;margin-left:0px;"> Ekle</button> 

<button v-on:click="updt()"  required style = "float:left;width:80px;height:25px;margin-left:10px;"> Güncelle</button> 

<button v-on:click="ara()"  required style = "float:left;width:80px;height:25px;margin-left:10px;"> Ara</button> 
<button @click="yenile()"  required style = "float:left;width:130px;height:25px;margin-left:10px;"> Tabloyu Yenile</button>


<input type="button" value="Olay Günlüğünü Görüntüle"  required style = "float:left;width:180px;height:25px;margin-left:10px;" id="i6" @click="change()"/></input> 
<br/>
<br/>





 <h4 required style ="float:left;margin-left:300px;"> Personel Tablosu </h4> 


<h4  id = "i7" required style ="float:right;margin-right:300px;visibility: hidden;"> Olay Günlüğü </h4> 
<br/>
<br/>
<br/>
<br/>





<table id="firstTable"  >
  <thead>
    <tr>
      <th>ID</th>
      <th>Ad</th>
      <th>Soyad</th>
      <th>Departman</th>
      <th>Maaş</th>
      <th>İşlemler</th>
      

    </tr>
  </thead>

  <tbody>
    <tr v-for="row in rows" v-on:dblclick = "bilgigetir(row.id)">
      <td>{{row.id}}</td>
      <td>{{row.name}}</td>
      <td>{{row.surname}}</td>
      <td>{{row.department}}</td>
      <td>{{row.salary}}</td>
      <td><input type="button" value="Sil" v-on:click="rowdel(row.id)"/>
       <input type="button" value="Zam Yap" v-on:click="zamyap(row.id)"/></td>
    </tr>
  </tbody>
</table>


<table id="secondTable" required style ="float:right;visibility: hidden;" ><!-- class="hidden"-->
  <thead>
    <tr>
      <th>Olay Adı</th>
      <th>Açıklama</th>
    </tr>
  </thead>

  <tbody>
    <tr v-for="row in eventss">
     
   <td>{{row.olayAdi}}</td>
   <td>{{row.aciklama}}</td>
    </tr>
  </tbody>

</table>
</div>
</template>





<script>
export default {

  name: 'Ders7',

  data () {
    return {
    	ins : 7 ,
      gloid : 0,
      
			 rows: [
      { id: 1, name: "Ahmet ", surname: 'Ak', department : 'Memur',salary: '1422' },
      { id: 2, name: "Gamze ", surname: 'Yesil',department : 'Tekniker', salary: '5151' },
      { id: 3, name: "Sinem ", surname: 'Mor', department : 'Memur',salary: '3434'},
      { id: 4, name: "Ali ", surname: 'Kara', department : 'Uzman',salary: '3000' },
      { id: 5, name: "Polat ", surname: 'Alemdar',department : 'Mühendis',salary: '2233' },
      { id: 6, name: "Hasan ", surname: 'Kasan',department : 'Uzman', salary: '5354' }
    ],
    eventss: [
      
    ]
    }
  },
  methods: {

  		add: function(){
       var elem = document.getElementById('firstTable');
        if(document.getElementById("i2").value != "" && document.getElementById("i3").value != "" && document.getElementById("i4").value != "sc" && document.getElementById("i5").value != ""){
  		  
       
       
          this.rows.push({id:this.ins,name:document.getElementById("i2").value,surname:document.getElementById("i3").value,department:document.getElementById("i4").value,salary:document.getElementById("i5").value});
          this.eventss.push({olayAdi:"Personel Ekleme",aciklama:document.getElementById("i2").value+ " " + document.getElementById("i3").value +" " + "isimli kisi eklendi"});
        this.ins+=1;
        

   elem.scrollTop = elem.scrollHeight;
      }
       
        else if(document.getElementById("i4").value == "sc") {
            alert("Departman Kısmını boş bırakamazsınız.");
        }
        else{
           alert("Temel bilgileri boş bırakamazsınız.");
        }
				document.getElementById("i2").value = ""
        document.getElementById("i3").value = ""
        document.getElementById("i4").value ="sc"
        document.getElementById("i5").value =""
 

			},



      rowdel: function(id){
         
      var rw = document.getElementById("firstTable").rows.length;
      var myTable = document.getElementById('firstTable');
        for (var i = 0; i < rw; i++) {

          if(myTable.rows[i].cells[0].innerHTML==  id){
            var  dn = confirm(myTable.rows[i].cells[1].innerHTML +" " + myTable.rows[i].cells[2].innerHTML + " isimli personeli silmek  istediğinze emin misiniz ?");
            if(dn==true){
              this.eventss.push({olayAdi:"Personel Silme",aciklama:myTable.rows[i].cells[1].innerHTML +" " + myTable.rows[i].cells[2].innerHTML +" " + "isimli kisi silindi"});
              document.getElementById("firstTable").deleteRow(i);

              
            break;
            }
            else{
              break;
            }
          }
        }




      },
      zamyap: function(id){
       var rw = document.getElementById("firstTable").rows.length;
        var myTable = document.getElementById('firstTable');
        var zamOran = prompt(" % kaç zam yapmak istersiniz?");

       var zam = Number(zamOran);
              for (var i = 0; i < rw; i++) {
             if(myTable.rows[i].cells[0].innerHTML ==  id){
        var eski = Number(myTable.rows[i].cells[4].innerHTML);
        var yeni = Number(eski+((eski*zam)/100)) ;
      
         myTable.rows[i].cells[4].innerHTML =Number(yeni);
         if(zamOran != 0){ this.eventss.push({olayAdi:"Zam",aciklama:myTable.rows[i].cells[1].innerHTML +" " + myTable.rows[i].cells[2].innerHTML +" " + "isimli kişiye %"+zamOran+" Zam yapıldı"});
       }
        
         
}
       }



      },
			bilgigetir:function(id){
        
   
		  this.gloid = id ;
       
     
      
      var rw = document.getElementById("firstTable").rows.length;
      var myTable = document.getElementById('firstTable');
        for (var i = 0; i < rw; i++) {
          
          if(myTable.rows[i].cells[0].innerHTML == id ){
             
        
        document.getElementById("i2").value=myTable.rows[i].cells[1].innerHTML;
        document.getElementById("i3").value=myTable.rows[i].cells[2].innerHTML;
        document.getElementById("i4").value=  myTable.rows[i].cells[3].innerHTML   
        document.getElementById("i5").value=  myTable.rows[i].cells[4].innerHTML; 
        this.eventss.push({olayAdi:"Personel Detay Getirme",aciklama:myTable.rows[i].cells[1].innerHTML +" " + myTable.rows[i].cells[2].innerHTML +" " + "isimli kisinin bilgileri getirildi."});  

              
            break;
            }
            
          }
			},


      change: function(){
      
        
    if ( document.getElementById("i6").value=="Olay Günlüğünü Görüntüle") {
     document.getElementById("i6").value = "Olay Günlüğünü Gizle";
    }
    else {document.getElementById("i6").value = "Olay Günlüğünü Görüntüle";} 


        var x = document.getElementById('secondTable');
        var y = document.getElementById('i7');
    if (x.style.visibility === 'hidden') {
        x.style.visibility = 'visible';
        y.style.visibility = 'visible';

    } else {
        x.style.visibility = 'hidden';
        y.style.visibility = 'hidden';
    }

      },



			updt: function(){
        
      var id = this.gloid
     
      var rw = document.getElementById("firstTable").rows.length;
      var myTable = document.getElementById('firstTable');
      for (var i = 0;i < rw;i++) {
   
       if( myTable.rows[i].cells[0].innerHTML==  id){
         myTable.rows[i].cells[1].innerHTML = document.getElementById("i2").value; // rows[1] diyince ilk satıri degisitryor
         myTable.rows[i].cells[2].innerHTML = document.getElementById("i3").value;
         myTable.rows[i].cells[3].innerHTML = document.getElementById("i4").value;
          myTable.rows[i].cells[4].innerHTML = document.getElementById("i5").value;

          this.eventss.push({olayAdi:"Personel Detay Getirme",aciklama:myTable.rows[i].cells[1].innerHTML +" " + myTable.rows[i].cells[2].innerHTML +" " + "isimli kisinin bilgileri güncellendi."});  

       }


    }


    },




    ara: function(){
      if(document.getElementById('i2').value != ""){

         var searchText = document.getElementById('i2').value;
           console.log("İ2ye gore : " + searchText);
       } else if(document.getElementById('i4').value != null) {
      
          
           var searchText = document.getElementById('i4').value;
           console.log("İ4ye gore : " + searchText);
          
       }
       else{
        alert('İsim ve ya Departmanlardan birini seçmek zorundasınız.');
       }

     

    var targetTable = document.getElementById('firstTable');
    var targetTableColCount;
            
    
    for (var rowIndex = 0; rowIndex < targetTable.rows.length; rowIndex++) {
        var rowData = '';

        
        if (rowIndex == 0) {
           targetTableColCount = targetTable.rows.item(rowIndex).cells.length;
           continue; //.
        }
                
        
        for (var colIndex = 0; colIndex < targetTableColCount; colIndex++) {
            rowData += targetTable.rows.item(rowIndex).cells.item(colIndex).textContent;
        }

        // Eğer aranan terim bulunduysa göster yoksa satırı gizle 
        if (rowData.indexOf(searchText) == -1)
            targetTable.rows.item(rowIndex).style.display = 'none';
        else
            targetTable.rows.item(rowIndex).style.display = 'table-row';
    }
   

    },
    yenile: function(){
         var searchText = "";


    var targetTable = document.getElementById('firstTable');
    var targetTableColCount;
            
   
    for (var rowIndex = 0; rowIndex < targetTable.rows.length; rowIndex++) {
        var rowData = '';

        
        if (rowIndex == 0) {
           targetTableColCount = targetTable.rows.item(rowIndex).cells.length;
           continue; 
        }
                
        
        for (var colIndex = 0; colIndex < targetTableColCount; colIndex++) {
            rowData += targetTable.rows.item(rowIndex).cells.item(colIndex).textContent;
        }

        
        if (rowData.indexOf(searchText) == -1){
           
            
           }
        else{

            targetTable.rows.item(rowIndex).style.display = 'table-row';
    
     }
    }
  },
  	
  }
}
</script>





<style lang="css" scoped>
#canvas{
  
	width:600px;
	padding:200px 20px;
	text-align:center;
	border:1px solid #333;
}

table {
  float: left;
  font-family: 'Open Sans', sans-serif;
  width: 700px;
  border-collapse: collapse;
  border: 3px solid #44475C;
  margin: 10px 10px 0 10px;
  display: inline-table;
}


table th {

  text-transform: uppercase;
  text-align: left;
  background: #44475C;
  color: #FFF;
  padding: 8px;
  min-width: 30px;
}

table td {
   
  text-align: left;
  padding: 8px;
  border-right: 2px solid #7D82A8;
}

table tbody tr:nth-child(2n) td {
   
  background: #D4D8F9;
  /* 00FF00 */
}



</style>