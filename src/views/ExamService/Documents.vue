<template>
  <div class=" w-full text-4xl  font-light  text-white   h-12 bg-primary flex p-2 justify-between items-center"
    style="text-align:center">
    <div>
      <img src="../../assets/Images/arrow-left-circle.png" class="m-4 h-12  left-2 cursor-pointer " @click="back"
        alt="الخلف">
    </div>
    <div>
      وثائق &nbsp;&nbsp;</div>
  </div>
  <div class="flex justify-between items-center mt-4 mx-6 ">
    <div class="flerx justify-center items-center space-x-4 text-primary text-lg">
      <button class="bg-primary text-body text-lg rounded-lg text-center  px-5 hover:bg-hovercolor"
        @click="">طباعة</button>

    </div>
    <div class="flerx justify-center items-center space-x-4 text-primary text-lg">
      <button class="bg-primary text-body text-lg rounded-lg text-center  px-5 hover:bg-hovercolor"
        @click="SearchStudent()">عرض</button>

    </div>
    <div class="flerx justify-center items-center space-x-4 text-primary text-lg">

      <select class="rounded-lg text-primary text-lg h-8 " v-model="docType">
        <option value="k">
          كشف علامات
        </option>
        <option value="b">
          بيان وضع
        </option>
      </select>
      <label>
        : الوثيقة
      </label>
    </div>

    <div class="flerx justify-center items-center space-x-4 text-primary text-lg">
      <input type="text" class="search rounded-lg w-34" v-model="university_num">
      <label>
        : الرقم الجامعي
      </label>
    </div>
  </div>
  <div>
    <div class=" border-primary border-2 mx-4 mt-6 mb-6" v-if="docType == 'k'">
      <div class="flex  items-center justify-between mb-24 mt-6 mx-6  text-primary text-lg">
        <div class="h-42 w-42">
          <img src="../../assets/Images/al-baath-logo.png" class="h-36 w-36 pt-2 " alt="" />
        </div>
        <div class="m-1 ">
          <label class="flex justify-center items-center mx-auto">الجمهورية العربية السورية</label><br>
          <label class="flex justify-center items-center mx-auto">جامعة البعث
          </label><br>
          <label class="flex justify-center items-center mx-auto">كلية الآداب والعلوم الإنسانية</label>
        </div>
      </div>
      <div class="flex justify-center text-primary text-4xl mb-24">
        كشف العلامات
      </div>
      <div class=" mx-auto mt-2">
        <table class="t1 text-primary">
          <tr class="t1 text-primary">
            <td class="t1 bg-body text-primary ">
              {{ student1.mothername }}
            </td>
            <td class="t1 bg-body  text-primary">
              : اسم الأم
            </td>
            <td class="t1 bg-body text-primary">
              {{ student1.fathername }}
            </td>
            <td class="t1 bg-body text-primary">
              : اسم الأب
            </td>
            <td class="t1 bg-body text-primary">
              {{ student1.fullname }}
            </td>

            <td class="t1 bg-body text-primary">
              : اسم الطالب وكنيته
            </td>
          </tr>
          <tr class="t1 text-primary">
            <td class="t1 bg-body text-primary ">
              {{ student1.birthdate }} {{ student1.birthplace }}
            </td>
            <td class="t1 bg-body text-primary ">
              : محل وتاريخ الولادة
            </td>
            <td class="t1 bg-body text-primary">
              {{ student1.nationality }}
            </td>
            <td class="t1 bg-body text-primary">
              : الجنسية

            </td>
            <td class="t1 bg-body text-primary">
              {{ student1.created_at }}
            </td>

            <td class="t1 bg-body text-primary">
              : تاريخ التسحيل
            </td>
          </tr>

        </table>
      </div>
      <div class="flex justify-end text-primary text-lg mt-14 mx-2">
        <label>
          2022 فيما يلي كشف بدرجات الطالب/ة خلال سنين دراسته الجامعية في كلية الآداب والعلوم الإنسانية برنامج التعليم
          المفتوح قسم الترجمة حتى العام الدراسي
        </label>
      </div>
       <!-- <MarksTable t="السنة الأولى" :y1="y1" :year1="year1"></MarksTable>
       <MarksTable t="السنة الثانية" :y2="y2" :year2="year2"></MarksTable>
       <MarksTable t="السنة الثالثة" :y3="y3" :year3="year3"></MarksTable> 
       <MarksTable t="السنة الرابعة" :y4="y4" :year4="year4"></MarksTable>  -->
       <div class="mt-4">
        <div class="flex justify-center text-primary text-2xl">
          السنة الأولى
        </div>
        <div class=" flex mx-10">
          <table class="" v-for="(exam, index) in exams1" :key="index">
            <tr>
              <th colspan="3">الدرجة</th>
              <!-- <th colspan="3" rowspan="2">مقررات الفصل الثاني</th> -->
              <th colspan="3" rowspan="2"> {{ exam[index].type == 'f' ? 'مقررات الفصل الاول' : 'مقررات الفصل الثاني' }}</th>
            </tr>
            <tr>
              <th colspan="2">كتابة</th>
              <th>رقماً</th>
            </tr>
            <tbody v-for="paper in exam" :key="paper.id">
              <tr>
                <td colspan="2">{{ paper.typing }}</td>
                <td>{{ paper.Mark }}</td>
                <td colspan="3">{{ paper.course_name }}</td>
              </tr>
            </tbody>
            <tfoot>

              <td colspan="3">{{ exam[index].type == 'f' ? y1.Avg : y1.Year_Courses_Count }}</td>

              <td colspan="3"> {{ exam[index].type == 'f' ? 'المعدل' : 'المجموع' }} </td>
            </tfoot>
          </table>



        </div>
      </div>
      <div class="mt-4">
        <div class="flex justify-center text-primary text-2xl">
          السنة الثانية
        </div>
        <div class=" flex mx-10">
          <table class="" v-for="(exam, index) in exams2" :key="index">
            <tr>
              <th colspan="3">الدرجة</th>
              <!-- <th colspan="3" rowspan="2">مقررات الفصل الثاني</th> -->
              <th colspan="3" rowspan="2"> {{ exam[index].type == 'f' ? 'مقررات الفصل الاول' : 'مقررات الفصل الثاني' }}</th>
            </tr>
            <tr>
              <th colspan="2">كتابة</th>
              <th>رقماً</th>
            </tr>
            <tbody v-for="paper in exam" :key="paper.id">
              <tr>
                <td colspan="2">{{ paper.typing }}</td>
                <td>{{ paper.Mark }}</td>
                <td colspan="3">{{ paper.course_name }}</td>
              </tr>
            </tbody>
            <tfoot>

              <td colspan="3">{{ exam[index].type == 'f' ? y2.Avg : y2.Year_Courses_Count }}</td>

              <td colspan="3"> {{ exam[index].type == 'f' ? 'المعدل' : 'المجموع' }} </td>
            </tfoot>
          </table>



        </div>
      </div>
      <div class="mt-4">
        <div class="flex justify-center text-primary text-2xl">
          السنة الثالثة
        </div>
        <div class=" flex mx-10">
          <table class="" v-for="(exam, index) in exams3" :key="index">
            <tr>
              <th colspan="3">الدرجة</th>
              <!-- <th colspan="3" rowspan="2">مقررات الفصل الثاني</th> -->
              <th colspan="3" rowspan="2"> {{ exam[index].type == 'f' ? 'مقررات الفصل الاول' : 'مقررات الفصل الثاني' }}</th>
            </tr>
            <tr>
              <th colspan="2">كتابة</th>
              <th>رقماً</th>
            </tr>
            <tbody v-for="paper in exam" :key="paper.id">
              <tr>
                <td colspan="2">{{ paper.typing }}</td>
                <td>{{ paper.Mark }}</td>
                <td colspan="3">{{ paper.course_name }}</td>
              </tr>
            </tbody>
            <tfoot>

              <td colspan="3">{{ exam[index].type == 'f' ? y3.Avg : y3.Year_Courses_Count }}</td>

              <td colspan="3"> {{ exam[index].type == 'f' ? 'المعدل' : 'المجموع' }} </td>
            </tfoot>
          </table>



        </div>
      </div>
      <div class="mt-4">
        <div class="flex justify-center text-primary text-2xl">
          السنة الرابعة
        </div>
        <div class=" flex mx-10">
          <table class="" v-for="(exam, index) in exams4" :key="index">
            <tr>
              <th colspan="3">الدرجة</th>
              <!-- <th colspan="3" rowspan="2">مقررات الفصل الثاني</th> -->
              <th colspan="3" rowspan="2"> {{ exam[index].type == 'f' ? 'مقررات الفصل الاول' : 'مقررات الفصل الثاني' }}</th>
            </tr>
            <tr>
              <th colspan="2">كتابة</th>
              <th>رقماً</th>
            </tr>
            <tbody v-for="paper in exam" :key="paper.id">
              <tr>
                <td colspan="2">{{ paper.typing }}</td>
                <td>{{ paper.Mark }}</td>
                <td colspan="3">{{ paper.course_name }}</td>
              </tr>
            </tbody>
            <tfoot>

              <td colspan="3">{{ exam[index].type == 'f' ? y4.Avg : y4.Year_Courses_Count }}</td>

              <td colspan="3"> {{ exam[index].type == 'f' ? 'المعدل' : 'المجموع' }} </td>
            </tfoot>
          </table>



        </div>
      </div>
      <div>
        <label class="flex justify-end text-primary text-lg m-6">
          : ملاحظات
        </label>
        <div class="flex justify-end">
          <textarea class="flex justify-end text-primary text-lg m-6 rounded-lg w-96 h-24 p-2" dir="rtl"></textarea>
        </div>
      </div>
      <label
        class="flex justify-center text-primary m-2 ">_______________________________________________________________________________</label>
      <div class="flex justify-between items-center text-primary text-2xl mb-24 mx-16 ">
        <label>
          عميد كلية الآداب والعلوم الإنسانية
        </label>
        <label>
          رئيس الدائرة
        </label>
        <label>
          رئيس شعبة الامتحانات
        </label>
        <label>
          المدقق
        </label>
        <label>
          المنظم
        </label>
      </div>
      <div class="flex justify-between items-center text-primary text-2xl mb-24 mx-16 ">
        <label>مدير شؤون الطلاب</label>
        <label>
          نائب رئيس الجامعة لشؤون التعليم المفتوح
        </label>
      </div>

    </div>
    <div class=" border-primary border-2 mx-4 mt-6 mb-6" v-if="docType == 'b'">
      <div class="flex  items-center justify-between mb-24 mt-6 mx-6  text-primary text-lg">
        <div class="h-42 w-42">
          <img src="../../assets/Images/al-baath-logo.png" class="h-36 w-36 pt-2 " alt="" />
        </div>
        <div class="m-1 ">
          <label class="flex justify-center items-center mx-auto">الجمهورية العربية السورية</label><br>
          <label class="flex justify-center items-center mx-auto">جامعة البعث
          </label><br>
          <label class="flex justify-center items-center mx-auto">كلية الآداب والعلوم الإنسانية</label>
        </div>
      </div>
      <div class="flex justify-center text-primary text-4xl mb-24">
        بيان وضع
      </div>
      <div class=" mx-auto mt-2">
        <table class="t1 text-primary">
          <tr class="t1 text-primary">
            <td class="t1 bg-body text-primary ">
              {{ student1.mothername }}
            </td>
            <td class="t1 bg-body  text-primary">
              : اسم الأم
            </td>
            <td class="t1 bg-body text-primary">
              {{ student1.fathername }}
            </td>
            <td class="t1 bg-body text-primary">
              : اسم الأب
            </td>
            <td class="t1 bg-body text-primary">
              {{ student1.fullname }}
            </td>

            <td class="t1 bg-body text-primary">
              : اسم الطالب وكنيته
            </td>
          </tr>
          <tr class="t1 text-primary">
            <td class="t1 bg-body text-primary ">
              {{ student1.birthdate }} {{ student1.birthplace }}
            </td>
            <td class="t1 bg-body text-primary ">
              : محل وتاريخ الولادة
            </td>
            <td class="t1 bg-body text-primary">
              {{ student1.nationality }}
            </td>
            <td class="t1 bg-body text-primary">
              : الجنسية

            </td>
            <td class="t1 bg-body text-primary">
              {{ student1.created_at }}
            </td>

            <td class="t1 bg-body text-primary">
              : تاريخ التسحيل
            </td>
          </tr>

        </table>
      </div>
      <label class="flex justify-end text-primary text-2xl mt-24 m-6">
        هو من طلاب كلية الآداب والعلوم الإنسانية برنامج التعليم المفتوح قسم الترجمة رقمه
        الجامعي{{ student1.university_num }} وبناءً عليه أعطي هذه الوثيقة
      </label>
      <div class="flex justify-center text-primary ">____________________________________________________________________
      </div>
      <div class="flex justify-between items-center text-primary text-2xl mt-24 mb-24 mx-16 ">
        <label>
          عميد كلية الآداب والعلوم الإنسانية
        </label>

        <label>
          رئيس شعبة الامتحانات
        </label>
      </div>

    </div>


  </div>
