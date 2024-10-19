<script>
  import Schedule from './Schedule.svelte';
  import CourseForm from './CourseForm.svelte';

  let courses = [];
  let loading = false;
  let _error = null;

  async function fetchSchedule(courseCodes) {
    try {
      loading = true;
      _error = null;
      let formData = new FormData();
      formData.append('course_codes', courseCodes);
      formData.append('block', "2024;FA");
      // const response = await fetch('http://api.coursebuilder.trevinjones.com:5000/submitcodes', {
      const response = await fetch("http://localhost:5000/submitcodes", {
        method: 'POST',
        body: formData
      });
      courses = await response.json();
      console.log(courses);
    } catch (error) {
      console.error('Error fetching schedule:', error);
      _error = error;
    } finally {
      loading = false;
    }
  }
  function handleFormSubmit(event) {
    fetchSchedule(event.detail.courseCodes);
  }
</script>

<div>
  <CourseForm on:submit={handleFormSubmit} />
  <h1>Your Weekly Schedule</h1>
  {#if loading}
    <p>Loading...</p>
  {/if}
  {#if _error !== null}
    <p style="color: red;">Error fetching schedule. Please try again with different course codes.</p>
  {/if}
  <Schedule {courses} />
</div>
