   <script>
    export let courses = [];

    const daysOfWeek = ['M', 'T', 'W', 'R', 'F'];
    const hoursInDay = 16; // Define the total number of hours you want to display (8 AM to 10 PM)
    const blockHeight = 100; // Height of each hour block in pixels
  
    const getTopPosition = (start) => {
      // Convert start time to a top position in pixels
      return (start - 5) * blockHeight; // Assuming classes start at 5 AM
    };
  
    const getCourseHeight = (start, end) => {
      // Calculate the height based on the start and end times
      return (end - start) * blockHeight;
    };

    function formatTime(time) {
        const hours = Math.floor(time);
        const minutes = Math.round((time - hours) * 60);
        const period = hours >= 12 ? 'PM' : 'AM';
        const formattedHours = hours % 12 || 12;
        const formattedMinutes = minutes.toString().padStart(2, '0');
        return `${formattedHours}:${formattedMinutes} ${period}`;
    }
  </script>
  
  <style>
    .schedule-container {
        display: grid;
        grid-template-columns: auto 1fr;
        gap: 10px;
        position: relative;
        padding-right: 10px;
    }
    .schedule {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 10px;
      position: relative;
      height: 1400px; /* Total height for the schedule */
    }
    .day-header {
      font-weight: bold;
      text-align: center;
    }
    .course {
      position: absolute;
      border: 1px solid #ccc;
      padding: 0px;
      border-radius: 5px;
      background-color: #f9f9f9;
      transition: background-color 0.3s;
      left: 0;
      right: 0;
    }
    .course:hover {
      background-color: #e0e0e0; /* Change background on hover */
    }
    .hour-line {
        position: absolute;
        width: 100%;
        border-top: 1px solid #ddd;
    }
    .time-labels {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        height: 1400px;
        padding-right: 10px;
    }
    .time-label {
        text-align: right;
        padding-right: 5px;
        font-size: 14px;
        color: #666;
        height: 100px;
        line-height: 100px;
        font-weight: bold;
    }
  </style>
  
  <div class="schedule-container">
    <div class="time-labels">
        {#each Array(hoursInDay) as _, i}
            <div class="time-label">{(i + 5) % 12 || 12}:00</div> <!-- Assuming classes start at 5 AM -->
        {/each}
    </div>
  <div class="schedule">

    {#each daysOfWeek as day}
      <div class="day-header">{day}</div>
    {/each}
  
    {#each daysOfWeek as day}
      <div style="position: relative; height: 1400px;"> <!-- Relative positioning for each day -->
        {#each Array(hoursInDay) as _, i}
            <div class="hour-line" style="top: {i * 100}px;"></div> <!-- Assuming each hour is 50px high -->
        {/each}
        {#each courses as course}
          {#each course.times as time}
            {#if time.day === day}
              <div 
                class="course"
                style="
                  top: {getTopPosition(time.start)}px; 
                  height: {getCourseHeight(time.start, time.end)}px;
                ">
                <strong>{course.title}</strong><br>
                {course.course_code}-{course.section_number}<br>
                {formatTime(time.start)} - {formatTime(time.end)} 
              </div>
            {/if}
          {/each}
        {/each}
      </div>
    {/each}
  </div>
  </div>
  