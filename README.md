# Challenge_06
## 뽀모도로 타이머

'뽀모도로'는 이탈리아어로 토마토를 뜻한다. 프란체스코 시릴로가 대학생 시절 토마토 모양으로 생긴 요리용 타이머를 이용해 25분간 집중 후 휴식하는 일처리 방법을 제안한데서 그 이름이 유래했다.

SeekBar를 좌우로 이동하여 시간을 설정한 뒤 손을 떼는 즉시 타이머가 실행된다.

타이머가 0초에 도달하면 벨소리를 울리고 타이머를 종료한다.


## 기능

* SoundPool로 음원 파일 재생
* 타이머
* Custom Seekbar
* 초기 SeekBar는 0으로 설정 되어 있고 사용자가 SeekBar를 우측으로 이동하면 할 수록 시간이 증가한다.(최대 60분)
* 사용자가 손을 떼면 그 즉시 설정된 시간으로 부터 타이머가 실행되고, raw폴더의 시계 효과음을 재생한다. 동시에 1초마다 화면을 갱신한다.
* SeekBar의 Progress가 0에 도달하면 벨소리 음원을 재생한다. 

## 학습 내용

* ConstraintLayout
* CountDownTimer
* SoundPool
  * **선언**
     ``` kotlin
    private val soundPool = SoundPool.Builder().build()
     ```
    **로드**
     ``` kotlin
     tickingSoundId = soundPool.load(this, R.raw.timer_ticking, 1)
     ```
     * 마지막 '1'은 value인데, 현재는 아무 의미 없지만 구글에서는 추후 호환성을 위해 value값을 지정하는것을 권장하고 있다.
     
    **재생**
     ``` kotlin
     soundPool.play(soundId, 1F, 1F, 0, 0, 1F)
     ```
     * soundPool.play("id", "기기의 좌측 스피커 볼륨", "우측 스피커 볼륨", "재생 우선순위", "반복여부"(-1일경우 무한반복), "재생속도")
     
    **제어**
     ``` kotlin
     soundPool.autoPause()
     ```
     * Pause()는 soundPool.play에서 리턴한 값(Stream)만을 중지하고, autoPause은 현재 활성화된 모든 Stream을 전체 중지한다. 이 앱에서는 따로 구분할 필요가 없기 때문에 autoPause()를 사용했다.
     ``` kotlin
     soundPool.autoResume()
     ```
     * Stream 재개
    

# 실행화면

