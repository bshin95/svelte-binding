<script>
  import CustomInput from "./CustomInput.svelte"
  import Toggle from "./Toggle.svelte"
  import { isValidEmail } from './validation'

  let val = ''
  let price = 0;
  let selectedOption = 1;
  let agreed;
  let favColor = 'red';
  let singleFavColor = 'red';
  let usernameInput;
  let customInput;
  let enteredEmail;
  let formIsValid = false;

  $: if (isValidEmail(enteredEmail)) {
    formIsValid = true;
  } else {
    formIsValid = false;
  }

  $: console.log(val)
  $: console.log(selectedOption)
  $: console.log(price)
  $: console.log(agreed)
  $: console.log(favColor)
  $: console.log(singleFavColor)
  $: console.log(customInput)

  function setValue(event) {
    val = event.target.value
  }

  function saveData() {
    // console.log(document.querySelector('#username').value)
    console.log(usernameInput.value)
    customInput.empty();
  }
</script>


<!-- <input type="text" value={val} on:input={setValue}> -->
<!-- <input type="text" bind:value={val}> -->
<!-- these two lines are written the same way, they both setup a two-way binding, the second line is just shorter -->

<!-- ******* Custom component binding ******* -->
<CustomInput bind:val={val} bind:this={customInput}/>
<!-- this is the samething as the code above, except it is in another component -->

<Toggle bind:chosenOption={selectedOption}/>

<input type="number" bind:value={price}>

<!-- ******* Checkbox binding ******* -->
<label>
  <input type="checkbox" bind:checked={agreed}/>
  Agree to terms?
</label>

<!-- ******* radio binding/group binding ******* -->
<h1>Favorite color?</h1>
<label>
  <input type="radio" name="color" value="red" bind:group={favColor}>
  Red
</label>
<label>
  <input type="radio" name="color" value="green" bind:group={favColor}>
  Green
</label>
<label>
  <input type="radio" name="color" value="blue" bind:group={favColor}>
  Blue
</label>

<!-- ******* select binding ******* -->
<select bind:value={singleFavColor}>
  <option value="green">Green</option>
  <option value="red">Red</option>
  <option value="blue">Blue</option>
</select>

<!-- ******* element references binding ******* -->
<hr>

<input type="text" bind:this={usernameInput}>
<button on:click="{saveData}">Save</button>

<hr>
<h1>Email checker</h1>
<form on:submit|preventDefault>
  <input type="email" bind:value={enteredEmail} class={isValidEmail(enteredEmail) ? '' : 'invalid'}>
  <button type="submit" disabled={!formIsValid}>Save</button>
</form>