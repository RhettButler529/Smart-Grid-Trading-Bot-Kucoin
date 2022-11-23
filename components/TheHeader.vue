<script setup>
    const props = defineProps({
        tabid: {
            type:Number,
            default : 1
        }
    })
    

    const indicatorPosition = computed(() =>{
        if(props.tabid==1) return  "20px"
        else if(props.tabid==2) return "100px"
        else return "168px"
    })
 
    const emit = defineEmits(['click-tab'])
    function clickTab(id){
        
        emit('click-tab', id)
    }
    
</script>

<template>
    <div>
        <header>
            
        </header>
        <nav>
            <ul id='tabs'>
                <li><a  @click="clickTab(1)" style="cursor: pointer;">Prepare</a></li>
                <li><a  @click="clickTab(2)" style="cursor: pointer;">Flight</a></li>
                <li><a  @click="clickTab(3)" style="cursor: pointer;">Test</a></li>
            </ul>
            <span id='indicator' :style="{left:indicatorPosition}"></span>
        </nav>
    </div>
</template>
