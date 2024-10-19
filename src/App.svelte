<script>
  import Schedule from './Schedule.svelte';
  import CourseForm from './CourseForm.svelte';

  let courses = [];

  async function fetchSchedule(courseCodes) {
    try {
      let formData = new FormData();
      formData.append('course_codes', courseCodes);
      formData.append('block', "2024;FA");
      const response = await fetch('http://3.88.240.136:5000/submitcodes', {
      // const response = await fetch("http://localhost:5000/submitcodes", {
        method: 'POST',
        body: formData
      });
      courses = await response.json();
      console.log(courses);
    } catch (error) {
      console.error('Error fetching schedule:', error);
    }
  }
  function handleFormSubmit(event) {
    fetchSchedule(event.detail.courseCodes);
  }
</script>

<div>
  <CourseForm on:submit={handleFormSubmit} />
  <h1>Your Weekly Schedule</h1>
  <Schedule {courses} />
</div>
