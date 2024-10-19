<script>
  import Schedule from './Schedule.svelte';

  let courses = [
    {
      name: "Course 1",
      times: [
        {
          day: "M",
          start: 7.0,
          end: 10.0
        },
        {
          day: "W",
          start: 8.0,
          end: 10.0
        }
      ],
      course_code: "CSC 101",
      section_num: "01",
      delivery_method: "In-Person",
      block: "Full",
      title: "str",
      num_credits: 3.0
    },
    {
      name: "Course 2",
      times: [
        {
          day: "M",
          start: 10.0,
          end: 12.0
        },
        {
          day: "W",
          start: 10.5,
          end: 12.0
        }
      ],
      course_code: "CSC 102",
      section_num: "01",
      delivery_method: "In-Person",
      block: "Full",
      title: "str",
      num_credits: 3.0
    },
    {
      name: "Course 3",
      times: [
        {
          day: "T",
          start: 12.0,
          end: 14.0
        },
        {
          day: "R",
          start: 12.0,
          end: 14.0
        }
      ],
      course_code: "CSC 103",
      section_num: "01",
      delivery_method: "In-Person",
      block: "Full",
      title: "str",
      num_credits: 3.0
    }
  ];
</script>

<div>
  <h1>Your Weekly Schedule</h1>
  <Schedule {courses} />
</div>
