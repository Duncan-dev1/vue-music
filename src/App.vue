<template>
  <div id="app">
   <header>
     <h1>My Music</h1>
   </header>
   <main>
     
     <section class="player">
       <h2 class="song-title">{{current.title}}-<span>{{current.artist}}</span></h2>
    <div class="controls" >
      <button class="prev" @click="prev"> Prev</button>
      <button class="play" v-if="!isplaying" @click="play">Play</button>
      <button class="pause" v-else @click="pause"> Pause</button>
      <button class="next" @click="next">Next</button>
      <button class="my_playlist" @click="my_playlist">Create Playlist</button>
    </div>
     </section>
  <section class="playlist">
    <h3>The Playlist</h3>
    <button v-for="song in songs " :key="song.src" @click="play(song)"
    :class="(song.src ==current.src) ? 'song playing' :'song'">
    {{song.title}}- {{song.artist}}
    </button>
  </section>
    
   </main>
  </div>

</template>

<script>


export default {
 name:'app',
 data(){
   return{
     current:{},
     index:1,
     
     ispaying:false,
     songs:[
       {
         title:'Kuliko Jana',
         artist:'Sauti Sol',
         src:require('./assets/music/Sauti Sol - Kuliko Jana ft (RedFourth Chorus) SMS [Skiza 1069356] to 811.mp3')
       },
        {
         title:'Maombi',
         artist:'Nadia Mukami',
         src:require('./assets/music/Nadia Mukami - Maombi (official video)   DIAL  811 177# TO SET AS SKIZA.mp3')
       },
        {
         title:'Still The One',
         artist:'Sauti Sol',
         src:require('./assets/music/Sauti Sol - Still The One (Official Music Video) SMS [Skiza 1063120] to 811.mp3')
       },
        {
         title:'All i need',
         artist:'Steve Kekana',
         src:require('./assets/music/Steve Kekana - All I need (Is Right Here in Africa).mp3')
       },
        {
         title:'Wanted',
         artist:'One republic',
         src:require('./assets/music/OneRepublic - Wanted.mp4')
       }   
     ],
     player:new Audio()
   }
 },
 methods:{
play(song){
  if(typeof song.src != "undefined" ){
    this.current=song;
      this.player.src=this.current.src;
  }
  this.player.play();
  this.player.addEventListener('ended',function(){
this.index++;
 this.index++;
  if (this.index >this.songs.length-1){
    this.index=0;
  }
  this.current=this.songs[this.index];
  this.play(this.current)
  }.bind(this));
  this.isplaying=true;
},
pause(){
  this.player.pause();
  this.isplaying=false;
},
next(){
  this.index++;
  if (this.index >this.songs.length-1){
    this.index=0;
  }
  this.current=this.songs[this.index];
  this.play(this.current)
},
prev(){
   this.index--;
  if (this.index <0){
    this.index=this.songs.length-1;
  }
  this.current=this.songs[this.index];
  this.play(this.current)
},
/*add(){
this.songs.push({title:'Radio Love', artist:'Nadia Mukami', src:require('./assets/music/Nadia Mukami - Radio Love (Official Video) Ft. Arrow Bwoy SMS SKIZA 8545509 to 811.mp3') })
}  */
 },
 
 created (){
   this.current=this.songs[this.index];
   this.player.src=this.current.src;
   
  // this.player.play();
 }
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
body {
	font-family: sans-serif;
}
header {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 15px;
	background-color: #212121;
	color: #FFF;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.song-title {
  color: #53565A;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.song-title span {
  font-weight: 400;
  font-style: italic;
}
.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
}
.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #FFF;
  background-color: #CC2E5D;
}
.next, .prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #FFF;
  background-color: #FF5858;
}
.playlist {
  padding: 0px 30px;
}
.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist .song:hover {
  color: #FF5858;
}
.playlist .song.playing {
  color: #FFF;
  background-image: linear-gradient(to right, #CC2E5D, #FF5858);
}
</style>