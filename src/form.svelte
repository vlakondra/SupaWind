<script>
    import { createForm } from "svelte-forms-lib";
    import * as yup from "yup";

    const { isValid, isValidating,form, errors, state, handleChange, handleSubmit } = createForm({
        initialValues: {
            title: "Mr.",
            name: "",
            email: "vvv@mm.com",
        },

        validationSchema: yup.object().shape({
            name: yup.string().
            min(3,"имя д.б. не менее 3-х символов").
            required("Укажите, пожалуйста, имя"),

            email: yup.string().
            email("укажите корректный email").
            required(),

            title:yup.string().
            oneOf(["Mr,","Mrs","Mx."]).
            required()
        }),

        onSubmit: (values) => {
            alert(JSON.stringify(values.email));
        },
    });
</script>
<div>{$isValid}</div>
<div>
    {JSON.stringify($errors)}
</div>
<div>
    {JSON.stringify($form)}
</div>

<form on:submit={handleSubmit}>
    <div>
        <label for="title">title</label>
        <select
            id="title"
            name="title"
            on:change={handleChange}
            bind:value={$form.title}
        >
            <option />
            <option>Mr.</option>
            <option>Mrs.</option>
            <option>Mx.</option>
        </select>
    </div>
    <div>
        <label for="name">name</label>
        <input
            id="name"
            name="name"
            on:change={handleChange}
            on:blur={handleChange}
            bind:value={$form.name}
        />
        {#if $errors.name}
          <p>
            <small>
                {$errors.name}
            </small>
        </p>
        {/if}
    </div>
    <div>
        <label for="email">email</label>
        <input
            id="email"
            name="email"
            type='email'
            on:change={handleChange}
            on:blur={handleChange}
            bind:value={$form.email}
        />
        {#if $errors.email}
        <small>
            {$errors.email}
        </small>
    {/if}
    </div>
    <p>
        <button disabled={!$isValid} type="submit">Submit</button>
    </p>
</form>
