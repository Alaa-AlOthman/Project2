<template lang="">
     <div class="mt-4">
        <div class="flex justify-center text-primary text-2xl">
          {{t}}
        </div>
        <div class=" flex mx-10">
          <table class="" v-for="(exam, index) in exams" :key="index">
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

              <td colspan="3">{{ exam[index].type == 'f' ? y.Avg : y.Year_Courses_Count }}</td>

              <td colspan="3"> {{ exam[index].type == 'f' ? 'المعدل' : 'المجموع' }} </td>
            </tfoot>
          </table>



        </div>
      </div>
</template>
<script>
export default {
  data() {
    return {
     
    }
  },
  props:['year','y','t'],
  computed: {
    exams() {
      const firstSemester = this.year.filter(el => el.type === 'f')
      const secondSemester = this.year.filter(el => el.type === 's')
      return [[...secondSemester], [...firstSemester]]
    },
  }
}
</script>
<style lang="">
    
</style>