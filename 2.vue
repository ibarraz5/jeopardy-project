

<template>
    <div>
       <h1 class="title"> Random User Generator</h1>
<div class="user-profile">
   <img id="avatar" src="https://randomuser.me/api/portraits/med/women/6.jpg" />
   <div id="fullname">andrea sørensen</div>
 <div id="username">goldendog885
 </div>
   <div class="description">
     <div>Email: <span id="email">andrea.sørensen@example.com</span></div>
     <div>City: <span id="city">nr åby</span></div>
 </div>
 <div class="footer">
   <button id="btn">Next User!</button>
</div>
</div>
   </div> 




</template>

<script>
   export default{
       data(){
           avatar: document.getElementById('avatar')
       },
       methods:{
           const url =' https://randomuser.me/api/ ';

           let avatar = document.getElementById('avatar');
           let fullname = document.getElementById('fullname');
           let username = document.getElementById('username');
           let email = document.getElementById('email');
           let city = document.getElementById('city');
           let btn = document.getElementById('btn');
           handleErrors (res){
               if(!res.ok){
                   throw (res.status);
               }
               console.log(res);
               return res;
               }
       }
   }

const url =' https://randomuser.me/api/ ';

let avatar = document.getElementById('avatar');
let fullname = document.getElementById('fullname');
let username = document.getElementById('username');
let email = document.getElementById('email');
let city = document.getElementById('city');
let btn = document.getElementById('btn');

btn.addEventListener("click", function() {
 fetch(url)
   .then(handleErrors)
   .then(parseJSON)
   .then(updateProfile)
   .catch(printError)
});

function handleErrors (res){
 if(!res.ok){
   throw (res.status);
 }
 console.log(res);
 return res;
}

function parseJSON (res){
 return res.json();
}

function updateProfile (profile){
 avatar.src = profile.results[0].picture.medium;
 fullname.innerHTML = profile.results[0].name.first +" "+profile.results[0].name.last; 
 username.innerHTML = profile.results[0].login.username; 
 email.innerHTML = profile.results[0].email;
 city.innerHTML = profile.results[0].location.city;
 return 1;
}

function printError (error){
 console.log(error);
}  

</script>

<style scoped>

@import url(https://fonts.googleapis.com/css?family=Raleway|Varela+Round|Coda);

body {
 background: #ecf0f1;
 padding: 2.23em;
}

.title {
 color: #2c3e50;
 font-family: "Coda", sans-serif;
 text-align: center;
}
.user-profile {
 margin: auto;
   width: 27em; 
 height: 11em;
 background: #fff;
 border-radius: .3em;
}

.user-profile  #fullname {
 margin: auto;
 margin-top: -4.40em;
 margin-left: 5.80em;
 color: #16a085;
 font-size: 1.53em;
 font-family: "Coda", sans-serif;
 font-weight: bold;
}

#username {
 margin: auto;
 display: inline-block;
 margin-left: 10.43em;
 color: #3498db;
 font-size: .87em;
 font-family: "varela round", sans-serif;
}

.user-profile > .description {
 margin: auto;
 margin-top: 1.35em;
 margin-right: 3em;
 width: 18em;
 color: #7f8c8d;
 font-size: .87em;
 font-family: "varela round", sans-serif;
}

.user-profile > img#avatar {
   padding: .7em;
 margin-left: .3em;
 margin-top: .3em;
 height: 6.23em;
 width: 6.23em;
 border-radius: 18em;
}


.footer {
   margin: 2em auto;
   height: 3.70em;
 background: #16a085;
 text-align: center;
 border-radius: 0 0 .3em .3em;
 display: flex;
 justify-content: center;
 align-items: center;
 transition: background 0.1s;
}

button {
 color: white;
 font-family: "Coda", sans-serif;
 text-align: center;
 font-size: 20px;
 background: none;
 outline: none;
 border: 0;
}

.footer:hover {
 background: #1abc9c;
}
</style>