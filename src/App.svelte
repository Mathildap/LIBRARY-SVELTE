<script>
	import Library from './Library.svelte';
	import NewBook from './NewBook.svelte';
	export let doUpdate = false;
	let newBook;
	
	const newBookHandler = (info) => {
		console.log(info);

		let title = info.title;
		let author = info.author;

		let newBook = {'title': title, 'author': author, 'img': './img/nopic.png', 'onloan': false};

		fetch('http://localhost:3000/books', 
        {method: 'POST', 
        headers: {'Content-type': 'application/json'}, body: JSON.stringify(newBook)
        })
        .then(res => res.json())
        .then(data => {
            console.log(data);
			newBook = true;
        })
        .catch(err => console.log(err));
		doUpdate = !doUpdate
	}

</script>

<main>
	<h1>Välkommen till Biblioteket!</h1>
	<h2>Nyheter</h2>
	{#key doUpdate}
		<Library {newBook} />
	{/key}
	<NewBook {newBookHandler} />
</main>

<style>
	main {
		text-align: center;
		margin: 0 auto;
	}
	h1 {
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}
	h2 {
		font-size: 2em;
		font-weight: 100;
	}
</style>