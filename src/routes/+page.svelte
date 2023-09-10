<script>
    import Typewriter, { loopOnce } from 'svelte-typewriter';
    const msgs = [
        "I am sending you all the strength I can <3. Things will be okay",
        "Dexter is happy to have you as his owner, he feels supported by you <3",
        "It's stressful. It's a lot. Know that you are doing your best :hug",
        "You are incredible. Dexter is blessed to have you as his owner",
        "Your heart agonizes. It's awful. Things will get better :hug ",
        "You are brilliant and diligent. You are the best caretaker Dexter could ask for",
        "You have a internet family ready to help you. They will do so much for you. We're ready to support.",
        "You have a weird programmer guy who deeply cares about you. Things will be okay :hug",
        "6 months of discord friendship means I would download fortnight and play it non-stop for you (:",
        "Mina or your gaming pals would too! :DD",
        "It will be okay :hug",
        "Dexter - 'Meow Meow Meow' =>(Translated)=> 'Thank you mom/owner/parent for taking care of me :D'",
        "Dexter - 'Meow Meow Meow' =>(Translated)=> 'We'll play more when I'm better!'",
        "Dexter - 'Meow Meow Meow' =>(Translated)=> 'You are doing your best. I'm happy you're here'",
        "Dexter - 'Meow Meow Meow' =>(Translated)=> 'Your jokes are funny! I can't laugh cause I'm a cat. If I could though, you'd hear me all the time :D'"
    ]
    const formatted_msgs = msgs.map((msg) => ({"text": msg}))
    const seconds = new Date().getTime() / 1000;
    const item_num = Math.floor((seconds % 60) % formatted_msgs.length)
    const lines = [formatted_msgs[item_num]]
    // const lines = [
    //     {
    //         text: "We probably can't give you all the peace you need :( ..."
    //     },
    //     {
    //         text: "...but we can make each day a little better :hug"
    //     },
    //     {
    //         text: "Please be kind to yourself."
    //     },
    //     {
    //         text: "Accept yourself."
    //     },
    //     {
    //         text: "Feel the love from your cats and fishies."
    //     },
    //     {
    //         text: "I wish I knew",
    //     },
    //     {
    //         text: "the magical set of words to correct what you're feeling inside :hug"
    //     },
    // ]
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
