<script>
  import CustomInput from "./CustomInput.svelte"
  import Toggle from "./Toggle.svelte"

  let val = ''
  let selectedOption = 1;

  $: console.log(val)
  $: console.log(selectedOption)

  function setValue(event) {
    val = event.target.value
  }
</script>

<!-- <input type="text" value={val} on:input={setValue}> -->
<!-- <input type="text" bind:value={val}> -->
<!-- these two lines are written the same way, they both setup a two-way binding, the second line is just shorter -->

<CustomInput bind:val={val}/>
<!-- this is the samething as the code above, except it is in another component -->

<Toggle bind:chosenOption={selectedOption}/>