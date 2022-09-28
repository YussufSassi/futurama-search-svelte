  <script>
    export let char;
    const say = (message) => {
    let speech = new SpeechSynthesisUtterance();
    speech.text = message;
    window.speechSynthesis.speak(speech);
  }
  </script>

<div class="flex flex-col gap-2">
    <button class="text-2xl cursor-pointer" on:click="{() => {say(char.Name)} }">{char.Name}</button>
<p>Species 👽: {char.Species}</p>
<p>Age 🕰: {char.Age}</p>
<p>Planet 🌍: {char.Planet}</p>
<p>Profession(s) 💼: {char.Profession}</p>
<p>Status: {char.Status == "Alive" ? "👶" : char.Status == "Deceased" ? "💀" : char.Status}</p>
<p>Relatives 👨‍👩‍👦‍👦: {char.Relatives}</p>
<p>Voiced by 🎙: {char.VoicedBy}</p>
<p>First appearance 📺: {char.FirstAppearance}</p>
</div>