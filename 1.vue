<!-- <template>
    <div class="balance">
        <HelloWorld msg="Hello Ivan"/>

    </div>
</template>

<script>
    import HelloWorld from "./components/HelloWorld.vue";

    export default {
        name: "App",
        components: {
            HelloWorld,            
        }
}
</script>


<style scoped>

</style> -->

<template>
    <div id="app">
       <h1>Authors</h1>
       <input class="amount" type="number" min="1" max="9" name="num" id="num"
           v-model="amountPut" /><br>
       <button @click="getAuthors()">Submit</button>
       <button type="reset" @click="getReset()">Reset</button>  
       <ul id="authors"></ul>
       <img id="image" src="https://randomuser.me/api/portraits/med/women/6.jpg"/>
       <p id="authorName"></p>
       <p id="authorImg"></p>

      <h1>Random Joke Generator</h1> 
      <p id="jokeDisplay"></p>
      <button @click="newJoke()">New Joke</button>
      <button type="reset" @click="resetJoke()">Reset</button> 
   </div> 




</template>

<script>

  export default {
   data(){
       return{
           amountPut:'',
           jokes: ['Guess the number of programmers it takes to change a light bulb? Zero its a hardware problem',
                   'There are only 10 kinds of people in this world: those who know binary and those who don’t.',
                   'Real programmers count from 0.', 
                   'Why did the programmer quit his job? Because he didnt get arrays.', 
                   'A foo walks into a bar takes a look around and says Hello World',
                   '0 is false 1 is true right? 1',
                   'Things arent always #000000 and #FFFFFF.',
                   'What is the most used language in programming? Profanity',
                   '!False its funny because its True',
                   'You had me at Hello World',
                   '2b||!2b',
                   'Yesterday I changed the name on my wifi to Hack if you can. Today I found it named Challenge Accepted',
                   'A programmer is a person who fixed a problem that you didnt know you had in a way you dont understand',
                   'How can you tell if a computer geek is an extrovert? They stare at your shoes when you talk instead of their own.',
                   'I would love to change the world but they wont give me the source code.',
                   'If at first you dont succedd call it version 1.0',
                   'Computers make very fast very accurate mistakes',
                   'I farted in the Apple store and everyone got mad at me. Not my fault they dont have Windows.',
                   'Knock Knock... Whos there? Art... Art Who? R2D2',
                   'Hilarious and amazingly true thing: if a pizza has a radius (z) and a depth (a) that pizzas volume can be defined Pi*z*z*a.'
                   ],

       }
   },
 
   methods:{
       
       getReset(){
           document.getElementById("authorName").innerHTML = "";
           document.getElementById('num').value='';
           },
       getAuthors() {
/*             fetch(
               `https://randomuser.me/api/?results=${this.amountPut}`
           )
           .then((res) => res.json())
           .then((data) => {
               this.data = data;
               let authors = data.results;
               let ul= document.getElementById('authors').innerHTML
                return authors.map(function(author) {
               let img= document.getElementById('image1')
               img.src = author.picture.medium;
               let li= document.getElementById('authorInfo').innerHTML
               let span= document.getElementById('authorName').innerHTML
               span = `${author.name.first} ${author.name.last}`;
               this.append(li, img);
               this.append(li, span);
               this.append(ul, li);
               }) 
           }) */
           console.log("The user/s is/are displayed.")
                   fetch(
                       `https://randomuser.me/api/?results=${this.amountPut}`
                       )
                       .then((res) => res.json())
                       .then((results) => {
                           /*                             document.getElementById('authorName').innerHTML= data.name
*/ 
                           this.results = results;
                           console.log(results.results)
                           const html= results.results.map(results =>{
                               return `
                               <p>${results.name.first} ${results.name.last} </p>
                               `
                           })
                           document.getElementById('authorName').insertAdjacentHTML("afterbegin", html)

                           const html1= results.results.map(results =>{
                                let image= document.getElementById("image")
                                image.src= results.results.picture.medium
                               return `
                               <p>${image.src}</p>
                               `
                           })
                           document.getElementById('authorImg').insertAdjacentHTML("afterbegin", html1)

                           console.log(html)

                           return `image`
                       }) 
       },
           newJoke(){
                   var randomNumber=Math.floor(Math.random()*(20))
                   if(randomNumber % 2 == 0) {
                   console.log("The number is even.")
                   document.getElementById('jokeDisplay').innerHTML=this.jokes[randomNumber]
                   }

                   // if the number is odd
                   else {
                   console.log("The number is odd.")
                   fetch(
                       `https://official-joke-api.wl.r.appspot.com/random_joke`
                       )
                       .then((res) => res.json())
                       .then((data) => {
                           this.data = data;
                           document.getElementById('jokeDisplay').innerHTML= data.setup +" "+ data.punchline
                       })
                   }

               },
               resetJoke(){
                   document.getElementById('jokeDisplay').innerHTML=''
               },
   },
   mounted(){
       this.getAuthors();
   }, 
}    

</script>

<style scoped>

body {
 background: #f5f5f5;
}
h1{
   text-align: center;
   font-family: arial;
   color: #5a5a5a;
}
ul{
   display: flex;
   list-style:none;
   flex-wrap: wrap;
   align-items: flex-start;
   justify-content:center;
   flex-basis: 80%;
}

li{
   flex-basis: 20%;
     display:flex;
     flex-direction: column;
     margin-bottom: 20px;
     align-items:center;
}

span{
   font-family: arial;
       font-size: 14px;
       color: #5a5a5a;
       text-align: center;
}

img{
   margin: 5px;
       border-radius: 3px;
       box-shadow: 1px 1px 3px rgba(0,0,0,0.2); 
}

p{
   font-size: 150%;
}
</style>
