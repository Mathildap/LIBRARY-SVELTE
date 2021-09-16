<script>
    export let book = {};
    export let onLoan;

    const loanBookHandler = (e) => {
        onLoan(e.target.id);
    };

</script>

<article>
    <!-- svelte-ignore a11y-missing-attribute -->
    <img src={book.img} />
    <div>
        <h3>{book.title}</h3>
        <h4>{book.author}</h4>
        {#if book.onloan === false}
            <button on:click={loanBookHandler} id={book.id}>Låna</button>
        {:else}
            <p class="onloan">Utlånad</p>
            <p class="returnBook" on:click="{loanBookHandler}" id={book.id}>Lämna tillbaka</p>
        {/if}
    </div>
</article>

<style>
    article {
        margin: 5px;
        box-shadow: 2px 2px 5px rgb(194, 194, 194);
        border-radius: 3px;
        min-width: 24%;
    }
    h3 {
        text-transform: uppercase;
		font-size: 1.8em;
		font-weight: 100;
        margin: 0;
        margin-top: 10px;
    }
    h4 {
		font-size: 1.2em;
		font-weight: 100;
        margin: 0;
        margin-bottom: 15px;
    }
    p {
        font-size: 1em;
		font-weight: 100;
    }
    .onloan {
        font-style: italic;
    }
    .returnBook {
        text-decoration: underline;
        cursor: pointer;
    }
    .returnBook:hover {
        color: rgb(179, 179, 179);
    }
    button {
        padding: 5px 15px;
        margin-top: 10px;
        border: 1px solid black;
        background-color: white;
    }
    button:hover {
        border-color: rgb(201, 201, 201);
        color: rgb(201, 201, 201);
    }
</style>