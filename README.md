# ROS_Navigation_in_5days

- [Unit 2 ROS Navigation Deconstruction]

ROS Navigation에서 중요한 부분은 Map을 생성한 다음에 로봇의 위치를 파악하는 Localization을 해준 

다음에 Path Planning을 통하여 원하는 위치를 가는 것입니다. 추가적으로 Transforms가 중요한데, 

이것은 로봇 어디에 laser가 부착되어있는지 입니다. 왜냐하면 데이터는 레이저 위치를 기반으로 정보를 

얻는 것이기 때문에, 로봇의 프레임에 맞게 다시 계산을 하여야 합니다. 제공되는 라이브러리를 사용하는 것은

파라미터 설정이 중요합니다.

​

- [Unit 3 Map Creation]

laser scanner와 Odometry를 센서를 이용하여 주변 환경을 둘러봄으로써, Map을 생성해줍니다. 이때 , 

ROS에서는 Rviz를 통하여 맵을 만들 수 있습니다. 이때, Map은 저장할 수 있고 다시 불러올 수 있습니다. 그리고

맵을 만든 후, 로봇의 위치도 함께 저장할 수 있습니다.

​

- [Unit 4 Robot Localiztion]

monte carlo 알고리즘은 랜덤으로 점들을 무수히 만들면 점들을 갯수를 통하여 면적을 구할 수 있는 알고리즘입니다.

이를 활용하여  위치를 결정할 수 있습니다. 우선 map을 만든 후, monte carlo 알고리즘을 이용하여 각각의 점들에서

맵이 만들어진 거리 차와 현재 가지고 있는 데이터와 비교하여 확률적으로 가장 높은 지점이 현재 위치로 결정하는 알고리즘

입니다. 이때, 가능성이 있는 위치는 빨간색 화살표로 표시가 되어집니다.(예전 뉴턴 책에서 랜덤을 만드는 함수가 중요하다고

언급을 해주었는데, 여기서 이렇게 접하게 되어 신기합니다.ㅎㅎ) 

​

- [Unit 5 Path Planning I]

경로 탐색은 Global planner 설정과 local planner 설정이 있는데, 이번 강좌에서는 Global planner에 대해서 설명을 

해주었습니다. 그리고 ROS에서 제공되어지는 Global plan 알고리즘에는

*Navfn(Dijkstra's algorithm) , Carrot Planner 가 있습니다.

​

- [Unit 6 Path Planning II]

local planner는 Odometry와 laser data를 계속하여 계산을 하고 있으면, 경로를 가는 도중, 

장애물을 마주했을 때 재계산을 통하여 경로를 다시 설정하는 것입니다. 간단하게 설명을 하면 전체적인 

경로는 global plan가 결정하고 가는 길 중간 중간 경로를 변경하는 것은 local planner를 이용하여 수정하여 

경로를 설정합니다. Rviz를 통하여 path에서 global planner와 local planner의 색깔을 변경하면 그 차이를 확인할

수 있습니다. local planner 종류에는 *dwa_local_planner(제일 많이 사용),

teb_local_planner(Timed Elastic Band Method), eband_local_planner(Elastic Band Method)가 있습니다. 

local planner의 기본적인 알고리즘 개요는 여러개의 경로를 만든 다음에 각 각의 경로에 점수를 매긴 후, 

제일 높은 점수를 가진 경로를 선택하는 알고리즘입니다.

costmap은 값이 있는 지도입니다. (각 점수를 통하여 장애물 유무를 알 수있습니다.)

종류는 global cost map 과 local cost map이 있습니다. global cost map은 현재 감지하지 않지만, 

이전에 감지하였던 것을 바탕으로 만들어진 지도이고, local cost map은 현재 센서에서 감지되고 있는 지도입니다.
