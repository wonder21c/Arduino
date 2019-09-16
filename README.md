1.시나리오 및 작성 소감
아두이노와 processing, 그리고 10k저항과 조도센서를 이용하여 수업을 진행하였습니다.
조도센서가 경보기,가로등에 실생활등 여러 방면에 사용되는 만큼 흥미를 가지고 수업을 들었습니다.
직접 조도센서가 빛을 감지하고 아두이노가 송신을 하고 컴퓨터가 수신하는 상호작용을 통해 신기함에 아두이노에 대한 흥미가 더욱 생겨났습니다.
아두이노를 통해 실생활에 사용되고있는 어두워지면 가로등이켜지는 가로등을 오늘 수업을 통해 배운내용으로 만들 수 있다는걸 알게되었습니다.
매주 수업을 진행할때마다 게임보다는 아두이노를 가지고 노는게 더욱 재밌어지는거 같습니다.
아두이노를 배울 수 있어서 너무 행복합니다.교수님 아두이노 화이팅!


2.아두이노코드

void setup() {  

  Serial.begin(9600);
  
}

void loop() {

  int a = analogRead(A0);
  
  Serial.println(a); //a=a+1;
  
  delay(500);
  
}


3.프로세싱코드

import processing.serial.*;

Serial p;

void setup(){

  size(300,300);
  
  p=new Serial(this,"COM7",9600);
  
}
void draw(){

  if(p.available()>0){
  
    String m=p.readString();
    
    int a = int(m.trim());
    
    println(a);
    
    if(a>250) fill(0,255,0);
    
   else     fill(255,0,0);
    
    ellipse(150,150, 200,200);
  }
  
}


