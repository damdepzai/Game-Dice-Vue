<template>
    <div class="wapper-controls">
        
            <button class="control btn-new" v-on:click="newGame"><i class="ion-ios-plus-outline"></i>New game</button>
            <button class="control btn-roll" v-on:click="rollDice"><i class="ion-ios-loop"></i>Roll dice</button>
            <button class="control btn-hold" v-on:click="hold"><i class="ion-ios-download-outline"></i>Hold</button>
            
            <input 
            
            v-bind:disabled="isPlaying"
                v-bind:value="finalScore"
                v-on:input="$emit('handldeChangeFinalScore',$event)"
             type="number" placeholder="Final score" class="final-score">
    </div>
</template>
<script>
export default {
    name: 'controls',
    props:{
        finalScore:{
            type:[Number , String ] , default : 100
        },
        isPlaying:{type:Boolean ,default :false}

    },
    data(){
        return{

        }
    },
    methods:{
        newGame(){
            console.log(" Đây là từ Control  nhé ");
            // kích hoạt sự kiện kích  khi ta kích vào nút new game
            this.$emit("handleNewGame");
        },
        rollDice(){
            console.log("Đấy là rollDice từ control");
            //emit là chuyền 1 tín hiệu cho lớp cha biết là có 1 handle  ở bên lớp con
            this.$emit("handleRollDice");

        },
        hold(){
            console.log("đây là hold ở trong  controll");
            this.$emit("handleHold");
        }
    }
    
}
</script>
<style>
/**********************************************
*** Control
**********************************************/
.control {
    position: absolute;
    width: 200px;
    left: 50%;
    transform: translateX(-50%);
    color: #555;
    background: none;
    border: none;
    font-family: Lato;
    font-size: 20px;
    text-transform: uppercase;
    cursor: pointer;
    font-weight: 300;
    transition: background-color 0.3s, color 0.3s;
}
.control.disable {
    pointer-events: none;
}

.control:hover { font-weight: 600; }
.control:hover i { margin-right: 20px; }

.control:focus {
    outline: none;
}

.control i {
    color: #42b983;
    display: inline-block;
    margin-right: 15px;
    font-size: 32px;
    line-height: 1;
    vertical-align: text-top;
    margin-top: -4px;
    transition: margin 0.3s;
}

.btn-new { top: 45px;}
.btn-roll { top: 403px;}
.btn-hold { top: 467px;}

.final-score {
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: 520px;
    color: #555;
    font-size: 18px;
    font-family: 'Lato';
    text-align: center;
    padding: 10px;
    width: 160px;
    text-transform: uppercase;
}

.final-score:focus { outline: none; }
</style>