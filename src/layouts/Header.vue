<template>
    <div>
        <div class="header">
            <div class="content-search">
                <input type="text" placeholder="Buscar por cidade...">
                <svg id="menu" xmlns="http://www.w3.org/2000/svg" width="60" height="60" fill="currentColor" class="bi bi-list" viewBox="0 0 16 16" color="white">
                    <path fill-rule="evenodd" d="M2.5 12a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5zm0-4a.5.5 0 0 1 .5-.5h10a.5.5 0 0 1 0 1H3a.5.5 0 0 1-.5-.5z"/>
                </svg>
            </div>
            <div class="content-logo">
                <h1>MEU TEMPO</h1>
                <svg xmlns="http://www.w3.org/2000/svg" width="60" height="60" fill="currentColor" class="bi bi-cloudy-fill" viewBox="0 0 16 16" color="white">
                    <path d="M13.405 7.027a5.001 5.001 0 0 0-9.499-1.004A3.5 3.5 0 1 0 3.5 13H13a3 3 0 0 0 .405-5.973z"/>
                </svg>
            </div>
        </div>
        <div class="sub-header">
            <div>
                <img class="icon" :src="changeIcon()"  width="35px" height="35px">
                <p>{{ localizacao }} / {{ temperaturaRecente }}</p>
            </div>
        </div>
    </div>
</template>>

<script>

export default {
    data() {
        return {
            localizacao: 'São Bernardo do Campo-SP',
            temperaturaRecente: 20,
            chanceDeChuva: 30,
            icon: require('@/assets/icons/cloud-drizzle.svg'),
            gettingLocation: '',
            errorStr: '',
            options: ''
        }
    },
    methods:  {
        changeIcon() {
            if(this.chanceDeChuva <= 30) {
                this.icon = require('@/assets/icons/cloud-sun.svg')
            }else if(this.chanceDeChuva > 30 && this.chanceDeChuva <= 50) {
                this.icon = require('@/assets/icons/cloud-drizzle.svg')
            }
            return this.icon
        }
    },
    created() {
        if("geolocation" in navigator) {
            const successCallback = (position)=> {
                console.log(position)
            }
            const errorCallback = (error) => {
                console.error(error)
            }
            navigator.geolocation.getCurrentPosition(successCallback, errorCallback)
        } else {
            alert("Não funciona!!")
        }

    }
}

</script>

<style scoped>
    .header {
        width: 100%;
        height: 122px;
        background-color: #1F8A5C;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }
    .content-search {
        display: flex;
        justify-content:center;
        align-items: center;
    }
    input {
        width: 591px;
        height: 62px;
        border-radius: 10px;
        font-size: 24px;
        
    }
    input[placeholder] {
        padding-left: 10px;
    }
    .content-logo {
        display: flex;
        justify-content: center;
        align-items: center;
        color: white;
    }
    .content-logo h1 {
        padding-right: 3px;
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
    }
    #menu{
        cursor: pointer;
    }
    .sub-header {
        height: 49px;
        background-color: #C6E0D8;
        display: flex;
        align-items: center;
        font-size: 20px;
    }
    .sub-header div {
        display: flex;
        align-items: center;
        padding-left: 13%;
    }
    .icon {
        padding-right: 6px;
    }
</style>