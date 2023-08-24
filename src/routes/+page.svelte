<script>
    import Typewriter, { loopOnce } from 'svelte-typewriter';
    const lines = [
        {
            text: "We probably can't give you all the peace you need :( ..."
        },
        {
            text: "...but we can make each day a little better :hug"
        },
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
