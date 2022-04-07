# mirror-tracing
A mirror tracing task written in JavaScript. The task can be used in **SoSci Survey** surveys following the steps below.

## Use in SoSci Survey
- Create a new text element in SoSci Survey as "HTML Code"
- Create a new question element in SoSci Survey as "Internal Variables" 
    - Add additional internal variables under the same question element if required

- Create a new survey and add both the text and the question element to the survey (Note: the (invisible) question element needs to be placed **before** the text element for the variables to be loaded before the JS code is executed)

- Place below code in inside the HTML section of the text element (see comments in code)

```html
<div style="width: 400px; height: 300px; position: relative; margin: auto;">
    <canvas id="mirror" width="400" height="300"
            style="width: 100%; height: 100%; position: absolute; top: 0; left: 0; border: 1px solid #000000;"></canvas>
    <canvas id="mirror_top" width="400" height="300"
            style="width: 100%; height: 100%; position: absolute; top: 0; left: 0; border: 1px solid #000000;"></canvas>
</div>
<div style="width: 400px; height: 300px; position: relative; margin: auto;">
    <canvas id="paint" width="400" height="300" style="border: 1px solid #000000;"></canvas>
</div>
<div style="width: 400px; position: relative; margin: auto; font-size: large; font-family: sans-serif;">

    <div style="display: flex; justify-content: center; padding: 1em;">
        <div id="status_div" style="font-weight: bold;"></div>
    </div>

    <div style="display: flex; justify-content: space-between; padding: 0 1em;">
        <div id="errors_div">Errors: 0</div>
        <div id="time_div"></div>
    </div>
</div>

<script src="https://cdn.jsdelivr.net/gh/mxwebdev/mirror-tracing@113e887043847d44b4fa292ebb1efd9faaa9e3c1/mt.js">
</script>

<script>
    // Start Mirror Trace
    do_mirror(0);
    // Define input elements to store values in SoSci Survey
    var mt_errors = document.getElementById("MT02_01");
    var mt_timeSpent = document.getElementById("MT02_02");
    var mt_finished = document.getElementById("MT02_03");

    function updateScore() {
        mt_errors.value = errors;
        mt_timeSpent.value = timeSpent;
        mt_finished.value = finished;
        // Disable submit button until task is finished (remove if not needed)
        submitButton = document.getElementById('submit0');
        if (!finished) {
            submitButton.disabled = true;
        } else {
            submitButton.disabled = false;
        }
    }
    // Store values in SoSci Survey variables
    SoSciTools.attachEvent(window, "load", function (evt) {
        window.setInterval(updateScore, 500);
        updateScore();
    });
</script>
````
