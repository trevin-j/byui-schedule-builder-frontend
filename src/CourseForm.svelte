<script>
  import { createEventDispatcher } from 'svelte';

  let courseCodes = '';
  const dispatch = createEventDispatcher();

  function handleSubmit(event) {
    event.preventDefault();
    // const codesArray = courseCodes.split(',').map(code => code.trim());
    dispatch('submit', { courseCodes: courseCodes });
  }
</script>

<style>
  .course-form {
    margin-bottom: 20px;
  }
  .course-form input {
    padding: 8px;
    margin-right: 10px;
    font-size: 14px;
  }
  .course-form button {
    padding: 8px 12px;
    font-size: 14px;
    cursor: pointer;
  }
</style>

<form class="course-form" on:submit={handleSubmit}>
  <label for="courseCodes">Enter course codes, separated by commas:</label>
  <br />
  <input
    type="text"
    placeholder="E.g. CSE 110, CSE 210"
    bind:value={courseCodes}
  />
  <button type="submit">Submit</button>
</form>