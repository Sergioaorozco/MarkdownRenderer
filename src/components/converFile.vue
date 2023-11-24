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
    renderOutput(){
      return this.fileOutput ? `<div class="outInfo">${this.fileOutput}</div>` : `<p>First Copy Something</p>`
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
        class="border bg-slate-200 border-slate-400 rounded-lg p-2 w-full"></textarea>
      <!-- <iframe id="outputText" class="border border-slate-400 rounded-lg bg-slate-200 p-2 w-full" readonly :srcdoc="fileOutput"></iframe> -->
      <div class="border border-slate-400 rounded-lg bg-white p-2 w-full outputText overflow-y-auto" readonly v-html="renderOutput()"></div>
    </div>
    <button @click="convertMarkDown" class="bg-orange-600 hover:bg-orange-700 text-slate-900 transition-colors duration-200 font-bold py-3 rounded-lg" :class="{'bg-slate-600/30 text-slate-400 pointer-events-none' : !isMDX}">{{!isMDX ?
    'Disabled, first add some Markdown' : 'Parse Texts'}}</button>
  </main>
</template>
s
<style is:global lang="scss">
  .wrapper {
    max-inline-size: 1125px;
    margin: 0 auto;
  }

  .outputText {
    text-align: left;
    font-family: 'Inter';
    color: #636363;
    .outInfo {
      pre{
        display: block;
        padding: 9.5px;
        margin: 0 0 10px;
        font-size: 13px;
        line-height: 1.42857143;
        color: #333;
        word-break: break-all;
        word-wrap: break-word;
        background-color: #f5f5f5;
        border: 1px solid #ccc;
        border-radius: 4px;
      }
      .warning {
        background-color: #ff8;
        padding: 20px;
        border-radius: 6px;
      }
      table {
        border-spacing: 0;
        border-collapse: collapse;
        background-color: transparent;
        & > thead > tr > th, & > tbody > tr > th, & > tfoot > tr > th, & > thead > tr > td, & > tbody > tr > td, & > tfoot > tr > td { 
          padding: 8px;
          line-height: 1.42857143;
          vertical-align: top;
          border-top: 1px solid #ddd;
        }
        & > tbody > tr:nth-child(odd) > td, .table-striped > tbody > tr:nth-child(odd) > th { background-color: #f9f9f9; }
      }
      *:not(pre,table){ all: revert;}
    }
  }

</style>