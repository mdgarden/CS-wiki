주요 참고 기사
https://blog.theodo.com/2023/07/ble-integration-for-rn-apps/ (심장박동수 체크 앱)

사용법
https://9105lgm.tistory.com/252

11.07.
Error: Device is not authorized to use BluetoothLE
권한이 없는 줄 알았음 -> 위치 권한 추가 -> 위치 권한 부여됐는데 blemanager가 실행이 안됨 -> 안드로이드 빌드하면서 blemanager가 안들어간게 아닌가(지금 여기)

권한 문제를 해결할 수가 없고 관련 자료도 찾기 어려워 그냥 RN으로 갈아타기로 결정함
내일 하루 해보고 하루만에 블루투스까지 문제 없이 실장할 수 있으면 RN으로 

맥에서 현재 파일/폴더의 경로 복사하기 `option+command+c`


11.08.

장치 이름이 고정이 아니잖아? 잘못된 장치를 선택하면 어케해야하지?
지금 어디서 막히는거지??? 장치가 어드버타이징을 안하고 있나??
이 장치 자체를 우리쪽에서 다 만드는건가? 그럼 특이 상황의 신호도 고정인가? 신호를 받기만 하는거라면 집에 있는 텐키리스 키보드로 어케되지않을까?

- 만약 리액트로 개발하는게 아니었으면 ble와 블루투스 클래식의 구분이 필요없는지?
- ble쪽에서 꾸준하게 신호보내는 로직은 필요없는지?
- 일단 plx가 텐키리스 키보드 탐지하는지 확인
	- 키 입력을 받을 수 있는지 확인
	- 1번 키 눌렀을 때 SMS가 전송되도록 일단 구조 짜면 나중에 ble가 바뀌어도 크게 손댈 부분은 없어질듯