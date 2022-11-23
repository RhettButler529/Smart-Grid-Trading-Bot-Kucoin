<template>
    
    <div>
        <link rel="stylesheet" href="/css/reset.css" />
        <link rel="stylesheet" href="/css/main.css">
        <link rel="stylesheet" href="/css/devicesize-widget.css" type="text/css" />
        <link rel="stylesheet" href="/css/orientation-widget.css" type="text/css" />
        <!-- <link rel="stylesheet" href="/jquery/ui-lightness-jquery-ui.css" type="text/css" /> -->
        <div class = "the-header">
            <TheHeader :tabid="tabnum" @click-tab="switchTab"/>
        </div>
        <form id="setup" name="setup" onsubmit="renderAd(); return false">
            <div id="content">
                <!-- <div v-if="tabnum == 1" class = "form-prepare"> -->
                <section :style="{display:istab1}">
                    <FormPrepare @next-tab="switchTab" />
                </section>    
                <!-- </div> -->
                <!-- <div v-show="tabnum == 2" class = "form-flight"> -->
                <section :style="{display:istab2}">    
                    <FormFlight @next-tab="switchTab" />
                </section>    
                <!-- </div> -->
                <!-- <div v-if="tabnum == 3" class = "form-test"> -->
                <section :style="{display:istab3}">    
                    <FormTest/>
                </section>    
                <!-- </div> -->
            </div>
        </form>

        <div class = "the-footer">
            
        </div>
    </div>
</template>

<script setup>


    const adtag = ref(null)
    const tabnum = ref(1)

    const istab1 = computed(() => {
        if(tabnum.value==1)return "block"
        else return "none"
    })

    const istab2 = computed(() => {
        if(tabnum.value==2)return "block"
        else return "none"
    })
    const istab3 = computed(() => {
        if(tabnum.value==3)return "block"
        else return "none"
    })

    const title = ref('Smart Grid Trading Bot')
    const description = ref('My amazing Nuxt app')

    useHead({
        title,
        meta: [
            {
                name: 'description',
                content: description
            }
        ],
        
        script: [
            {
                src: '/public/safari/test',
                body: true
            },
            {
                src: '/public/safari/main',
                body: true
            },
            {
                src: '/public/safari/mraidview',
                body: true
            }
            
        ]
    })

    
    function switchTab(id){
        tabnum.value = id
    }
    onMounted(() => {
        
     //   testView()
        load()
    })
    
</script>