# Juego-processing
Codigo para un juego de naves y rocas cayendo con clases 

//se definen objetos arriba siempre!!
Piedras piedra, piedra2;
Alien alien;
PImage img2;  //paracarga de Game Over imagen
int vida = 1;  //
PImage img;
void setup() {
  size(800, 600);
  img2 = loadImage("cielo.jpg");
  alien = new Alien();
  piedra = new Piedras();
  piedra2 = new Piedras();
}

void draw() {
  imageMode(CENTER);
  image(img2, 255, 400);
  alien.dibujar();
  GameOver();
  piedra.display();
  piedra2.display();
  piedra.mover();
  piedra2.mover();
  detectar();
  detectar2();
  if (piedra.muerta()) {
    
    //vuelve a generarse
    piedra = new Piedras();
  }
  if (piedra2.muerta()) {
    piedra2 = new Piedras();
  }
}

void detectar() {
  if (alien.getPosX() < piedra.getPosX() +100
    && alien.getPosX() > piedra.getPosX() -100
    && alien.getPosY() < piedra.getPosY() +50
    && alien.getPosY() > piedra.getPosY() -50) {
      
      //si chocan pasa esto
    background(255, 0, 0);
    vida = vida-1;
  }
}

void detectar2() {
  if (alien.getPosX() < piedra2.getPosX() +100
    && alien.getPosX() > piedra2.getPosX() -100
    && alien.getPosY() < piedra2.getPosY() +50
    && alien.getPosY() > piedra2.getPosY() -50) {
    background(255, 0, 0);
    vida = vida -1;
    
  }
}

void GameOver() {
  if (vida == 0 ) {
    piedra.detener();
    piedra2.detener();
    img = loadImage("gameover.png");
    image(img, width/2, height/2, width, height);
  }
}


void keyPressed() {

  switch(keyCode) {
  case UP:
    alien.moverarriba();
    break;
  case DOWN:
    alien.moverabajo();
    break;
  case LEFT:
    alien.moverizquierda();
    break; 
  case RIGHT:
    alien.moverderecha();
    break;
  }
}



CLASE ALIEN

class Alien {
  PImage imagen;
  float posX;
  float posY;

//constructor
  Alien () {
    posX = width/2;
    posY = height -100;
    imagen = loadImage("alien.png");
  }

 //devuelve la posicion de X con el return posX; 

  float getPosX() {
    return posX;
  }
  
  float getPosY() {
    return posY;
  }
  
  void moverderecha() {
   posX = posX +10;
  }
  
  void moverizquierda() {
    posX = posX -10;
  }

  void moverarriba() {
    posY = posY -10;
  }
  void moverabajo() {
    posY = posY +10;
  }


  void dibujar() {
    imageMode(CENTER);
    imagen = loadImage("alien.png");
    image (imagen, posX, posY, 100, 140);
  }
  
}

CLASE PIEDRAS

class Piedras {
  PImage imagen;
  float posX;
  float posY;
  float desp; //velocidad dela piedra;
  float tamano;
  
//constructor
  Piedras () {
    posX = random(0, width);
    posY = 0;
    desp = random (5, 10);
    tamano = random (50, 150);
  }
   float getPosX() {
    return posX;
  }
  float getPosY() {
    return posY;
  }
  void mover() {
    posY = posY +desp;
  }

  void detener () {
    posX = height +500;
    posY = width +500;
  }
  
  void display() {
    imageMode(CENTER);
    imagen = loadImage("roca.png");
    image (imagen, posX, posY, tamano, tamano);
  }
  
  boolean muerta() {
    
    if (posY > height) {
      return true;
    }else 
    return false;
  }
}
