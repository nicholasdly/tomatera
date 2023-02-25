<script>
    let work_duration = 25;  // minutes
    let break_duration = 5;  // minutes

    let paused = true;
    let working = true;

    let minutes = work_duration;
    let seconds = 0;

    let interval;

    function tick() {
        if (minutes <= 0 && seconds <= 0) {
            minutes = working ? break_duration : work_duration;
            working = !working;
        } else if (seconds <= 0) {
            minutes--;
            seconds = 59;
        } else {
            seconds--;
        }
    }

    function toggle_pause() {
        if (paused) {
            interval = setInterval(() => {
                tick();
            }, 1000);
        } else {
            clearInterval(interval);
        }
        paused = !paused;
    }

    function reset() {
        clearInterval(interval);
        paused = true;
        working = true;
        minutes = work_duration;
        seconds = 0;
    }
</script>

<h2>
	{`${minutes}:${seconds.toString().padStart(2,'0')}`}
</h2>
<button on:click={toggle_pause}>
    {paused ? 'Start' : 'Stop'}
</button>
<button on:click={reset}>
    Reset
</button>