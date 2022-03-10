<script context="module">
    let monaco_promise
    let _monaco

    monaco_promise = import("./monaco.js")
    monaco_promise.then((mod) => {
        _monaco = mod.default
    })
</script>

<script>
    import { onMount } from "svelte"
    import { createEventDispatcher } from "svelte"

    const dispatch = createEventDispatcher()

    export let value

    let editor
    let monaco
    let container

    const init = (editor) => {
        editor.onDidChangeModelContent((event) => {
            dispatch("change", editor.getValue())
            value = editor.getValue()
        })
    }

    onMount(() => {
        if (_monaco) {
            monaco = _monaco
            editor = monaco.editor.create(container)
            init(editor)
        } else {
            monaco_promise.then(async (mod) => {
                console.log(container)
                monaco = mod.default
                editor = monaco.editor.create(container, {
                    value: value,
                    language: "scss"
                })

                init(editor)
            })
        }

        return () => {
            // destroyed = true
        }
    })
</script>

<div class="monaco-container" bind:this={container} style="width: 800px; height: 100%; text-align: left" />
