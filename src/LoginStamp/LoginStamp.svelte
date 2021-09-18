<script lang="ts">
	export let value = 0
	export let cost = 1
    export let label = ''

	function onClick () {
		value += cost
	}
</script>

<div>
	<button on:click="{onClick}">{label}</button>
</div>

<style>
	div {
		width: 100%;
        margin-bottom: 16px;
	}

    button {
        width: 240px;
        margin: 0 auto;
        display: block
    }

	@media (min-width: 640px) {
		button {
			max-width: none;
		}
	}
</style>