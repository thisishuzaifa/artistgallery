<template>
<div>
  <div class="artist">
    <h1>Artist Directory</h1>
    <div>
      <input class="filterInput"  type="text" v-on:input="filter()" v-model="filter"><br />
      <button class="addButton" v-on:click="showInputBoxes">Add artist</button>
    </div>
  </div>

  <div class="artistInputs" v-if="addButtonClicked">
      <input placeholder="Artist Name" type="text" v-model="artistName"><br />
      <input placeholder="About artist" type="text" v-model="aboutArtist"><br />
      <input placeholder="Image url" type="text" v-model="url"><br />
      <div class="artistButton">
      <button class="addButton2" v-on:click="addArtist(artistName, aboutArtist, url)">Add</button>
      </div>
  </div>

  <div v-if="artistsArray.length > 0 && !filter">
    <div class="artistCard" v-for="artist in artistsArray" :key="artist.id">
      <img :src="artist.url" alt="">
      <span>
      <p>{{artist.name}}</p>
      <p>{{artist.about}}</p>
      </span>
      <button class="deleteButton" v-on:click="deleteBtn(artist.id)">Delete</button>
    </div>
  </div>
</div>

</template>

<script>

export default{
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      addButtonClicked: false,
      artistsArray: [],
      idNum: 0,
      filter: "",
      filtered: []
    }
  },
  methods: {
    showInputBoxes: function(){
      this.addButtonClicked = !this.addButtonClicked;
    },
    addArtist: function(artistName, aboutArtist, url){
      this.artistsArray.push({
        name: artistName,
        about: aboutArtist,
        url: url,
        id: this.idNum
      });
      this.idNum++;
      this.addButtonClicked = !this.addButtonClicked;
    },
    deleteBtn: function(id){
      this.artistsArray = this.artistsArray.filter(function(artist){
        return artist.id !== id;
      });
    },
    filter: function(){
      this.filtered = this.artistsArray.filter(function(artist){
        return artist.name.toLowerCase().includes(this.filter.toLowerCase());
      }.bind(this));
    }
  }

}

</script>

<style scoped>

.addButton, .artistButton, .deleteButton, .addButton2{
  background-color: #2c3e50;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 10px;
  margin: 10px;
  width: 100px;
  height: 30px;
}

.artist{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.artistCard{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  margin: 10px;
  padding: 10px;
  border: 1px solid black;
  border-radius: 5px;
}

.artistInputs{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}





</style>