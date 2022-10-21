<script>

let text = `Mugwort is a common name for several species of aromatic flowering plants in the genus Artemisia. In Europe, mugwort most often refers to the species Artemisia vulgaris, or common mugwort. In East Asia the species Artemisia argyi is often called "Chinese mugwort" in the context of traditional Chinese medicine, or àicǎo (艾草) in Mandarin. Artemisia princeps is a mugwort known in Korea as ssuk (쑥) and in Japan as yomogi (ヨモギ).[1] While other species are sometimes referred to by more specific common names, they may be called simply "mugwort" in many contexts.

The Anglo-Saxon Nine Herbs Charm mentions mucgwyrt. A folk etymology, based on coincidental sounds, derives mugwort from the word "mug"; more certainly, it has been used in flavoring drinks at least since the early Iron Age.[1] Other sources say mugwort is derived from the Old Norse muggi (meaning "marsh") and German wuertz (wort in English, originally meaning "root"), which refers to its use since ancient times to repel insects, especially moths.[2] The Old English word for mugwort is mucgwyrt where mucg-, could be a variation of the Old English word for "midge": mycg. Wort comes from the Old English wyrt (root/herb/plant), which is related to the Old High German wurz (root) and the Old Norse urt (plant).[3]
`;

let nice = '';
let state = 0;
let display = text.substring(0,24);
let i = 0;
let pos = 'normal'
$: nice = text.split(' ');

function renderText() {
    window.scrollTo(0, 0);
    document.body.style.cursor = `url('https://raw.githubusercontent.com/Silbad/pixa/main/icons/feather.svg'), auto`;
    if (i < 0) {
      i = 0;
    }
    if (i > nice.length) {
      i = 0;
    }
    if (nice[i] && nice[i+4]) {
      setTimeout(function(){
        display = nice[i] + ' ' + nice[i+1] + ' ' + nice[i+2] + ' ' + nice[i+3] + ' ' + nice[i+4];
        if (pos == 'back') {
          i=i-5;
          pos = 'normal'
        }
        else if (pos == 'next') {
          i=i+10;
          pos = 'normal'
        } else {
          i=i+5;
        }
        renderText();
      }, 1500);
    }

    // edge case - only partial input there
    if (nice[i] && !(nice[i+1])) {
      setTimeout(function(){
        display = nice[i]
        i=i+5;
      }, 1500);
    }
    else if (nice[i+1] && !(nice[i+2])) {
      setTimeout(function(){
        display = nice[i] + nice[i+1]
        i=i+5;
      }, 1500);
    }
    else if (nice[i+2] && !(nice[i+3])) {
      setTimeout(function(){
        display = nice[i] + nice[i+1] + nice[i+2]
        i=i+5;
      }, 1500);
    }
    // edge case - only partial input there end

}

let key;let keyCode;
function handleKeydown(event) {
	key = event.key;
	keyCode = event.keyCode;

  if (keyCode == 37) {
    pos = 'back';
  }

  if (keyCode == 39) {
    pos = 'next';
  }
}
</script>



<svelte:window on:keydown={handleKeydown}/>
<html data-theme="retro" lang="en">
<body>
  <div id="wrapper" class="p-10">
    <div style="padding: 300px;
                padding-bottom: 200px;
                font-size: 3em;">
    {display}
    </div>

    <div id="input" class="mt-10 pt-10">
      <textarea id="inputfield" bind:value={text}></textarea>
    </div>
    <br />

    <button id="play-btn" on:click={renderText}>▶️</button>
  </div>
</body>
</html>



<style>
body {
  max-width: 100%;
  height: 1450px;
  overflow-x: hidden;
  overflow-y: hidden;
  background-color: #100816;
  color: #FFFCFF;
  text-shadow: black 3px 2px;
  font-size: 1.3em;
}

#wrapper {
  text-align: center;
}

#inputfield {
  border-radius: 15px;
  opacity: 0.4;
  padding: 5px;
  background-color: turquoise;
  color: pink;
  font-size: 0.7em;
  width: 1100px;
  height: 282px;
}

#input {
  margin-top: 50px;
}
</style>
