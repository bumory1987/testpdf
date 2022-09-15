<template>
  <div id="pdfvuer">
    <div id="buttons" class="ui grey three item inverted bottom fixed menu transition hidden">
      <a class="item" @click="page > 1 ? page-- : 1">
        <i class="left chevron icon"></i>
        Back
      </a>
      <a class="ui active item">
        {{page}} / {{ numPages ? numPages : '∞' }}
      </a>
      <a class="item" @click="page < numPages ? page++ : 1">
        Forward
        <i class="right chevron icon"></i>
      </a>
    </div>

  <pdfvuer :src="pdfdata"   :page="page" style="width:100%;margin:20px auto;">
  <template v-slot:loading>
    loading content here...
  </template>
  </pdfvuer>
  </div>
</template>

<script>
import pdfvuer from 'pdfvuer'
import {ref , onMounted} from 'vue'

export default {
  name: 'HelloWorld',
  components: {
    pdfvuer
  },
  props: ['linkInfo'],
  setup(props){
    console.log(props.linkInfo)
    const pageman = ref(1)
    const numPages = ref(0)
    const pdfdata = ref(pdfvuer.createLoadingTask(
          {url :props.linkInfo,
           }))

    const page = ref(1)

    onMounted(()=>{
      pdfdata.value.then(pdf=>{
        numPages.value = pdf.numPages
        console.log(numPages.value)
      })
    })
 
    return {pageman, pdfdata, numPages, page }
  }
}
</script>

<style src="pdfvuer/dist/pdfvuer.css"></style>
<style lang="css" scoped>
  #buttons {
    margin-left: 0 !important;
    margin-right: 0 !important;
  }
  /* Page content */
  .content {
    padding: 16px;
  }
</style>
