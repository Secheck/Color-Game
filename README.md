# Color-Game

color red = #CE1836;
color orange = #F85931;
color yellow = #EDB92E;
color green = #A3A948;
color blue = #009989;

color[] colors = {red, orange, yellow, green, blue}; //declaring 
String[] colorWords = {"red", "orange", "yellow", "green", "blue"}; //loading values

int rng1 = int(random(0, 5));
int rng2 = int(random(0, 5));

int points = 0; 

int mode = 0;

int timer = 1; 

void setup () {
  size(700, 700); 
  background(255);
  mode = 0;
}

void draw() {
  if ( mode == 0 ) { 
    intro();
  } else if ( mode == 1 ) { 
    game();
  } else if ( mode == 2 ) {
    gameover();
  } else {
    println("Mode error!");
  }
}


void mouseReleased() {
  if ( mode == 0 ) { 
    introClicks();
  } else if ( mode == 1 ) {  
    gameClicks();
  } else {
    println("Mode error!");
  }
}

// Intro tab

void intro() {
  fill(0);
  stroke(0);
  strokeWeight(2);
  rect(350, 0, 350, 700);
  textSize(32); 
  fill(#62FBFF); 
  textSize(50); 
  text("Start", 289, 330);
}

void introClicks() {
  mode = 1;
}

// Game tab

boolean ans = false; 

void game() {
  timer = timer + 1;

  background(255);
  fill(0);
  rect(350, 0, 350, 700);
  fill(colors[rng1]);
  text(colorWords[rng2], 289, 330);
  fill(#62FBFF);
  text("True", 50, 630);
  text("False", 550, 630);
  text(points, 20, 50);
  text(timer, 50, 50);
  if (timer > 60) {
    gameover();
  }
}


// checkAnswer returns true if game not over, else returns false
boolean checkAnswer() {
  if (rng1 == rng2) {
    ans = true;
  } else {
    ans = false;
  }

  if (ans == true) {
    if (mouseButton == LEFT) {
      points++;
      timer = 0; 
      return true;
    }
  } else {
    if (mouseButton != LEFT) {
      points++;
      timer = 0; 

      return true;
    }
  }
  return false;
}

void gameClicks() {
  if (checkAnswer() == true) {     
    rng1 = int(random(0, 5));
    rng2 = int(random(0, 5));  
    game();
  } else {
    gameover();
  }
} 

// Game over tab

void gameover() {
  mode = 2;
  background(0);
  fill(#62FBFF);
  text("Game Over", 290, 350); 
}
