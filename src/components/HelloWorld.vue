<template>
  <div>
  <button @click="--pageman">prev page</button><button @click="++pageman">next page</button>

  <pdfvuer src="./static/task.pdf"  :key="pageman" :id="pageman" :page="pageman" style="width:100%;margin:20px auto;">
  <template v-slot:loading>
    loading content here...
  </template>
  </pdfvuer>
  </div>
</template>

<script>
import pdfvuer from 'pdfvuer'
import {ref ,  onMounted} from 'vue'

export default {
  name: 'HelloWorld',
  components: {
    pdfvuer
  },

  setup(){
    const pageman = ref(1)
    const totalPage = ref(0)
    const pdfdata = ref('')
    const other = ref(null)
    // const other = ref('https://pdftron.s3.amazonaws.com/downloads/pl/demo-annotated.pdf')
    const getPdf  = async () => {
        pdfdata.value= 'https://pdftron.s3.amazonaws.com/downloads/pl/demo-annotated.pdf'
        other.value = await pdfvuer.createLoadingTask('https://pdftron.s3.amazonaws.com/downloads/pl/demo-annotated.pdf')
        totalPage.value = other.value.numPages
        console.log(totalPage.value)



        // pdfdata.value.then(pdf =>{
        //   numPages.value = pdf.numPages;        })
        // pdfdata.value = await pdfvuer.createLoadingTask('https://pdftron.s3.amazonaws.com/downloads/pl/demo-annotated.pdf')
        // console.log( pdfdata.value)
        // pdfdata.value.then(pdf => {
        //   self.numPages = pdf.numPages;
          // window.onscroll = function() { 
          //   changePage() 
          //   stickyNav()  
          // }
  
        //   // Get the offset position of the navbar
        //   var sticky = $('#buttons')[0].offsetTop
  
        //   // Add the sticky class to the self.$refs.nav when you reach its scroll position. Remove "sticky" when you leave the scroll position
        //   function stickyNav() {
        //     if (window.pageYOffset >= sticky) {
        //       $('#buttons')[0].classList.remove("hidden")
        //     } else {
        //       $('#buttons')[0].classList.add("hidden")
        //     }
        //   }
  
        //   function changePage () {
        //     var i = 1, count = Number(pdf.numPages);
        //     do {
        //       if(window.pageYOffset >= self.findPos(document.getElementById(i)) && 
        //           window.pageYOffset <= self.findPos(document.getElementById(i+1))) {
        //         self.page = i
        //       }
        //       i++
        //     } while ( i < count)
        //     if (window.pageYOffset >= self.findPos(document.getElementById(i))) {
        //       self.page = i
        //     }
        //   }
        // });
    
    } 

    onMounted(()=>{
       getPdf()
    })

    return {pageman, pdfdata, other }
  }
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
