<script>

let text = `The Anglo-Saxon Nine Herbs Charm mentions mucgwyrt. A folk etymology, based on coincidental sounds, derives mugwort from the word "mug"; more certainly, it has been used in flavoring drinks at least since the early Iron Age.[1] Other sources say mugwort is derived from the Old Norse muggi (meaning "marsh") and German wuertz (wort in English, originally meaning "root"), which refers to its use since ancient times to repel insects, especially moths.[2] The Old English word for mugwort is mucgwyrt where mucg-, could be a variation of the Old English word for "midge": mycg. Wort comes from the Old English wyrt (root/herb/plant), which is related to the Old High German wurz (root) and the Old Norse urt (plant).[3]
`;

let nice = '';
let state = 0;
let display = '';
let i = 0;
let pos = 'normal'
$: nice = text.split(' ');

function renderText() {
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
    <div>
    {display}
    </div>

    <div id="input" class="mt-10 pt-10">
      <textarea id="inputfield" bind:value={text}></textarea>
    </div>
    <br />

    <button on:click={renderText}>▶️</button>
  </div>
</body>
</html>



<style>
body {
  max-width: 100%;
  height: 850px;
  overflow-x: hidden;
  overflow-y: hidden;
  background-color: #8527FF;
  color: #FFFCFF;
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
  width: 300px;
  height: 40px;
}

#input {
  margin-top: 50px;
}
</style>
