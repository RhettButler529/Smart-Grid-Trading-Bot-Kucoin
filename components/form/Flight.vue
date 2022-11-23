<script setup>
    
    const adFragment = ref('')
    const emit = defineEmits(['next-tab'])
        
    function renderAd(){
        emit('next-tab', 3)
        renderHtmlAd()
        
    }
</script>
<template>
    <div>                
        <div>
            <h2 >tag source</h2>
            <div>
                <!--textarea name="adFragment" id="adFragment" rows="10" ><script src='http://rtr.innovid.com/r1.5637e6df321548.45146407;cb=[timestamp]'></script></textarea><br/-->
                <textarea v-model="adFragment" name="adFragment" id="adFragment" rows="10" placeHolder="Your HTML fragment here" ></textarea><br/>
                <!-- <NuxtLink to="/safari/device-page" target="_blank"> -->
                    <input type="button" value="Render" @click="renderAd" />
                <!-- </NuxtLink> -->
                
            </div>
        </div>


    </div>
</template>