<template lang="">

  <div class="mx-12 text-xl font-medium">
      
     <table>
         <thead>   
             <th class="text-lg">ملاحظات</th>
             <th class="text-lg">النتيجة</th>
             <th class="text-lg">كتابة</th>
             <th class="text-lg">العلامة</th>
             <th  class="text-lg">السنة</th>
             <th class="text-lg">اسم الأب</th> 
             <th class="text-lg">الاسم والنسبة</th>
             <th class="text-lg">الرقم الجامعي</th>
            
         </thead>
          <tbody  v-for="item in results" :key="item.id">
         
             <tr>
             
         <td> </td>
         <td> {{item.state}}</td>
         <td> </td>
         <td>{{item.Mark}}</td>
         <td> </td>
         <td> </td>
         <td> {{item.student_name}}</td>
         <td>{{item.university_num}} </td>
         
             </tr>
         </tbody>
     </table>
 </div>
</template>
<script>


import axios from "axios";
import { mapGetters } from "vuex";
export default {
 data() {
   return {
     results: [],
     data: {},
     
   }
 },
 methods: {
 async refresh(){
   try {
     const res = await axios.post('/ExamByCourse', {
       code: this.c_code,
       specialization: this.spec,
       study_year: '2013/2012',
       Examsemster: this.semster
     }, { headers: { 'Authorization': 'Bearer ' + this.$cookies.get('access_token'), 'Access-Control-Allow-Credentials': true } });

     console.log(res)
     this.data = res.data
     this.results = this.data.results
     console.log(this.data)
   }
   catch (e) {
     console.log(e);
   }
 }

 }, async mounted() {
   this.refresh()
 }, computed: {
   ...mapGetters(["spec"]),
   ...mapGetters('Exam', ['c_code', 'study_year', 'semster', 'selYear']),
 }

 ,watch:{
   selYear(){
     this.refresh()
   },
   c_code(){
     this.refresh()
   },
   semster(){
     this.refresh()
   }
 }
}
</script>
<style lang="">
   
</style>