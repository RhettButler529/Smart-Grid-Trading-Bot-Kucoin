<template>
    <div>              
        <div id="consoleDiv">
            <h2 class="no-margin">console</h2>
            <div class="consoleFrame"><code id="console"></code></div>
            <em><input id="logError" type="checkbox" checked=""> Error
                <input id="logInfo" type="checkbox" checked=""> Info
                <input type="button" value="Clear" onclick="document.getElementById('console').innerHTML = ''">
            </em>
        </div>
        <div id="controlsDiv" style="display:none">
            <h2 class="no-margin">controls</h2>
            <div id="orientationDiv" class="mraid-widget">
                <div id="orientationToggle" :class="orientationV" @click="toggleOrientation"></div>
                <div id="orientationTiming" type="button" @click="toggleOrientationTiming" :class="state"></div>
                <p class="formValues"><span class="value">
                <select name="orientationState" id="orientationState" v-model="orientationV" @change="rotate">
                    <option value="portrait">portrait</option>
                    <option value="landscape">landscape</option>
                </select>
                </span>
                </p>
            </div>

        </div>
                

    </div>
</template>

<script setup>
    const orientationV = ref("portrait")
    const state = ref("t-off")
    const timer = ref(null)
    const interval = ref(null)
    function rotate(){
        mraidview.rotateOrientation();
    }
    function toggleOrientation(){
        if(orientationV.value == "portrait") orientationV.value = "landscape"
        else orientationV.value = "portrait"
        rotate()
    }
    function toggleOrientationTiming(){
        if (state.value == "t-off") {
            
            timer.value = prompt("Enter number of milliseconds to update orientation state", 1000);
            interval.value = setInterval(toggleOrientation, timer.value);
            state.value = "t-on"
        } else {
            clearInterval(interval.value);
            state.value =  "t-off";
        }
    }

</script>