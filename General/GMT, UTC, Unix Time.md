	## Unix Time
- 시각을 나타내는 방식이다.
- POSIX시간이나 Epoch[^주1] 시간이라고 부르기도 한다.
- **1970년 1월 1일 00:00:00 협정 세계시(UTC)부터의 경과 시간을 초로 환산하여 정수로 나타낸 것이다.**
- 윤초 때문에 유닉스 시간이 표현할 수 없는 UTC가 있다. 예를 들면 `1998년 12월 31일 23:59:60`같은.
- [유닉스 시간의 장점은 시간을 정수로 표현하여 파싱하기가 쉽고 다른 시스템 간에서 사용할 수 있게 되는 것.](https://kb.narrative.io/what-is-unix-time)

### 유닉스 시간의 유래
- January 1st, 1970 at 00:00:00 UTC is referred to as the Unix epoch.   Early Unix engineers picked that date arbitrarily because they needed to set a uniform date for the start of time, and New Year's Day, 1970, seemed most convenient. [^주2]

### y2k 사건

참고 자료
https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%8B%89%EC%8A%A4_%EC%8B%9C%EA%B0%84
https://kb.narrative.io/what-is-unix-time
https://nunucompany.tistory.com/14

[^주1]: 세, 세대, 시대(=era)
[^주2]: 파파고 번역 - 1970년 1월 1일 00:00 UTC는 유닉스 시대라고 합니다. 초기 유닉스 엔지니어들은 시간 시작 날짜를 획일적으로 정해야 했기 때문에 임의로 그 날짜를 선택했고, 1970년 새해 첫날이 가장 편리해 보였다.