</template>

<script>
import axios from "axios";
import { mapGetters } from 'vuex'
import { ref } from '@vue/reactivity'
import MarksTable from "../../components/ExamService/documents/MarksTable.vue";
export default {
  components:{MarksTable},
  setup() {
    const y1 = ref({})
    const y2 = ref({})
    const y3 = ref({})
    const y4 = ref({})
    const year1 = ref({})
    const year2 = ref({})
    const year3 = ref({})
    const year4 = ref({})
    const seco2 = ref({})
    const sec1 = ref({})
    const data = ref([])
    const section = ref('')
    const docType = ref('')
    const select = (s, d) => { section.value = s; Show.value = d }
    const allcourses = ref([{}]);
    const name = ref('')
    const id = ref('')
    const Show = ref(false)
    const stopreg = ref(false)
    const search = ref('')
    const status = ref('')
    const failed = ref([])
    const ShYear = ref(false)
    const sure = ref(false)
    const sr = () => { sure.value = true }
    const tran = ref(false)
    const trans = () => { tran.value = !tran.value }
    const student1 = ref({
      fullname: '',
      fathername: '',
      mothername: '',
      birthplace: '',
      birthdate: '',
      gender: '',
      place_num_registration: '',
      nationality: '',
      address: '',
      phone: '',
      recruitment_division: '',
      national_num: '',
      homephone: '',
      university_num: '',
      certifeca: '',
      specialization: '',
      created_at: ''
    })
    const suspsen = ref([])

    return { sec1, y1, y2, y3, y4, seco2, failed, data, select, section, docType, Show, id, name, status, search, ShYear, allcourses, sr, sure, stopreg, tran, trans, student1, suspsen, year1, year2, year3, year4 }
  },


  methods: {
    back() {
      this.$router.go(-1)
    }, async SearchStudent() {
      this.show = true
      try {
        this.$store.commit('Student/SetID', this.id)
        console.log(this.university_num)
        const res = await axios.post("/searchForStudent", {
          university_num: this.university_num,
          specialization: this.spec
        }, { headers: { 'Authorization': 'Bearer ' + this.$cookies.get('access_token'), 'Access-Control-Allow-Credentials': true } })
        console.log(res)
        this.student1 = res.data.data

      }
      catch (e) {
        console.log(e);
      }

      if (this.docType == 'k') {
        try {
          const res = await axios.post('/getMarksStudent', {
            specialization: this.spec,
            university_num: this.university_num
          }, { headers: { 'Authorization': 'Bearer ' + this.$cookies.get('access_token'), 'Access-Control-Allow-Credentials': true } });

          console.log(res)
          this.data = res.data
          for (var y of this.data) {
            if (y.year == 'first') {
              this.y1 = y.detal
              this.year1 = this.merge(this.y1)
            } if (y.year == 'second') {
              this.y2 = y.detal
              this.year2 = this.merge(this.y2)
            }
            if (y.year == 'third') {
              this.y3 = y.detal
              this.year3 = this.merge(this.y3)
            }
            if (y.year == 'forth') {
              this.y4 = y.detal
              this.year4 = this.merge(this.y4)
            }
          }
          console.log(this.year3)
          console.log(this.year1)

        }
        catch (e) {
          console.log(e);
        }
      }




    }, async getby() {
      try {
        const res = await axios.post('/getMarksStudent', { university_num: this.university_num, specialization: this.spec }, { headers: { 'Authorization': 'Bearer ' + this.$cookies.get('access_token'), 'Access-Control-Allow-Credentials': true } });
        console.log(res);
        this.allC = [];
        const new55 = res.data.cours;
        var u = 0;
        for (var v of new55) {
          this.allC[u] = v;
          u += 1;
        }
        console.log(this.allC);
      }
      catch (e) {
        console.log(e);
      }
    }, suspSelect(s) {
      this.select(s)
      this.loadsusp()
    }, merge(year) {
      var y = [];
      var type = '';
      var first = []
      for (var f of year.first_semster) {
        type = 'f'
        f.type = type
        first.push(f)
      }
      var second = []
      for (var f of year.second_semster) {
        type = 's'
        f.type = type
        second.push(f)
      }
      for (var f of first) {
        y.push(f)
      }
      for (var f of second) {
        y.push(f)
      }
      //  console.log(y)
      return y;
    }



  }, computed: {
    ...mapGetters(["spec", "dept"]),
    exams1() {
      const firstSemester = this.year1.filter(el => el.type === 'f')
      const secondSemester = this.year1.filter(el => el.type === 's')
      return [[...secondSemester], [...firstSemester]]
    }, exams2() {
      const firstSemester = this.year2.filter(el => el.type === 'f')
      const secondSemester = this.year2.filter(el => el.type === 's')
      return [[...secondSemester], [...firstSemester]]
    }, exams3() {
      const firstSemester = this.year3.filter(el => el.type === 'f')
      const secondSemester = this.year3.filter(el => el.type === 's')
      return [[...secondSemester], [...firstSemester]]
    },
    exams4() {
      const firstSemester = this.year4.filter(el => el.type === 'f')
      const secondSemester = this.year4.filter(el => el.type === 's')
      return [[...secondSemester], [...firstSemester]]
    },
  }
}
</script>

<style>
.t1 {
  border-style: none;
  margin: 0PX;
  padding: 0PX;

}
</style>
