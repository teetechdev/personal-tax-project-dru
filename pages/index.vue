<template>
  <div>
    <b-container fluid style="margin-bottom: 20px;">
      <div>
        <h3 align="center" class="mt-5 text-primary">
          คำนวณภาษีเงินได้บุคคลธรรมดา
        </h3>
      </div>
      <b-row>
        <b-col
          sm="12"
          md="10"
          lg="8"
          xl="6"
          offset-md="1"
          offset-lg="2"
          offset-xl="3"
        >
      <div class="mt-3">
        เมนู:
        <div class="btn-group" role="group" aria-label="Basic example">
          <button type="button" :class="[page === 1 ? 'active btn btn-primary' : 'btn btn-secondary']" @click="page = 1" >เงินได้</button>
          <!-- <button type="button" :class="[page === 2 ? 'active btn btn-primary' : 'btn btn-secondary']" @click="page = 2" :disabled="checkPage">ลดหย่อน</button> -->
          <button type="button" :class="[page === 2 ? 'active btn btn-primary' : 'btn btn-secondary']" @click="page = 2" :disabled="checkPage">ภาษี</button>
        </div>
        <!-- <hr/> -->
      </div>
          <b-table-simple caption-top responsive v-if="page === 1">
            <caption>
              เงินได้:
            </caption>
            <colgroup>
              <col style="width: 330px" />
              <col />
              <col />
            </colgroup>
            <b-tbody>
              <b-tr>
                <b-td>เงินเดือน :</b-td>
                <b-td
                  ><b-form-input v-model="form1.a" type="number"></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
              <b-tr>
                <b-td>รายได้อื่น ๆ :</b-td>
                <b-td
                  ><b-form-input v-model="form1.b" type="number"></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
              <b-tr>
                <b-td>รวมเงินได้ที่นำไปคำนวณภาษี :</b-td>
                <b-td
                  ><b-form-input
                    :value="form1dis1"
                    type="number"
                    disabled
                  ></b-form-input
                ></b-td>
                <b-td> </b-td>
              </b-tr>
              <b-tr>
                <b-td>ยกเว้น เงินสะสมกองทุนสำรองเลี้ยงชีพ :</b-td>
                <b-td
                  ><b-form-input v-model="form1.d" type="number" :disabled="checkPage" @keyup="checkd"></b-form-input
                ></b-td>
                <b-td>หักได้ 15% แต่ไม่เกิน 500,000 บาท</b-td>
              </b-tr>
              <b-tr>
                <b-td>หักเงินสำรองเลี้ยงชีพ ที่เกิน 10,000 บาท :</b-td>
                <b-td
                  ><b-form-input
                    v-model="form1.e"
                    type="number"
                    disabled
                  ></b-form-input
                ></b-td>
                <b-td>ส่วนที่ไม่เกิน 10,000 บาท</b-td>
              </b-tr>
              <b-tr>
                <b-td>ยกเว้น เงินสะสมกบข. + กองทุนสงเคราะห์ครูเอกชน :</b-td>
                <b-td
                  ><b-form-input v-model="form1.f" type="number" @keyup="checkf" :disabled="checkform1f"></b-form-input
                ></b-td>
                <b-td>หักได้ไม่เกิน 500,000 บาท</b-td>
              </b-tr>
              <b-tr>
                <b-td>ยกเว้น กรณีอายุตั้งแต่ 65 ปี หรือบุคคลพิการ :</b-td>
                <b-td
                  ><b-form-input v-model="form1.g" type="number" @keyup="checkg"></b-form-input
                ></b-td>
                <b-td>หักได้ไม่เกิน 190,000 บาท</b-td>
              </b-tr>
              <b-tr>
                <b-td>รวมเงินได้ที่ได้รับการยกเว้น :</b-td>
                <b-td
                  ><b-form-input
                    :value="checkh"
                    type="number"
                    disabled
                  ></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
              <b-tr>
                <b-td>คงเหลือ เงินได้ก่อนหักค่าใช้จ่าย :</b-td>
                <b-td
                  ><b-form-input
                    :value="checki"
                    type="number"
                    disabled
                  ></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
              <b-tr>
                <b-td>หักค่าใช้จ่าย 50% แต่ไม่เกิน 100,000 บาท :</b-td>
                <b-td
                  ><b-form-input
                    :value="checkj"
                    type="number"
                    disabled
                  ></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
              <b-tr>
                <b-td>คงเหลือ :</b-td>
                <b-td
                  ><b-form-input
                    :value="checkk"
                    type="number"
                    disabled
                  ></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
            </b-tbody>
          </b-table-simple>
          <!-- <b-table-simple caption-top responsive v-else-if="page === 2">
            <caption>
              ลดหย่อน:
            </caption>
            <colgroup>
              <col style="width: 330px" />
              <col />
              <col />
            </colgroup>
            <b-tbody>
              <b-tr>
                <b-td>ค่าลดหย่อนส่วนตัว :</b-td>
                <b-td
                  ><b-form-input
                    v-model="form2.a"
                    type="number"
                    disabled
                  ></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
              <b-tr>
                <b-td>ค่าลดหย่อนส่วนตัว :</b-td>
                <b-td
                  ><b-form-input
                    v-model="form2.a"
                    type="number"
                    disabled
                  ></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
            </b-tbody>
          </b-table-simple> -->
          <b-table-simple caption-top responsive v-else-if="page === 2">
            <caption>
              คำนวณภาษี:
            </caption>
            <colgroup>
              <col style="width: 330px" />
              <col />
              <col />
            </colgroup>
            <b-tbody>
              <b-tr>
                <b-td>1. เงินเดือน ค่าจ้าง โบนัส บำนาญ อื่นๆ  :</b-td>
                <b-td
                  ><b-form-input :value="form2dis1" disabled type="number"></b-form-input
                ></b-td>
                <b-td>ต่อปี</b-td>
              </b-tr>
              <b-tr>
                <b-td>2. หักเงินที่ได้รับยกเว้น :</b-td>
                <b-td
                  ><b-form-input :value="checkh" disabled type="number"></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
              <b-tr>
                <b-td>3. คงเหลือ (1.-2.) :</b-td>
                <b-td
                  ><b-form-input :value="checki" disabled type="number"></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
              <b-tr>
                <b-td>4. หักค่าใช้จ่าย (ร้อยละ 50 ของ 3. แต่ไม่เกิน 100,000 บาท) :</b-td>
                <b-td
                  ><b-form-input :value="checkj" disabled type="number"></b-form-input
                ></b-td>
                <b-td></b-td>
              </b-tr>
              <b-tr>
                <b-td>5. คงเหลือ (3.-4.) :</b-td>
                <b-td
                  ><b-form-input :value="checkk" disabled type="number"></b-form-input
                ></b-td>
                <b-td> </b-td>
              </b-tr>
              <b-tr>
                <b-td>6. หักค่าลดหย่อน :</b-td>
                <b-td
                  ><b-form-input v-model="this.form2.f" disabled type="number"></b-form-input
                ></b-td>
                <b-td> </b-td>
              </b-tr>
              <b-tr>
                <b-td>7. เงินได้สุทธิ (5.-6.) :</b-td>
                <b-td
                  ><b-form-input :value="check2g" disabled type="number"></b-form-input
                ></b-td>
                <b-td> </b-td>
              </b-tr>
              <b-tr>
                <b-td>8. ภาษีคำนวณจากเงินได้สุทธิ </b-td>
                <b-td
                  ><b-form-input :value="check2h" disabled type="number"></b-form-input
                ></b-td>
                <b-td> </b-td>
              </b-tr>
            </b-tbody>
          </b-table-simple>
        </b-col>
      </b-row>
    </b-container>
    <div class="footer">
      <div class="d-flex justify-content-around align-content-center">
        <div style="font-size: 18px;">เงินได้สุทธิ <b-badge variant="primary">{{checkk}}</b-badge></div>
        <div style="font-size: 18px;">ค่าลดหย่อน <b-badge variant="success">{{form2.f}}</b-badge></div>
        <div style="font-size: 18px;">ภาษีที่ต้องชำระ <b-badge variant="danger">{{check2h}}</b-badge></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      page: 1,
      form1: {
        a: null,
        b: null,
        c: null,
        d: null,
        e: null,
        f: null,
        g: null,
        h: null,
        i: null,
        j: null,
        k: null,
      },
      form2:{
        a: 60000,
        b: null,
        c: null,
        d: null,
        e: null,
        f: 60000,
        g: null,
        h: null,
        i: null,
        j: null
      }
    }
  },
  computed:{
    checkPage(){
      if(!this.form1.a || !this.form1.b){
        return true
      }else{
        return false
      }
    },
    checkform1f(){
      if(!this.form1.d){
        return true
      }else{
        return false
      }
    },
    form1dis1(){
      this.form1.c = (parseInt(this.form1.a) || 0) + (parseInt(this.form1.b) || 0)
      return (parseInt(this.form1.a) || 0) + (parseInt(this.form1.b) || 0)
    },
    form2dis1(){
      this.form1.c = (parseInt(this.form1.a) * 12 || 0) + (parseInt(this.form1.b) || 0)
      return (parseInt(this.form1.a) * 12 || 0) + (parseInt(this.form1.b) || 0)
    },
    checkh(){
      this.form1.h = ((parseInt(this.form1.e) || 0)+(parseInt(this.form1.f) || 0)+(parseInt(this.form1.g) || 0))
      return ((parseInt(this.form1.e) || 0)+(parseInt(this.form1.f) || 0)+(parseInt(this.form1.g) || 0))
    },
    checki(){
      this.form1.i = ((parseInt(this.form1.c) || 0)-(parseInt(this.form1.h) || 0))
      return ((parseInt(this.form1.c) || 0)-(parseInt(this.form1.h) || 0))
    },
    checkj(){
      let presum = (parseInt(this.form1.a) || 0) + (parseInt(this.form1.b) || 0)
      let sum = ((presum * 50) / 100)
      if(sum > 100000){
        this.form1.j = 100000
        return 100000
      }else{
        this.form1.j = sum
        return sum
      }
    },
    checkk(){
      this.form1.k = (parseInt(this.form1.i) || 0) -  (parseInt(this.form1.j) || 0)
      return  (parseInt(this.form1.i) || 0) -  (parseInt(this.form1.j) || 0)
    },
    check2g(){
      this.form2.g =  this.form1.k - parseInt(this.form2.f)
      if(this.form2.g <= 0){
        return 0
      }else{
        return  this.form1.k - parseInt(this.form2.f)
      }
    },
    check2h(){
      let totalTax
      let precal = parseInt(this.form2.g)
      // // free
      if (precal>= 150000) {
        precal = precal- 150000
        totalTax = 0
      }else{
        return totalTax = 0
      }
      // 5
      // precal = precal - 150000
      if (this.form2.g >= 150000) {
        let pre = precal - 150000
        let after = precal - pre
        let tax5 = (after * 5) / 100
        totalTax = totalTax + tax5
        precal = precal - 150000
      } else {
        let tax5 = (precal * 5) / 100
        totalTax = totalTax + tax5
        return totalTax
      }
      // 10
      if (precal >= 200000) {
        let pre = precal - 200000
        let after = precal - pre
        let tax10 = (after * 10) / 100
        totalTax = totalTax + tax10
        precal = precal - 200000
      } else {
        let tax10 = (precal * 10) / 100
        totalTax = totalTax + tax10
        return totalTax
      }
      // 15
      if (precal >= 250000) {
        let pre = precal - 250000
        let after = precal - pre
        let tax15 = (after * 15) / 100
        totalTax = totalTax + tax15
        precal = precal - 250000
      } else {
        let tax15 = (precal * 15) / 100
        totalTax = totalTax + tax15
        return totalTax
      }
      // 20
      if (precal >= 250000) {
        let pre = precal - 250000
        let after = precal - pre
        let tax20 = (after * 20) / 100
        totalTax = totalTax + tax20
        precal = precal - 250000
      } else {
        let tax20 = (precal * 20) / 100
        totalTax = totalTax + tax20
        return totalTax
      }
      // 25
      if (precal >= 1000000) {
        let pre = precal - 1000000
        let after = precal - pre
        let tax25 = (after * 25) / 100
        totalTax = totalTax + tax25
        precal = precal - 1000000
      } else {
        let tax25 = (precal * 25) / 100
        totalTax = totalTax + tax25
        return totalTax
      }
      // 30
      if (precal >= 3000000) {
        let pre = precal - 3000000
        let after = precal - pre
        let tax30 = (after * 30) / 100
        totalTax = totalTax + tax30
        precal = precal - 250000
      } else {
        let tax30 = (precal * 30) / 100
        totalTax = totalTax + tax30
        return totalTax
      }
      //35
      if (precal >= 0) {
        let tax35 = (precal * 35) / 100
        totalTax = totalTax + tax35
        return totalTax
      }

    }
  },
  methods: {
    nextPage() {
      this.page += 1
    },
    previousPage() {
      this.page -= 1
    },
    checkd(){
      let sum =  (parseInt(this.form1.a) || 0) + (parseInt(this.form1.b) || 0)
      if(this.form1.d > sum){
        alert(`หักได้ 15% แต่ไม่เกิน 500,000 บาท
(ไม่เกิน ${(sum * 15 / 100)})`)
        this.form1.d = (sum * 15 / 100)
        if(parseInt(this.form1.d) > 10000){
          this.form1.e = parseInt(this.form1.d) - 10000
        }else{
          this.form1.e = null
        }
      }else{
        if(parseInt(this.form1.d) > 10000){
          this.form1.e = parseInt(this.form1.d) - 10000
        }else{
          this.form1.e = null
        }
      }
    },
    checkf(){
      let sum = parseInt(this.form1.f) + parseInt(this.form1.d)
      if(sum > 500000 ){
        this.form1.f = 500000 - parseInt(this.form1.d)
        alert(`หักได้ไม่เกิน 500,000 บาท
(ไม่เกิน ${500000 - parseInt(this.form1.d)})`)
      }
    },
    checkg(){
      if(parseInt(this.form1.g)>190000){
        alert('หักได้ไม่เกิน 190,000')
        this.form1.g = 190000
      }
    }
  },
}
</script>

<style scoped>
/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type='number'] {
  -moz-appearance: textfield;
}

.footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  background-color: #f5f5f5;
}
</style>
