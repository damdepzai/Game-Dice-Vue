<template>
  <div class="wapper-popup " v-bind:class="getClassPopup">
    <div class="rule">
      <h3>Luật chơi</h3>
      <p>Khi bạn ấn nút chơi game thì hệ thống sẽ bắt đầu chơi được và nếu bạn chọn điểm chiến thắng thì hệ thống sẽ mặc định là 100 điểm</p>
      <p>Mỗi khi bạn quay được xúc xắc số 1 thì sẽ bị mất lượt và chuyển lượt cho người bên kia </p>
      <p>Hãy ấn vào nút đã hiểu để bắt đầu trò chơi ngay nào</p>
      <p>Chúc bạn chơi game vui vẻ !!!!</p>
      <button v-on:click="confirm" class="confirm">Đã hiểu</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "PopupRule",
  props:{
      isOpenPopup: {
          type:Boolean,
          default:false,
      }
  },
  data() {
    return {};
  },
  methods: {
      confirm(){
          //truyền dữ liệu qua thằng cha của nó là app
          console.log(" confirm đây là đang ở trong popup");
          this.$emit("handleConfirm");
      }

  },
  computed: {
      getClassPopup :function(){
          return{
              'open-popup':this.isOpenPopup
          }
      }
  }
};
</script>
<style>
.wapper-popup {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.4);
  opacity: 0;
  visibility: hidden;
}
.rule{
    width: 350px;
    padding:20px;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%) scale(1.5);
    background-color:white;
    position: absolute;
    font-family: Arial, Helvetica, sans-serif;
     
   
}
.open-popup{
    opacity: 1;
    visibility: visible
}
.open-popup .rule{
    transform: translate(-50%,-50%) scale(1);
}
.rule H3{
    margin-bottom: 10px;
}
.rule .confirm{
    border:2px solid #333;
    margin-top: 20px;
    background: white;
    cursor: pointer;
    padding:8px 15px;
    transition: all 0.6 ease;
}
.rule .confirm:hover {
    background-color: #333;
    color:white;
}

</style>