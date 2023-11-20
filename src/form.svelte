<script>
    //https://svelte-forms-lib-sapper-docs.vercel.app/introduction
    //npm i svelte-forms-lib

    // https://www.npmjs.com/package/yup
    //npm i yup

    import { createForm } from "svelte-forms-lib";
    import * as yup from "yup";

    const { isValid, form, errors, state, handleChange, handleSubmit } =
        createForm({
            initialValues: {
                title: "Mr.",
                name: "",
                email: "vvv@mm.com",
                password: "",
                confirmpwd: "",
            },

            validationSchema: yup.object().shape({
                name: yup
                    .string()
                    .min(3, "имя д.б. не менее 3-х символов")
                    .required("Укажите, пожалуйста, имя"),

                email: yup
                    .string()
                    .email("Укажите корректный email")
                    .required(),

                title: yup.string().oneOf(["Mr,", "Mrs", "Mx."]).required(),

                password: yup.string().required("Укажите, пожалуйста, пароль"),

                confirmpwd: yup
                    .string()
                    .oneOf([yup.ref("password")], "Пароли не совпадают"),
            }),

            onSubmit: (values) => {
                alert(JSON.stringify(values.email));
            },
        });
</script>

<div>{$isValid}</div>
<!-- <div>
    {JSON.stringify($errors)}
</div>
<div>
    {JSON.stringify($form)}
</div> -->
<div class= "py-8 flex flex-col justify-center sm:py-12">
    <div class="relative py-3 sm:max-w-xl sm:mx-auto">
      <div class="absolute inset-0 bg-gradient-to-r from-amber-600 to-amber-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 rounded-3xl"></div>
      <div class="relative px-4 py-10 bg-orange-200 shadow-lg sm:rounded-3xl sm:p-20">
        <div class="max-w-md mx-auto">
          <div>
            <h1 class="text-2xl font-semibold">Login</h1>
          </div>
          <div class="divide-y divide-gray-200">
            <div class="py-8 text-base leading-6 space-y-4 text-gray-200 sm:text-lg sm:leading-7">
              <div class="relative">
                <input on:change={handleChange} 
                on:blur={handleChange} 
                bind:value={$form.name}  
                autocomplete="off" id="email" name="email" type="text" class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:borer-rose-600" placeholder="Email address" />
                <label for="email" class="absolute left-0 -top-3.5 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-440 peer-placeholder-shown:top-2 transition-all peer-focus:-top-3.5 peer-focus:text-gray-600 peer-focus:text-sm">Email Address</label>
              </div>
              <div class="relative">
                <input on:change={handleChange} 
                on:blur={handleChange} 
                bind:value={$form.password} 
                autocomplete="off" id="password" name="password" type="password" class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:borer-rose-600" placeholder="Password" />
                <label for="password" class="absolute left-0 -top-3.5 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-440 peer-placeholder-shown:top-2 transition-all peer-focus:-top-3.5 peer-focus:text-gray-600 peer-focus:text-sm">Password</label>
              </div>
              <div class="relative"> 
                <button on:submit={handleSubmit}
                disabled={!$isValid}
                class ="bg-amber-500 text-white rounded-md px-2 py-1"> Submit</button>
              </div>
            </div>
          </div>
          <div class="alert alert-warning">
            {#if $errors.email} {$errors.email} {/if}
            <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current shrink-0 h-5 w-5" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" /></svg>
          </div>
        </div>
        <div class="alert alert-warning">
        {#if $errors.password}{$errors.password}{/if}
        <svg xmlns="http://www.w3.org/2000/svg" class="stroke-current shrink-0 h-5 w-5" fill="none" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" /></svg>
        </div>
      </div>
    </div>
  </div>
  