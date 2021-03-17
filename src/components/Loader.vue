<template>
<svg version="1.1" id="L5" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
  viewBox="0 0 100 100" enable-background="new 0 0 0 0" xml:space="preserve">
  <circle fill="#e74c3c" stroke="none" cx="6" cy="50" r="6">
    <animateTransform 
       attributeName="transform" 
       dur="1s" 
       type="translate" 
       values="0 15 ; 0 -15; 0 15" 
       repeatCount="indefinite" 
       begin="0.1"/>
  </circle>
  <circle fill="#e74c3c" stroke="none" cx="30" cy="50" r="6">
    <animateTransform 
       attributeName="transform" 
       dur="1s" 
       type="translate" 
       values="0 10 ; 0 -10; 0 10" 
       repeatCount="indefinite" 
       begin="0.2"/>
  </circle>
  <circle fill="#e74c3c" stroke="none" cx="54" cy="50" r="6">
    <animateTransform 
       attributeName="transform" 
       dur="1s" 
       type="translate" 
       values="0 5 ; 0 -5; 0 5" 
       repeatCount="indefinite" 
       begin="0.3"/>
  </circle>
</svg>
</template>

<script>
export default {
  name: "Loader",
  
}
</script>

<style lang="scss" scoped>
@import url(https://fonts.googleapis.com/css?family=Comfortaa:400,700,300);

*,html{margin:0;padding:0}

//variables
$baseColor : #e74c3c;
$fontColor : #fff;



body{
  background: $baseColor;
  text-align: center;
  font-family: 'Comfortaa', cursive;
}
svg{
  width: 100px;
  height: 100px;
  margin: 20px;
  display:inline-block;
}
h1{
  text-align: center;
  color: $fontColor;
  margin: 0 0 100px;
  font-size: 34px;
  font-weight: 100;
  text-transform: uppercase;
  background-color: darken($baseColor, 5);
  padding: 20px 0;
  b{
    font-weight: 700;
  }
}

//follow me template
.made-with-love{
  margin-top: 20px;
  padding: 10px;
  font-size: 10px;
  font-family: arial;
  color: #fff;
  i{
    font-style: normal;
    color: #F50057;
    font-size: 14px;
    position: relative;
    top: 2px;
  }
  a{
    color: #fff;
    text-decoration: none;
    &:hover{
      text-decoration: underline;
    }
  }
}
</style>