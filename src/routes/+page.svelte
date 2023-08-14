<script>
    import Typewriter, { loopOnce } from 'svelte-typewriter';
    const lines = [
        {
            text: "Happy Birthday Bluumarine!",
        },
        {
            text: "You are really cool.",
        },
        {
            text: "From one overthinker, to another ...",
        },
        {
            text: "I want you to know ...",
        },
        {
            text: "You are really, really, so COOOL :D !\n\n",
        },
        {
            text: "I really, really, hope this year is super great for you.",
        },
        {
            text: "------------------------------",
        },
        {
            text: "(Couldn't figure out how to line break in a cool way)"
        },
        {
            text: "-----------------------------",
        },
        {
            text: "Anyways (lol) look at you! You are now 22! Congrats again :D.",
        },
        {
            text: "I can't imagine what great things will come your way.",
        },
        {
            text: "Here's to your happiest year so far :DD",
        },
        {
            text: "My favorite goat admirer, sleepy soldier, and speed reading whisperer :p <3 - Pablo"
        }

    ]
</script>

{#each lines as line, i (line.text)}
    <Typewriter
        interval={50}
        cursor={false}
        mode=loopOnce
        delay={i * 3500}>
        <h3>{line.text}</h3>
    </Typewriter>
{/each}
