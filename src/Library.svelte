<script>
    import { onMount, beforeUpdate, afterUpdate } from "svelte";
    import Book from './Book.svelte';
    import newBook from './App.svelte';
    export let library = [];
    let updateOnLoan;

    $: console.log(updateOnLoan);

    onMount(() => {
        fetch('http://localhost:3000/books')
        .then(res => res.json())
        .then(data => {
            library = data;
        })
    })

    beforeUpdate(() => {
        if (updateOnLoan === true) {
            fetch('http://localhost:3000/books')
            .then(res => res.json())
            .then(data => {
                library = data;
            })
        }
    });

    afterUpdate(() => {
        updateOnLoan = false;
    });

    const onLoan = (id) => {
    let bookId = parseInt(id);

    fetch('http://localhost:3000/books')
    .then(res => res.json())
    .then(data => {
        let answer;

        data.forEach(book => {
            if (book.id === bookId) {
                if (book.onloan === false) {
                    answer = true;    
                } else {
                    answer = false;
                };
            };
        });

        fetch('http://localhost:3000/books/'+ bookId, {
        method: 'PATCH',
        body: JSON.stringify({
        onloan: answer
        }),
        headers: {
        'Content-type': 'application/json'
        }
        })
        .then(response => response.json())
        .then(data => {
            updateOnLoan = true;
        });
    });
};

</script>

<section>
    {#each library as book}
        <Book {book} {onLoan}/>
        {:else} 
        <div>Laddar...</div>
    {/each}
</section>

<style>
    section {
        display: flex;
        justify-content: flex-start;
        flex-wrap: wrap;
        margin-left: 25px;
    }
</style>