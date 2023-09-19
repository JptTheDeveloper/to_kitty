<style>
    div, h1, h2 {
        color: white;
    }
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
        border: 4px ridge purple;
        border-radius: 4px;
        padding: 2px;
        margin-top: 16px;
    }
    .list-item-success {
        border: 4px ridge green;
        padding: 4px;
        margin: 0px;
    }
    .list-item-failure {
        border: 4px ridge yellow;
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
    let default_minutes = 20;
    function decrementDefaultMinute(){
        if (default_minutes > 0) {
            default_minutes -= 1
            minutesLeft = default_minutes
        } else {
            alert("Less than zero minutes not allowed >:O *makes bot noises*")
        }    }
    function incrementDefaultMinute() {
        if (default_minutes < 300) {
            default_minutes +=1
            minutesLeft = default_minutes
        } else {
            alert("I think 5hrs is a pretty good upper limit ngl - don't press it more than that lol")
        }
    }
    /**
	 * @type {any[]}
	 */
    let entries = []
    let timer_running = false;
    let timer_paused = false;
    setInterval(() =>{
        // @ts-ignore
        if (timer_running && !timer_paused && minutesLeft > 0) {
            decrementMinute()
        }
    }, 60*1000)

    let minutesLeft = default_minutes;
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
        const audio1 = new Audio("break-time-msg.mp3");
        audio1.play();
        const entry = confirm("Did you drink water, close your eyes, or stand up/walk around ? (\"Ok\" means yes)")
        let message = success_msgs[getRandomInt(success_msgs.length)] ;
        if (!entry) {
            message = failure_msgs[getRandomInt(failure_msgs.length)];
        } 
        entries = [...entries, {"entry": entry, "message": message }];
        timer_running = false;
        timer_paused = false;
        minutesLeft = default_minutes;
        let msg = "-break-msg-"+getRandomInt(4)+".mp3";
        if (entry) {
            msg = "yes" + msg;
            const audio2 = new Audio(msg);
            audio2.play();
        } else {
            msg = "no" + msg;
            const audio2 = new Audio(msg);
            audio2.play();
        }
    }
    function startTimer() {
        timer_running = true;
        timer_paused = false;
    }

    $: (timer_running && minutesLeft == 0) && GoTakeABreak()
    $: timer_ended = timer_running == false && timer_running == false
    // Messages for success and failure
    /**
	 * @param {number} max
	 */
    function getRandomInt(max) {
     return Math.floor(Math.random() * max);
    }
    let success_msgs = ["You did it! :D", "Your body thanks you :hug", "I'm happy you did that c:", "Look at you! Kitty is k-taking care of herself!"]
    let failure_msgs = ["It's okay! You got it next time :)", "Thanks for trying! It counts just as much :hug", "It's okay :hug - you got it next time c:"]
</script>
<div class="main">
    <h1>Kitty's Counter</h1>
    <div style="padding:16px">{"Hello! This is an attempt to make life +1% better! May it help with it's creation or use (:"}</div>
    {#if timer_running}
        <div class="animate-flicker">Timer status: {timer_paused?"Currently paused (:":"In progress :D ..."}</div>
        <button class="large-button" on:click={togglePausingTimer}>{timer_paused?"I>":"II"}</button>        
    {:else if timer_ended} 
        <div>Done!</div>
        <button on:click={startTimer}>Start A New Timer :DD</button>
    {/if}
    <h2>Configuration:</h2>
    <div>The following changes the default minutes set for the timer.</div>
    <div>When the timer ends, this is the time that will be set as a default.</div>
    <div>This is only updatable when the timer isn't running.</div>
    <br/>
    <div class="timer-buttons">
        <button disabled={timer_running} on:click={decrementDefaultMinute}>-</button>
        {"(: Default Timer is: "+default_minutes+" Minute(s)"}
        <button disabled={timer_running} on:click={incrementDefaultMinute}>+</button>
    </div>
    <br/>
    <br/>
    <div>The following shows the minutes left in the current timer.</div>
    <div>It also lets you update the currently running timer.</div>
    <div>This is only updatable when the timer is paused.</div>
    <div class="timer-buttons">
        <button on:click={decrementMinute} disabled={!timer_running || !timer_paused}>-</button>
        {!timer_running?"Update Timer For ...":""}  {minutesLeft} Minute(s) {timer_running? "Left!":""}
        <button on:click={incrementMinute} disabled={!timer_running || !timer_paused}>+</button>
    </div>
    {#if entries.length > 0}
        <div class="list">
        {#each entries as entry}
        <!-- Use Green and add a star for good entries, Add a counter on successes,  -->
            {#if entry.entry}
                <div class="list-item-success">{entry.message}</div>
            {:else}
                <div class="list-item-failure">{entry.message}</div>
            {/if}
        {/each}
        </div>
    {/if}
</div>