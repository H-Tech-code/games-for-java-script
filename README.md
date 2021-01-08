# games-for-java-script
var ball = createSprite(200,200,10,10);
var playerPaddle = createSprite(190,370,70,5);
var computerPaddle = createSprite(190,40,90,5);
var computer = createSprite(190,390,130,15);
var player = createSprite(190,12,130,15);
//variable to store different state of game
var gameState = "serve";
var computerScore = 0;
var playerScore = 0;

//computerPaddle.velocityY=0;
//computerPaddle.velocityX=10;
function draw() {
  background("green");
  ball.shapeColor="white";
  textSize(40);
  text(computerScore, 0, 200);
  text(playerScore,0,250);
  if (gameState === "serve") {
    text("Press Space to PLAY",5,180);
    playerPaddle.setAnimation("flail_gold_1");
    computerPaddle.setAnimation("flail_iron_1");
    //ball.setAnimation("tyrannosaurus_1");
  }
  for (var i = 20; i < 400; i=i+10){
    var sprite4 = createSprite(i, 206, 5, 2);
    //sprite4.setAnimation("watermelon");
  }
   if(keyDown("Space")){
    computerPaddle.velocityY = 0;
  }
  if(keyDown("Space")){
    computerPaddle.velocityX = 9;
  }
   if(keyDown("RIGHT_ARROW")){
    playerPaddle.x = playerPaddle.x+7;
  }
   if(keyDown("LEFT_ARROW")){
    playerPaddle.x= playerPaddle.x-7;
  }
 if (keyDown("space") && gameState === "serve") {
    serve();
    gameState = "play";
  }
  if(keyDown("r")){
    gameState = "serve";
  }
  if(playerScore==5||computerScore==5){
    gameState="over";
    text("game is finished",170,160);
    text("press r to play again", 150, 180);
  }
  //if(ball.y > 400 || ball.y <0) {
    //if(ball.y> 400){
      //computerScore = computerScore+1;
    //}
    //if(ball.y<0){
      //playerScore = playerScore+1;
    //}
  //if(ball.isTouching(computer||player)){
    if(ball.isTouching(computer)){
      playSound("sound://category_bell/vibrant_game_bell_ding.mp3");

      computerScore = computerScore+1;
    

  reset();
    gameState="serve";
  }
    if(ball.isTouching(player)){
      playSound("sound://category_bell/vibrant_game_bell_ding.mp3");

     playerScore =playerScore+1;
    

  reset();
    gameState="serve";
  }
if(ball.bounceOff(playerPaddle)){
  playSound("sound://category_hits/retro_game_weapon_-_light_punch_2.mp3");
  ball.velocityX = 3;
}
if(ball.bounceOff(computerPaddle)){
    playSound("sound://category_hits/retro_game_weapon_-_light_punch_2.mp3");

  ball.velocityX =-3;
}
computer.shapeColor = "yellow";
player.shapeColor = "yellow";  
//ball.shapeColor = "TRIANGLES";
createEdgeSprites();
computerPaddle.bounceOff(edges);
ball.bounceOff(edges);
//.bounceOff(playerPaddle);
drawSprites();
}
function serve() {
  ball.velocityX = 0;
  ball.velocityY = 4;
}
function reset(){
  ball.x=200;
  ball.y=200;
  ball.velocityX = 0;
  ball.velocityY = 0;
  //gameState = "serve";

}
