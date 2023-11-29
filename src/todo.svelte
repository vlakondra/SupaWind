<script>
    import { onMount } from "svelte";
    import { supabase } from "./store";
    import { supauser } from "./store";

    let todos = null;

    onMount(async () => {
        let { data: mytodos, error } = await supabase
            .from("mytodos")
            .select("*");

        if (mytodos) {
            todos = mytodos;
        }
    });

    async function addToList() {
       

        const { data, error } = await supabase
            .from("mytodos")
            .insert([{ content: "новое дело 6", done: false }])
            .select();

            console.log(error, data)
            if (data){
                todos = [...todos, { content: data[0].content, done: data[0].done }];
            }
    }
</script>

<div>
    <div>
        {#if todos}
            {#each todos as item}
                <p>
                    {item.content}
                </p>
            {/each}
        {:else}
            <p>Загрузка данных...</p>
        {/if}
    </div>
    <div>
        <button on:click={addToList}>
            Добавить
        </button>
    </div>
    <div>
        <button on:click={refresh}>
            Обновить
        </button>
    </div>
</div>
