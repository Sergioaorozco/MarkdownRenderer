<script>
import { marked } from "marked";

export default {
  data() {
    return {
      isMDX : false,
      fileInit : null,
      fileOutput : null,
    }
  },
  methods: {
    filledInput(e) {
      this.isMDX = e.target.value !== '';
      this.fileInit = e.target.value
    },
    convertMarkDown() {
      let conditionText = this.fileInit && this.isMDX;
      if (conditionText) {
        // Convert Markdown text to HTML using markdown-it
        const htmlText =  marked.parse(this.fileInit);

        // Update the fileOutput property with the HTML text
        this.fileOutput = htmlText;
      }
    },
  }
}

</script>

<template>
  <main class="wrapper text-center py-10 flex justify-center flex-col gap-y-10 w-full">
    <h1 class="text-slate-500 text-4xl font-bold">Markdown to <span class="text-slate-100 italic">Formatted Text</span>
    </h1>
    <div class="flex gap-x-4 justify-center mt-5 h-96">
      <textarea  @input="filledInput($event)" name="textInit" id="textInit" cols="30" rows="10" placeholder="Markdown text"
        class="border border-slate-400 rounded-lg p-2 w-full"></textarea>
      <iframe id="outputText" class="border border-slate-400 rounded-lg bg-slate-200 p-2 w-full" readonly :srcdoc="fileOutput"></iframe>
    </div>
    <button @click="convertMarkDown" class="bg-orange-600 hover:bg-orange-700 transition-colors duration-200 text-white py-3 rounded-lg" :class="{'bg-slate-600/30 pointer-events-none' : !isMDX}">{{!isMDX ?
    'No hay information' : 'Convertir Textos'}}</button>
  </main>
</template>
s
<style is:global>
  .wrapper {
    max-inline-size: 1125px;
    margin: 0 auto;
  }

</style>