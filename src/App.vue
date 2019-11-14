<template>
	<div id="app">
		  <div class="wrapper clearfix">
			  <!-- Truyen du lieu thi  phai thong qua thang props > chuyen du lieu tu cha vao con(Parent to child) -->
          
           <Players v-bind:scoresPlayer="scoresPlayer" 
		   			v-bind:currentScore="currentScore"
					v-bind:activePlayer="activePlayer"
					v-bind:isWinner="isWinner"
		    />
			<Control 
			v-bind:isPlaying="isPlaying"
				v-on:handleNewGame="handleNewGame" 
				v-on:handleRollDice="handleRollDice"
				 v-on:handleHold="handleHold"
				 v-bind:finalScore="finalScore"
				v-on:handldeChangeFinalScore=" handldeChangeFinalScore"
			 />
			<Dices  v-bind:dices="dices"/>
            <popup-rule v-bind:isOpenPopup="isOpenpopup"  v-on:handleConfirm="handleConfirm"/>
        </div>

	</div>
</template>

<script>
import Players from './components/Players';
import Control from './components/Controls';
import Dices from './components/Dices';
import PopupRule from './components/PopupRule';
export default {
	name: 'app',
	data () {
		return {
			isPlaying:false,
			isOpenpopup:false,
			activePlayer:1, // xem ai la nguoi choi
			scoresPlayer:[0,50],
			currentScore:100,
			dices:[2,4],
			finalScore:100
			
		}
		
	},
	components:{
		Players,
		Control,
		Dices,
		PopupRule,
	},
	methods:{
		handldeChangeFinalScore(e){
			console.log(e.target.value);
			var number =parseInt(e.target.value);
			if(isNaN(number))
			{
					this.finalScore='';
			}
			else
			{
				this.finalScore=number;
			}

		},
		nextPlayer(){
			this.activePlayer=this.activePlayer=== 0 ? 1 : 0 ,
			this.currentScore=0;
		},
		handleNewGame(){
			console.log(" đây là từ  app.vue nhé");
			// chỗ này sau đó phải hiện ra luật chơi
			this.isOpenpopup = true;
			
		},
		handleConfirm(){
			//chỗ này là handleConfirm ở lớp app nhé
			this.isOpenpopup=false;
			this.isPlaying=true;
			this.activePlayer=0;
			this.scoresPlayer=[0,0];
			this.currentScore=0;
			this.dices=[4,6];

		},
		handleRollDice(){
			
			if(this.isPlaying)
			{console.log("đây là ở trang app.vue");
				var dice1=Math.floor(Math.random()*6)+1;
				var dice2=Math.floor(Math.random()*6)+1;
				this.dices=[dice1,dice2];
				if(dice1===1 || dice2==1)
				{
					let activePlayer =this.activePlayer;
					
					setTimeout(function(){
						alert('Người chơi Player '+(activePlayer+1)+' đã quay trúng số 1 .Rất tiếc');
					},10)
					
						this.nextPlayer();
					
					

				}
				else{
					this.currentScore=this.currentScore + dice1 + dice2;
				}
			}
			else{
				alert("Bạn phải  ấn nút bắt đầu chơi , thì mới quay được xúc xắc");
			}
		},
		handleHold(){
			if(this.isPlaying)
			{
					console.log(" đã vào đến handleHold ở lớp App nhé");
					let {scoresPlayer,activePlayer,currentScore}=this;
					let scoreOld =scoresPlayer[activePlayer];
					this.$set(this.scoresPlayer,activePlayer,scoreOld+currentScore);
					if(!this.isWinner)
					{
this.nextPlayer();
					}
							
					
				
			}
			else{
				alert("Bạn phải ấn vào nút new game để bắt đầu chơi game");
			}
			
		}

	},
	computed:{
		isWinner(){
			let{scoresPlayer ,finalScore} =this;
			if(scoresPlayer[0]>=finalScore ||scoresPlayer[1]>=finalScore)
			{
				// dung cuoc choi
				this.isPlaying=false
				return true;
			}
			else{
				return false;
			}
		}
	}

	
}
</script>

<style>
	/**********************************************
*** GENERAL
**********************************************/

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    
}

.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

body {
    background-image: linear-gradient(rgba(62, 20, 20, 0.4), rgba(62, 20, 20, 0.4)), url('/public/assets/back.jpg');
    background-size: cover;
    background-position: center;
    font-family: Lato;
    font-weight: 300;
    position: relative;
    height: 100vh;
    color: #555;
}

.wrapper {
    width: 1000px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
    overflow: hidden;
}



</style>
