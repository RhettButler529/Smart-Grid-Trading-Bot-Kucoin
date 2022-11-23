<script setup>
    
    const screenWidth = ref(320)
    const screenHeight = ref(480)
    const adMaxWidth = ref(320)
    const adMaxHeight = ref(480)
    const adWidth = ref(320)
    const adHeight = ref(480)
    const adTop = ref(0)
    const adLeft = ref(0)
    const adMaxTop = ref(0)
    const adMaxLeft = ref(0)
    const offsetTop = ref(100)
    const offsetLeft = ref(500)
    const features = ref([
        'sms',
        'tel',
        'calendar',
        'storePicture',
        'inlineVideo',
        'vpaid'
])

    const emit = defineEmits(['next-tab'])
    function nextTab(){
        emit('next-tab', 2)
    }
    function resizeInitialAdSize(left, top, width, height){
        adWidth.value = width
        adHeight.value = height
        adLeft.value = left-offsetLeft.value
        adTop.value = top-offsetTop.value

    }
    function dragInitialAdSize(left, top){
        adLeft.value = left-offsetLeft.value
        adTop.value = top-offsetTop.value

    }
    function resizeMaxAdSize(left, top, width, height){
        adMaxWidth.value = width
        adMaxHeight.value = height
        adMaxLeft.value = left - offsetLeft.value
        adMaxTop.value = top - offsetTop.value
    }
    function dragMaxAdSize(left, top){
        adMaxLeft.value = left - offsetLeft.value
        adMaxTop.value = top - offsetTop.value
    }
    function resizeScreensize(left, top, width, height){
        screenWidth.value = width
        screenHeight.value = height
        
    }
    function dragScreensize(left, top){
        // offsetLeft.value = left
        // offsetTop.value = top
    }
    
</script>

<template>
    <div>        
        <h2 class="no-margin">properties</h2>
        <div id="propertiesDiv" style="display:none">
            <div id="propertiesSelectDiv">
            <div id="deviceDiv">
                <p class="no-margin">Device geometry:<br/>
                <table id="geometryTable"> 
                    <tr><td class="name">Default ad size (w x h):</td>
                        <td class="value">
                            <input id="adWidth" name="adWidth" class="dimension"  v-model="adWidth"/>
                            x
                            <input id="adHeight" name="adHeight" class="dimension" v-model="adHeight"/>
                        </td>
                    </tr>
                    <tr><td class="name">Default ad position (left, top):</td>
                        <td class="value">
                            <input id="adLeft" name="adLeft" class="dimension" v-model="adLeft"/>
                            ,
                            <input id="adTop" name="adTop" class="dimension" v-model="adTop"/>
                        </td>
                    </tr>
                    <tr><td class="name">Max ad size (w x h):</td>
                        <td class="value">
                            <input id="adMaxWidth" name="adMaxWidth" class="dimension" v-model="adMaxWidth"/>
                            x
                            <input id="adMaxHeight" name="adMaxHeight" class="dimension" v-model="adMaxHeight"/>
                        </td>
                    </tr>
                    <tr><td class="name">Max ad position (left, top):</td>
                        <td class="value">
                            <input id="adMaxLeft" name="adMaxLeft" class="dimension" v-model="adMaxLeft"/>
                            ,
                            <input id="adMaxTop" name="adMaxTop" class="dimension" v-model="adMaxTop"/>
                        </td>
                    </tr>
                    <tr><td class="name">Screen size (w x h):</td>
                        <td class="value">
                            <input id="screenWidth" name="screenWidth" class="dimension" v-model="screenWidth" />
                            x
                            <input id="screenHeight" name="screenHeight" class="dimension" v-model="screenHeight"/>
                        </td>
                    </tr>
                </table>
                </p>
            </div>
            
            <div id="placementDiv">
                <p class="no-margin">API version to test: 
                    <select name="version">
                        <option value="1.0">MRAID v1</option>
                        <option value="2.0" selected="selected">MRAID v2</option>
                    </select>
                </p>
                <p class="no-margin">Placement: 
                    <select name="placement">
                        <option value="inline" selected="selected">Inline</option>
                        <option value="interstitial">Interstitial</option>
                    </select>
                    <br/>
                    <input id="offscreen" name="offscreen" type="checkbox"/>Off-screen
                </p>
            </div>

            <div id="capabilitiesDiv">
                <p class="no-margin">Native features to emulate:
                    <ul id="capabilitiesList">
                        <li v-for="feature in features">
                            <input :id="feature" :name="feature" type="checkbox" checked="checked" /> {{feature}}
                        </li>
                        
                    </ul>
                </p>
            </div>
            </div>
            <input type="button" value="Next" @click="nextTab" />
        </div>
        
        <div id = "valuesDiv">
            <pre>low price</pre> <input type="text" value="1200"/><br/><br/>
            <pre>high price</pre> <input type="text" value="1700"/><br/><br/>
            <pre>Leverage</pre> <input type="text" value="2"/><br/><br/>
            <pre>Orders</pre> <input type="text" value="30"/><br/><br/>
            <pre>USDT</pre> <input type="text" value="50"/><br/><br/>
            <pre>ETH</pre> <input type="text" value="0.04"/><br/><br/>
            <pre>term</pre> <input type="text" value="24"/> hours<br/><br/>
            <input type="button" value="Next" @click="nextTab" />

        </div>
        <div id="devicePreviewDiv">
            
            <!-- <div class="drag" id="resizable-screensize" :style= "{width:screenWidth+'px',  height:screenHeight+'px'}" style="top:100px;left:500px"><p>screen size</p>
            <div class="handle SE"></div>
            </div>
            <div class="drag" id="resizable-maxAdSize" :style= "{width:adMaxWidth+'px',  height:adMaxHeight+'px', top:adMaxTop + offsetTop+'px', left:adMaxLeft + offsetLeft+'px'}" ><p>max ad area &amp; placement</p>
            <div class="handle SE"></div>
            </div> -->
            <!-- <div class="drag" id="resizable-initialAdSize" :style= "{width:adWidth+'px',  height:adHeight+'px' , top:adTop+offsetTop+'px', left:adLeft + offsetLeft+'px'}"><p>initial ad area &amp; placement</p>
            <div class="handle SE"></div>
            </div> -->
            <FormResizable  id="resizable-screensize" :w="screenWidth" :h="screenHeight" :x="500" :y="100"  :parent="false" :min-width="32" :min-height="32" @resizestop="resizeScreensize" @dragstop="dragScreensize">
                <p>screen size</p>
            </FormResizable>
            <FormResizable  id="resizable-maxAdSize" :w="adMaxWidth" :h="adMaxHeight" :x="adMaxLeft + offsetLeft" :y="adMaxTop + offsetTop" :parent="false" :min-width="32" :min-height="32" @resizestop="resizeMaxAdSize" @dragstop="dragMaxAdSize">
                <p>max ad area &amp; placement</p>
            </FormResizable>
            <FormResizable  id="resizable-initialAdSize" :w="adWidth" :h="adHeight" :x="adLeft + offsetLeft" :y="adTop+offsetTop" :parent="false" :min-width="32" :min-height="32" @resizestop="resizeInitialAdSize" @dragstop="dragInitialAdSize">
                <p>initial ad area &amp; placement</p>
            </FormResizable>
        </div>
                

    </div>
</template>