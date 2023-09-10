<style>
    .main {
        flex:2;
        flex-direction: column;
        align-items: center;
        height: 100vh;
        width: 100%;
        background-color: black;
    }
    .list {
        flex:1;
        flex-direction: column;
        border: 4px ridge greenyellow;
        border-radius: 4px;
        padding: 2px;
        margin-top: 16px;
    }
    .list-item {
        border: 4px ridge white;
        padding: 4px;
        margin: 0px;
    }
    .large-button {
        min-width: fit-content;
        width: 50%;
    }
    .timer-buttons {
        margin-top: 10px;
        background-color: blueviolet;
        width: fit-content;
    }
    @keyframes flickerAnimation {
    0%   { opacity:1; }
    50%  { opacity:0; }
    100% { opacity:1; }
    }
    @-o-keyframes flickerAnimation{
    0%   { opacity:1; }
    50%  { opacity:0; }
    100% { opacity:1; }
    }
    @-moz-keyframes flickerAnimation{
    0%   { opacity:1; }
    50%  { opacity:0; }
    100% { opacity:1; }
    }
    @-webkit-keyframes flickerAnimation{
    0%   { opacity:1; }
    50%  { opacity:0; }
    100% { opacity:1; }
    }
    .animate-flicker {
    -webkit-animation: flickerAnimation 1s infinite;
    -moz-animation: flickerAnimation 1s infinite;
    -o-animation: flickerAnimation 1s infinite;
        animation: flickerAnimation 1s infinite;
    }
</style>
<script>
    let welcome_screen = true;
    let entries = [true, true]
    let timer_running = false;
    let timer_paused = false;
    setInterval(() =>{
        if (timer_running && !timer_paused && minutesLeft > 0) {
            decrementMinute()
        }
    }, 1000)

    let minutesLeft = 1
    function togglePausingTimer() {
        timer_paused = !timer_paused
    }
    function decrementMinute() {
        if (minutesLeft > 0) {
            minutesLeft -= 1
        } else {
            alert("Less than zero minutes not allowed >:O *makes bot noises*")
        }
    }
    function incrementMinute() {
        if (minutesLeft < 300) {
            minutesLeft +=1
        } else {
            alert("I think 5hrs is a pretty good upper limit ngl - don't press it more than that lol")
        }
    }
    function GoTakeABreak() {
        const entry = confirm("Did you take a water, eye, or stand up and stretch break? (\"Ok\" means yes")
        entries = [...entries, entry]
        timer_running = false;
        timer_paused = false;
        minutesLeft = 20
        const audio = new Audio('audio_file.mp3');
        audio.play()
    }
    function startTimer() {
        welcome_screen = false;
        timer_running = true;
        timer_paused = false;
    }

    $: (timer_running && minutesLeft == 0) && GoTakeABreak()
    $: timer_ended = timer_running == false && timer_running == false
</script>
<div class="main">
    {#if welcome_screen}
    <div>Hello!</div>
     <button on:click={startTimer}>Click Here</button>
    {:else if timer_running}
        <div class="animate-flicker">Timer status: {timer_paused?"Currently paused (:":"In progress :D ..."}</div>
        <button class="large-button" on:click={togglePausingTimer}>{timer_paused?"I>":"II"}</button>        
    {:else if timer_ended} 
        <div>Done!</div>
        <button on:click={startTimer}>Start A New Timer :DD</button>
    {/if}
    <div class="timer-buttons">
        <button on:click={decrementMinute} disabled={timer_running && !timer_paused}>-</button>
        {!timer_running?"(: Set Timer For ...":""}  {minutesLeft} Minute(s) {timer_running? "Left!":""}
        <button on:click={incrementMinute} disabled={timer_running && !timer_paused}>+</button>
    </div>
    <div class="list">
    {#each entries as entry}
    <!-- Use Green and add a star for good entries, Add a counter on successes,  -->
        <div class="list-item">{entry?"You did it": "You did not, but it's okay!"}</div>
    {/each}
    </div>
</div>