<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    import { onMount } from "svelte";
    import { supabase } from "./store";
    import { supauser } from "./store";

    let todos = null;

    onMount(
        //Обработка создания компонента
        async () => {
            refresh();
        },
        // async () => {
        // let { data: mytodos, error } = await supabase
        //     .from("mytodos")
        //     .select("*");

        // if (mytodos) {
        //     todos = mytodos;
        // }
    );

    async function refresh() {
        //Обновление
        let { data: mytodos, error } = await supabase
            .from("mytodos")
            .select("*");

        if (mytodos) {
            todos = mytodos;
        }
    }

    async function addToList() {
        //обработка (fake) добавления
        const { data, error } = await supabase
            .from("mytodos")
            .insert([{ content: "новое дело 6", done: false }])
            .select();

        console.log(error, data);
        if (data) {
            todos = [
                ...todos,
                {
                    id: data[0].id,
                    content: data[0].content,
                    done: data[0].done,
                },
            ];
        }
    }
    async function onChange(ev) {
        //обработка checkBox

        console.log(ev.srcElement.checked);

        const { data, error } = await supabase
            .from("mytodos")
            .update({ done: ev.srcElement.checked })
            .eq("id", ev.srcElement.id)
            .select();

        console.log(data, error);
    }
</script>

<div>
    {#if todos}
        <div class="flex flex-col">
            {#each todos as item}
                <div
                    class="[&:not(:first-child)]:border-l
                            [&:not(:first-child)]:border-r
                            [&:not(:first-child)]:border-b
                            [&:first-child]:border
                            border-gray-400
                            flex flex-row
                            justify-between
                            p-2
                            rw"
                >
                    <div>
                        {item.id}
                    </div>
                    <div>
                        <input
                            id={item.id}
                            on:change={onChange}
                            bind:checked={item.done}
                            type="checkbox"
                        />
                    </div>
                    <div class="grow" style=" text-align:right" >
                        {item.content}
                    </div>
                </div>
            {/each}
        </div>
    {:else}
        <p>Загрузка данных...</p>
    {/if}

    <div>
        <button on:click={addToList}> Добавить </button>
    </div>
    <div>
        <button on:click={refresh}> Обновить </button>
    </div>
</div>

<style>
    /* .rw:first-child {
        border: 1px solid red;
    }
    .rw:not(:first-child) {
        border: 1px solid red;
        border-width: 0 1px 1px 1px;
    } */

    /* .rw{
        border-bottom: 1px solid blue;
        } */
</style>
