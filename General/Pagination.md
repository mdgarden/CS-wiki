---
tags:
  - Pagination
---

페이지네이션(pagination)은 웹 개발에서 매우 중요한 개념입니다. 페이지네이션이란, 데이터의 큰 집합을 사용자에게 보여줄 때 전체 데이터를 한 번에 보여주는 대신, 작은 부분으로 나눠서 페이지별로 보여주는 기술입니다. 이를 통해 사용자는 데이터를 쉽게 탐색할 수 있고, 서버는 한 번에 처리해야 하는 데이터 양을 줄여 성능을 향상시킬 수 있습니다.

예를 들어, 소셜 미디어 플랫폼에서 수천 개의 게시글을 한 번에 로드하려고 하면, 서버에 큰 부담이 가고 사용자 경험도 좋지 않습니다. 페이지네이션을 사용하면, 사용자는 필요한 데이터만큼만 요청하여 볼 수 있으며, 서버도 효율적으로 데이터를 처리할 수 있습니다.
## Page Based Pagination

페이지 기반 페이지네이션(Page Based Pagination)은 데이터를 페이지로 구분하여 사용자에게 제공하는 방법 중 하나입니다. 이 방식에서는 각 페이지가 고유한 번호를 가지며, 사용자는 특정 페이지 번호로 직접 이동할 수 있습니다. 페이지 기반 페이지네이션은 사용자가 데이터를 탐색하고 원하는 위치로 쉽게 이동할 수 있게 해줍니다.
## Cursor Based Pagination
- 가장 최근에 가져온 데이터를 기준으로 다음 데이터를 가져오는 Pagination
- 요청을 보낼 때 마지막 데이터의 기준값(ID등 Unique 값)과 몇 개의 데이터를 가져올지 명시
- 스크롤 형태의 리스트에서 자주 사용
	- 예) 앱의 ListView, 무한 스크롤
- 최근 데이터의 기준값을 기반으로 쿼리가 작성되기 때문에 데이터가 누락되거나 중복될 확률이 적음
데이터 페이지네이션 방식에는 크게 페이지 기반(page-based)과 커서 기반(cursor-based) 두 가지가 있으며, 각각의 장단점을 다음 표로 정리할 수 있습니다:

| 기준            | 페이지 기반 페이지네이션                                                                                  | 커서 기반 페이지네이션                                                                |
| ------------- | ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| **정의**        | 데이터를 고정된 크기의 페이지로 나누고, 각 페이지를 숫자로 식별합니다.                                                       | 데이터의 특정 지점(커서)에서 시작하여 고정된 크기만큼의 데이터를 제공합니다.                                 |
| **장점**        | - 사용자가 원하는 페이지로 직접 이동할 수 있어 탐색이 용이합니다.<br>- 전체 데이터셋의 크기를 알기 쉽습니다.                              | - 데이터 중복이 없습니다.<br>- 실시간으로 업데이트되는 데이터셋에 효율적입니다.<br>- 페이지 사이즈가 일정하지 않아도 됩니다. |
| **단점**        | - 대용량 데이터에서 마지막 페이지로 이동하는 데 시간이 많이 걸릴 수 있습니다.<br>- 데이터셋이 변경될 때 페이지네이션 결과에 중복이나 누락이 발생할 수 있습니다. | - 사용자가 임의의 페이지로 직접 이동하기 어렵습니다.<br>- 전체 페이지 수나 데이터셋의 크기를 알기 어렵습니다.           |
| **적합한 사용 사례** | - 사용자가 데이터셋 전체에서 특정 위치로 직접 이동하길 원할 때<br>- 데이터의 변동성이 낮은 경우                                      | - 데이터가 실시간으로 변하는 경우<br>- 데이터 중복이나 누락 없이 순차적으로 데이터를 탐색하길 원할 때                |

각 방식은 특정 상황이나 요구 사항에 따라 더 적합할 수 있으므로, 애플리케이션의 특성과 사용자의 필요를 고려하여 적절한 페이지네이션 전략을 선택하는 것이 중요합니다.