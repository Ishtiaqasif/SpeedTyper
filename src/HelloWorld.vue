<template>
   <div>
       <h1>Speed Typer</h1>
       <h3>Your Score:{{keywords.filter(x=>x.correct == true).length}}/{{keywords.length}}</h3>
       <p>
           <span
           :class="{correct: keyword.correct, wrong: keyword.wrong, pending: keyword.pending}" 
           :key="keyword.text" v-for="keyword in keywords">{{keyword.text}}{{' '}}</span>
       </p>
       <input type="text" :value="inputValue" @keyup.space="processInput($event)"/>
   </div>
</template>
<script>

let defaultKeywords = ['hello', 'bello', 'tello', 'xello','aello', 'bello', 'cello', 'dello']
        .map(keyword=>{
            return{
                text: keyword,
                correct: false,
                worng: false,
                pending: true
            }
        });

export default {
    data(){
        return {
            inputValue:"",
            index: 0,
            keywords: defaultKeywords  
        }
    },
    methods: {
        processInput(event){
            let value = event.target.value.trim(); 
            
            if (value == '') {
                return;
            }
 
            if (this.keywords[this.index].text === value) {
                //correct answer
                this.keywords[this.index].correct = true;
                this.keywords[this.index].worng = false;
                this.keywords[this.index].pending = false;
                
            }
            else{
                //wrong answer
                this.keywords[this.index].correct = false;
                this.keywords[this.index].worng = true;
                this.keywords[this.index].pending = false;
            }

            this.inputValue = '';
            this.index++;
        }
    }
    
    
}
</script>
<style lang="css" scoped>
h1{
    color: rgb(161, 24, 179);
}
p{
  color: red;
  font-size: large;
  font-style: italic;
  font-weight: bolder;  
}
.pending{
    color: orange
}
.correct{
    color: green
}
.wrong{
    color: red
}
</style>