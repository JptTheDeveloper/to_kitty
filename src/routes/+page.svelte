<script>
    import Typewriter, { loopOnce } from 'svelte-typewriter';
    const lines = [
        {
            text: "We probably can't give you all the peace you need :( ..."
        },
        {
            text: "...but we can make each day a little better :hug"
        },
        {
            text: "Please be kind to yourself."
        },
        {
            text: "Accept yourself."
        },
        {
            text: "Feel the love from your cats and fishies."
        },
        {
            text: "I wish I knew",
        },
        {
            text: "the magical set of words to correct what you're feeling inside :hug"
        },
    ]
</script>

{#each lines as line, i (line.text)}
    <Typewriter
        interval={40}
        cursor={false}
        mode=loopOnce
        delay={i * 4500}>
        <h3>{line.text}</h3>
    </Typewriter>
{/each}
