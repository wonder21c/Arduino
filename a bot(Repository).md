**1.시나리오 **
저희조는 영화 월E에 나오는 화성탐사로봇을 만들어보기위해서 실제로 저희가 만든 로봇이 화성에 간다고 가정하여 
소리센서와 led를 사용하여 저희만의 화성탐사 로봇을 제작해 보았습니다.

**2. 소스코드**
```c
#include <Servo.h>
#define PIEZO 6 // 피에조 부저



#define c4 3822 // 261.63Hz 도
#define d4 3405 // 293.67Hz 레
#define e4 3034 // 329.63Hz 미
#define f4 2863 // 349.23Hz 파
#define g4 2551 // 392.11Hz 솔
#define g4s 2408 // 415.30Hz 솔#
#define a4 2273 // 440.11Hz 라
#define b4 2025 // 493.88Hz 시
#define c5 1910 // 523.25Hz 도
#define d5 1703 // 587.33Hz 레


#define d5s 1607 // 584.37Hz 레#
#define e5 1517 // 659.26Hz 미
#define f5 1432 // 698.46Hz 파
#define g5 1276 // 783.99Hz 솔
#define a5 1136 // 880.11Hz 라
#define b5 1012 // 987.77Hz 시




int song[] = { e5, d5s, e5, d5s, e5, b4, d5, c5, a4, c4, e4, a4, b4, e4, g4s, b4, c5, e4, e5, d5s, e5, d5s, e5, b4, d5, c5, a4, c4, e4, a4, b4, e4, c5, b4, a4 };




int song_pivot = 0;
unsigned long mil = 0;




Servo sl, sr;
void setup(){
   pinMode(PIEZO, OUTPUT);


  pinMode(2, OUTPUT);
  pinMode(7, OUTPUT);
  sl.attach(13); sr.attach(12);
}
  long timeset1=0; 
  long timeset2=0;
  long Drl = 0;
  long DrR = 0;
  int led1=0;
  int led2=0;
  long turn1 = 0;
  void sing(int eum, int isLong) {
  long lele = 125000;





  if(isLong == 3) lele = 375000;
  else if(isLong == 6) lele = 750000;





  for(long i=0; i< lele ; i+= eum) {
    digitalWrite(PIEZO, HIGH);
    delayMicroseconds(eum/2);
    digitalWrite(PIEZO, LOW);
    delayMicroseconds(eum/2);
  }
}
void loop(){
   if (millis() - mil > 100) {
    int isLong;


    if(song_pivot == 8 || song_pivot == 12 || song_pivot == 16 || song_pivot == 26 || song_pivot == 30) {
      isLong = 3;
    } else if(song_pivot == 34) {
      isLong = 6;
    }


    sing(song[song_pivot++], isLong);
    if(song_pivot == 35)  song_pivot = 0;
    mil = millis();
  }




    if(timeset1 <= millis()) { //만약 다음 토글시간이 되었다면? 무조건 실행
    digitalWrite(2, led1);
    //sl.write(1300); sr.write(1700);
    timeset1=millis()+1000; //LED1의 다음 토글시간을 정함
    led1=!led1; //상태를 반전시킴 //LED
  }
  
  if(Drl <= millis()) { //만약 다음 토글시간이 되었다면? 무조건 실행
    sl.write(1300); sr.write(1700);
    Drl=millis()+1000; //LED1의 다음 토글시간을 정함
  } //움직이는 부분만 묶은 IF문 //전진
  
      if(timeset1 <= millis()) { //만약 다음 토글시간이 되었다면? 무조건 실행
    sl.write(1700); sr.write(1700);
    Drl=millis()+1000; //LED1의 다음 토글시간을 정함
    led1=!led1; //상태를 반전시킴
  } //회전
  
  if(timeset2 <= millis()) {
    digitalWrite(7, led2);
    //sl.write(1700); sr.write(1300);
    timeset2=millis()+1250;
    led2 = !led2;
  }//LED

     if(turn1 <= millis()) {
      for(;turn1<=2000;turn1=millis()){
        sl.write(1300); sr.write(1300);
      }
    turn1=millis()+1250;
  }//한바퀴

    if(DrR <= millis()) {
    digitalWrite(7, led2);
    //sl.write(1700); sr.write(1300);
    DrR=millis()+1250;
  }//후진
  
   if(DrR <= millis()) {
    sl.write(1300); sr.write(1300);
    DrR=millis()+1250;
  }//회전
} 
```

 **3. 동영상 **
 https://youtu.be/eM5sWFuwULE
 **4.소감**
 ```
 이번 아두이노 과제를 하면서 많은 것을 느꼈습니다.
 처음에는 아두이노에 LED와 조도센서 스피커를 하나하나씩하는것은 쉬웠는데 그것을 조합하여 abot에 적용하는 것이 힘들었습니다. 
 처음 난관은 delay였는데 저희 목적은 LED가 깜박이면서 춤을 추게하는 것이 첫번째 목표였습니다.
 그런데 delay 함수를 쓰면 delay 시간동안 다른 코드가 멈춘다는 것을 알았고 millis함수를 써서 문제를 해결해 나갈 수 있었습니다. 
 이렇게 하나하나씩 팀원들과 문제를 해결해나가면서 결국 abot을 저희가 원하는데로 작동시킬 수 있었고 팀원모두가 열심히 하였기에 
 성취감과 기쁨이 5배가 된거 같았습니다. 아두이노를 하면서 느낀점은 혼자가 아니라 팀원들과 같이하면 더 원활하게 
 문제를 해결해 나갈 수 있다는 점을 알게 되었습니다. 아두이노를 더 사랑해서 아두이노의 박사가 되고싶습니다. 
 감사합니다.
 ```
