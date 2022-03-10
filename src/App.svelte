<script>
    import Monaco from "./components/monaco/monaco-editor.svelte"

    let value = `body { color: red; }`
</script>

<div id="app">
    <button
        on:click={() => {
            console.log(value)
        }}>show value</button
    >

    <Monaco bind:value on:change={({ detail }) => console.log(detail)} />
</div>

<style>
    #app {
        width: 100vw;
        height: 100vh;
        position: relative;
        display: grid;
        justify-content: center;
        align-content: center;

        grid-template-columns: 100%;
        grid-template-rows: 100%;
    }

    * :global(.buttons) {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
        width: 500px;
    }
</style>
