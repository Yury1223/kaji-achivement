<script lang="ts">
	import LoginStamp from './LoginStamp/LoginStamp.svelte'
    import { onMount } from 'svelte'

	let totalCost = 0
	let useCost = 0
	let inited = false

	$: {
		save(totalCost)
	}
	
	onMount (
		() => {
			totalCost = Number(window.localStorage.getItem('totalcost'))
			inited = true
		}
	)

	function save (e) {
		if (!inited) return
		window.localStorage.setItem('totalcost', `${e}`)
	}

	function onClickUsePoint () {
		if (useCost <= 0) {
			return
		}

		if (totalCost - useCost < 0) {
			window.alert('ポイントが足りません')
			return
		}

		if (window.confirm('ポイントを使っても良いですか？')){
			totalCost = totalCost - useCost
			save (totalCost)
			window.alert('ポイントを使いました')
		}
	}
</script>

<main>
	<h1>🍣達成したら押そう🍣</h1>
	<h2>現在のポイント</h2>
	<p>{totalCost}</p>
	<h2>500ポイント: 欲しいもの</h2>
	<h2>100ポイント: 🍣</h2>
	<div class="use-wrapper">
		<input type="number" label="ポイントを使う" bind:value={useCost}/>
		<button on:click="{onClickUsePoint}">pt 使う！</button>
	</div>
	<LoginStamp label="お風呂掃除" cost="{10}" bind:value="{totalCost}"/>
	<LoginStamp label="トイレ掃除" cost="{9}" bind:value="{totalCost}"/>
	<LoginStamp label="洗面台掃除" cost="{8}" bind:value="{totalCost}"/>
	<LoginStamp label="キッチン掃除" cost="{7}" bind:value="{totalCost}"/>
	<LoginStamp label="床掃除" cost="{6}" bind:value="{totalCost}"/>
	<LoginStamp label="自炊" cost="{10}" bind:value="{totalCost}"/>
	<LoginStamp label="毎日500円貯金する" cost="{5}" bind:value="{totalCost}"/>
	<LoginStamp label="体操する" cost="{1}" bind:value="{totalCost}"/>
	<LoginStamp label="コーディングする" cost="{4}" bind:value="{totalCost}"/>
</main>

<style>
	main {
		padding: 16px;
	}

	h1, h2, p {
		display: block;
		text-align: center;
	}


	h2, p {
		margin: 16px 0;
	}

	p {
		font-size: 32px;
		font-weight: bold;
	}

	.use-wrapper {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.use-wrapper > button {
		margin-left: 16px;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>