# Challenge_06
## 뽀모도로 타이머

'뽀모도로'는 이탈리아어로 토마토를 뜻한다. 프란체스코 시릴로가 대학생 시절 토마토 모양으로 생긴 요리용 타이머를 이용해 25분간 집중 후 휴식하는 일처리 방법을 제안한데서 그 이름이 유래했다.

뽀모도로 타이머는 SeekBar를 좌우로 이동하여 시간을 설정한 뒤 손을 떼는 즉시 타이머가 실행된다.

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
  * <https://developer.android.com/reference/android/media/SoundPool>
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
     override fun onPause() {
        super.onPause()
        soundPool.autoPause()
     }
     ```
     * Pause()는 soundPool.play에서 리턴한 값(Stream)만을 중지하고, autoPause은 현재 활성화된 모든 Stream을 전체 중지한다. 이 앱에서는 따로 구분할 필요가 없기 때문에 autoPause()를 사용했다.
     ``` kotlin
     override fun onResume() {
        super.onResume()
        soundPool.autoResume()
     }
     ```
     * Stream 재개
    
    **종료**
     ``` kotlin
     override fun onDestroy() {
        super.onDestroy()
        soundPool.release()
     }
     ```
     
* WindowBackground
  * themes
    ``` kotlin
    <item name="android:windowBackground">@color/pomodoro_red</item>
    ```
     * xml단에서도 background를 설정할 수 있지만 이 경우 해당 액티비티의 LifeCycle에 맞춰 onCreate 상태에서부터 background가 적용되기 때문에 onCreate이전에는 적용되지 않는다.
     * themes에서 windowBackground으로 초기 설정을 할 수 있다.
* Vector Image
  * Vector Drawable은 처음 로드할 때 같은 래스터 이미지보다 CPU 사이클이 더 많이 소모될 수 있다.
  * 벡터 이미지는 최대 200 x 200dp 로 제한하는 것이 좋다. 이 이상인 경우 로드하는데 너무 오랜 시간이 걸릴 수 있다.
# 실행화면
<img src="https://user-images.githubusercontent.com/74666576/151254776-312b8149-eaa4-4b48-8bd7-1ea80af09441.jpg" width="270" height="500">
<img src="https://user-images.githubusercontent.com/74666576/151254789-340d15cb-16d9-4e85-9816-c4e044ee42ac.gif" width="270" height="500">
