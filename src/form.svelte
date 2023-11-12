
<script>
    import { createForm } from "svelte-forms-lib";
    import * as yup from "yup";

    const { form,errors,state, handleChange, handleSubmit } = createForm({
      initialValues: {
        title: "",
        name: "",
        email: "vvv@mm.com"
      },

validationSchema:yup.object().shape({
    name:yup.string().required(),
    email:yup.string().email().required()
}),


      
      onSubmit: values => {
        alert(JSON.stringify(values.email));
      },
      }
        );

  </script>
<div>
    {JSON.stringify($errors)}
</div>
<div>
    {JSON.stringify($form)}
</div>

  <form on:submit={handleSubmit}>
    <label for="title">title</label>
    <select
      id="title"
      name="title"
      on:change={handleChange}
      bind:value={$form.title}>
      <option></option>
      <option>Mr.</option>
      <option>Mrs.</option>
      <option>Mx.</option>
    </select>

    <label for="name">name</label>
    <input
      id="name"
      name="name"
      on:change={handleChange}
      on:blur={handleChange}
      bind:value={$form.name}
    />
{#if $errors.name}
     <small>
       {$errors.name}
     </small>
{/if}


    <label for="email">email</label>
    <input
      id="email"
      name="email"
      on:change={handleChange}
      bind:value={$form.email}
    />

    <button type="submit">Submit</button>
  </form>
