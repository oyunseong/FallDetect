# FallDetect

## 낙상 감지 어플

사용 방법 : 
1. 문자 기능을 사용하기 위한 퍼미션을 수락합니다.
2. 낙상 감지 문자를 받을 핸드폰 번호를 입력합니다.
3. 디바이스를 떨어뜨리거나 넘어지면 Toast 메시지와 함께 문자가 전송됩니다. 

SensorEventListener
~~

    override fun onSensorChanged(event: SensorEvent) {
        if (mListener != null) {
            movementStart = System.currentTimeMillis()

            val loX = event.values[0]
            val loY = event.values[1]
            val loZ = event.values[2]

            val loAccelerationReader = sqrt(
                loX.toDouble().pow(2.0)
                        + loY.toDouble().pow(2.0)
                        + loZ.toDouble().pow(2.0)
            )

            val precision = DecimalFormat("0.00")
            val ldAccRound = java.lang.Double.parseDouble(precision.format(loAccelerationReader))
            
            if (ldAccRound > 0.3 && ldAccRound < 1.3 && (movementStart - lastMovementFall) > 1000) {

                mShakeCount++
                mListener!!.onShake(mShakeCount)

                lastMovementFall = System.currentTimeMillis()

            }
        }   
 
 디바이스의 가속도가 0.3 ~ 1.3이상일 때 `onShake()` 이벤트를 발생시킵니다.

<img src="https://user-images.githubusercontent.com/42116216/203105072-6b430fe0-0743-45cf-97c9-6658d00e065a.png" width="200" height="400">

<img src="https://user-images.githubusercontent.com/42116216/203105411-078befe8-fdb6-4718-a7a5-b28a231e5428.png" width="200" height="400">

<img src="https://user-images.githubusercontent.com/42116216/203105521-5dc45eb9-653c-4a0a-80ac-ee0ef1866eeb.png" width="200" height="400">

<img src="https://user-images.githubusercontent.com/42116216/203105592-5ce0d911-e57e-4eeb-9b18-ec0b307b09a2.png" width="200" height="400">
