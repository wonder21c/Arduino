> ### 유튜브 링크
**[ir송수신기로 자율주행하기]https://www.youtube.com/watch?v=FBwOPQZjj9c&feature=youtu.be**


> ## 1. 팀원
**1.김준영**

**2.박형민**

**3.손정우(팀장)**

**4.이진욱**

**5.천준영**



> ## 2.ir송수신이란?
```
IR이란 적외선(Infrared Rays; IR)을 말하고 파장이 약 780nm~1mm의 범주에 들어있는 전자기파를 지칭하며

IR송수신기란 주변에서 흔히 볼 수 있는 가전제품의 원격 제어에 사용되는 리모컨이 적외선을 사용하는 통신의 

대표격이라 할 수 있습니다. IR송수신기를 이용하는 대표적인 예로 TV,DVD플레이어,셋톱박스를 들수있습니다.

그리고 왜 블루투스 리모콘 보다 IR리모콘을 더 많이 사용하는 이유는 가격대비 성능이 더 좋고 직진성과 회절성이 

뛰어나며 블루투스 같이 페어링의 절차가 없어 더 편리하기 때문인거 같습니다.
```

> ## 3-1.작동원리

```
적외선 다이오드에서 적외선을 방출하면적외선 수신기가 감지하고 전기적 신호로 전환하는 원리
```

> ## 3-2.Hz에 따른 인식 범위
<div>
  <img width=500 src="https://user-images.githubusercontent.com/50861700/69004723-5e7ac700-095b-11ea-9485-f5bbfffd9143.png">
  </div>

> ## 4.소드코드
```c
#include <Servo.h> // Include servo library
Servo sl, sr; // Declare left and right servos
void setup()
{   
  sl.attach(13);
  sr.attach(12);
  pinMode(10, INPUT); 
  pinMode(9, OUTPUT);
  pinMode(3, INPUT); 
  pinMode(2, OUTPUT);
  Serial.begin(9600);
}
int irDetect(int irLedPin, int irReceiverPin, long frequency)
{
  tone(irLedPin, frequency, 8);
  delay(1);
  int ir = digitalRead(irReceiverPin);
  delay(1);
  return ir;
}
void loop()
{
  int wl = irDetect(9, 10, 42000);
  Serial.print(wl);
  int wr = irDetect(2, 3, 42000);
  Serial.print("  ");
  Serial.println(wr);
  delay(100);

  if ((wl == 0) && (wr == 0)){

    backward(500); // Back up 1 second

    turnLeft(800); // Turn left about 120 degrees

  }

  else if (wl == 0){

    backward(500); // Back up 1 second

    turnRight(400); // Turn right about 60 degrees

  }

  else if (wr == 0){

    backward(500); // Back up 1 second

    turnLeft(400); // Turn left about 60 degrees

  }

  else{

    forward(20); // Forward 1/50 of a second

  }

}

void forward(int time){

  sl.write(1700);

  sr.write(1300);

  delay(time);

}

void turnLeft(int time){

  sl.write(1300);

  sr.write(1300);

  delay(time);

}

void turnRight(int time){

  sl.write(1700);

  sr.write(1700);

  delay(time);

}

void backward(int time) {

  sl.write(1300);

  sr.write(1700);

  delay(time);

}
```

> ## 5. ir송수신기 회로
<div>
  <img width=500 src="https://user-images.githubusercontent.com/50861700/69004550-77ce4400-0958-11ea-8288-340b27db64e8.jpg" >
  <img width=500 src="https://user-images.githubusercontent.com/50861700/69004710-41de8f00-095b-11ea-868b-adee705b66e6.png">
  </div>
  
> ## 6. 소감
```
아두이노 자동차를 ir 센서를 활용하여 자율 주행 자동차로 만들어보면서,아두이노를 이용하면 자율 주행 자동차와 

같은 발전된 기술이 들어간 물건을 제작할 수 있겠다는 생각을 할 수 있었고 아두이노에 대한 무궁무진한 가능성을 

느낄 수 있었습니다. 이러한 기술 이외에도 다양한 기술들을 익혀 저만의 것으로 만들어 다양한 작품들을 제작해보고

싶습니다. 조원끼리 함께 이런 작품을 만들어 보면서 다양한 아이디어에 대해 생각해볼 수 있었던 것 같습니다.

이런 기회를 주셔서 감사합니다. 심재창 교수님 창의공학 파이팅!
```
