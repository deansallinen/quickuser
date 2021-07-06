<script>

	import { fade } from "svelte/transition";
	let user = (async () => { 
			const response = await fetch('https://randomuser.me/api/?nat=AU,BR,CA,CH,DE,DK,ES,FI,FR,GB,IE,NO,NL,NZ,TR,US&inc=name,login,nat&noinfo&password=special,upper,lower,number,32') 
			let res = await response.json() 
			console.log(res.results[0])
			return res.results[0]
			})()

</script>

<main>
{#await user}
	<div />
{:then user}
	<div transition:fade={{ duration: 200 }}>
	<h1>{user.name.first} {user.name.last}</h1>

	<span><h4>Username </h4><input value={user.login.username}></span>
	<span><h4>Password </h4><input value={user.login.password}></span>
	<span><h4>Salt </h4><input value={user.login.salt}></span>

	<span><h4>SHA1 </h4><input value={user.login.sha1}></span>
	<span><h4>SHA256 </h4><input value={user.login.sha256}></span>
	<span><h4>UUID </h4><input value={user.login.uuid}></span>
	</div>

{:catch error}
	<p>{error.message}</p>
{/await}
</main>

<style>

  main {
	display: flex;
	height: 100vh;
	max-width: 40ch;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	max-width: 40ch;
	margin: 0 auto;
  }

main div h1{
	text-align: center;
}	

input {
	font-family: monospace;
	width: 40ch;
}
h4 {
	font-weight: semi-bold;
	margin-bottom: .5em;
}
</style>
