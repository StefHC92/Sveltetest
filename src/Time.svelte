<script>
    import Progress from './Progress.svelte';
    const totalSeconds = 20;
    let secondsLeft = totalSeconds;
    let isRunning = false;
    $: progress = (totalSeconds - secondsLeft)/totalSeconds * 100;
   

    function startTimer (){
        isRunning = true;
        const timer = setInterval(()=> {
        secondsLeft -= 1;
        if (secondsLeft == 0) {
            clearInterval(timer);
            isRunning = false;
            secondsLeft = totalSeconds;
            playSound();
         
        }
    },1000);
    }

    function playSound (){
        let audio = new Audio('/assets/oh_yeah.wav');
        audio.play();
    }
</script>

<style>
    h2 {
        margin: 100;
    }

    .start {
	width: 100%;
	margin: 10px 0;
	background-color:rgb(154, 73, 73);
    }

    .start[disabled]{
        background-color: gray;
        cursor: not-allowed;
    }
</style>


<div bp='grid'>
    <h2 bp='offset-5@md 4@md 12@sm'> 
        Seconds Left: {secondsLeft}
    </h2>
</div>

    <Progress progress = {progress}/>

<div bp='grid'>

    <button 
        disabled={isRunning} 
        on:click={startTimer} 
        bp='offset-5@md 4@md 12@sm' class='start'>
        Start
    </button>
</div>