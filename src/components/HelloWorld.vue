<template>
  <div class="hello">
    <button @click="showPrint">인쇄하기</button>

    <div ref="printArea">
      <div class="print-view" v-if="isPrintPOP">
        <p>test</p>
        <p class="test">인쇄 영역을 테스트합니다. 다국어 폰트 대응을 테스트합니다.</p>
        <p>印刷領域をテストします。多言語フォント対応をテストします。</p>
        <p>测试打印区域 。 测试多语种字体对应。</p>
        <p>Test the print area. Test multilingual font response.</p>

        <button @click="closePrint">닫기</button>
      </div>
    </div>

    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',

  props: {
    msg: String
  },

  data: function() {
    return {
      isPrintPOP: false
    }
  },

  mounted() {
    
  },

  methods: {
    // goPrint: function() {
    //   this.showPrint();
    //   this.startPrint();
    // },

    showPrint: function() {
      this.isPrintPOP = true;

      this.$nextTick(function() {
        this.startPrint();
      });
    },

    startPrint: function() {
      let app = document.getElementById('app')
      const printContents = this.$refs.printArea.innerHTML
      let printDiv = document.createElement('DIV')

      // console.log(printDiv);

      printDiv.innerHTML = printContents
      document.body.appendChild(printDiv)
      app.style.display = 'none'
      window.print();

      app.style.display = 'block'
      printDiv.style.display = 'none'
      printDiv.innerHTML = ''
    },

    closePrint: function() {
      this.isPrintPOP = false;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* @page { size: landscape; } */
.print-view { position: absolute; width: 500px; height: 500px; background: aqua !important; -webkit-print-color-adjust: exact; left: 50%; margin-left: -250px; }
.print-view p { border: 5px solid red; }
.print-view .test { background: rgb(136, 136, 138); }
</style>
