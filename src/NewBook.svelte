<script>
    export let title = '';
    export let author = '';
    export let newBookHandler = {};

    const onSubmit = (e) => {
        e.preventDefault();

        newBookHandler({title: e.target.title.value, author: e.target.author.value});

        e.target.title.value = '';
        e.target.author.value = '';
    };

</script>

<section>
    <h4>Lägg till ny bok</h4>
    <form on:submit={onSubmit}>
        <input type='text' id='title' placeholder='Titel' bind:value={title}/>
        <input type='text' id='author' placeholder='Författare' bind:value={author} />
        <button type='submit'>Lägg till</button>
    </form>
</section>

<style>
    section {
        margin-top: 20px;
        padding-bottom: 100px;
    }
    h4 {
        text-transform: uppercase;
        font-weight: 100;
        font-size: 2em;
    }
</style>