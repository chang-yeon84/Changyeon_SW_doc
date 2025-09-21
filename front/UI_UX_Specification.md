# 로그인 페이지 (Login Page) UI 개발 명세서

## 1.1. 페이지 개요 (Overview)
- **페이지 이름:** 로그인 페이지 / login_page
- **목적:** 소셜 로그인(네이버)을 통해 사용자를 인증하고 앱의 핵심 기능에 접근할 수 있도록 합니다.  
- **주요 기능:** 네이버 계정을 이용한 소셜 로그인  

## 1.2. 컴포넌트 분석 (Component Breakdown)
- **AppLogo**  
  - 앱의 로고가 표시될 컴포넌트입니다.  

- **SocialLoginButton**  
  - 소셜 로그인 기능을 수행하는 버튼 컴포넌트입니다.  
  - **Props:**
    - `onClick` (Function)

## 1.3. 상태 관리 (State Management)


## 1.4. 사용자 인터랙션 및 이벤트 처리 (User Interactions & Events)
- **사용자 액션:** '네이버 로그인' 버튼 탭  
- **이벤트 핸들러:**  
  1. `isLoading` 상태를 `true`로 설정  
  2. 네이버 OAuth 인증 API 호출  
  3. 성공 시: 인증 토큰을 저장하고 메인 화면으로 이동  
  4. 실패 시: `isLoading` 상태를 `false`로 변경, 에러 메시지 노출  

## 1.5. 예외 처리 (Edge Cases)
- **API 인증 실패:**  
  - 사용자가 인증 창에서 취소하거나 네트워크 오류 발생 시  
  - "로그인에 실패했습니다. 잠시 후 다시 시도해주세요." 팝업 메시지 표시  

- **네트워크 연결 없음:**  
  - 오프라인 상태에서 로그인 시도할 경우  
  - "인터넷 연결을 확인해주세요." 알림 표시  

## 1.6. 접근성 (Accessibility)

## 1.7. 페이지 이미지
![페이지 이미지](front/Ui_images/login.png)


# 메인 대시보드 (Main Dashboard) UI 개발 명세서

## 1.1. 페이지 개요 (Overview)
- **페이지 이름:** 메인 대시보드 / main
- **목적:** 사용자가 오늘 예정된 일정을 한눈에 파악하고, 현재 날씨 및 다가오는 일정에 대한 실시간 알림을 제공하는 앱의 메인 화면입니다.  
- **주요 기능:**  
  - 오늘 일정 목록 조회
  - 일정 완료 상태 표시    
  - 현재 날씨 확인  
  - 일정 기반 동적 알림 확인  
  - 다른 주요 메뉴(추천, 프로필)로의 이동  

## 1.2. 컴포넌트 분석 (Component Breakdown)
- **Header**  
  - 페이지 제목("오늘의 일정"), 일정 요약("3개의 일정이 있습니다")  
  - 오늘 일정 리스트로 이동하는 아이콘 포함 상단 영역  

- **ScheduleCard**  
  - 하나의 일정을 표시하는 카드 컴포넌트  
  - `시간`, `일정 이름`, `위치` 정보를 `props`로 받음  

- **WeatherInfoCard**  
  - 현재 날씨 아이콘, 온도(예: 23°), 날씨 상태(맑음), 지역(인천광역시) 표시  

- **AlertCard**  
  - 다가오는 일정에 대한 동적 정보 표시  
  - 외출 준비 알림, 대중교통 도착 정보 등 포함  

- **BottomNavigationBar**  
  - 앱의 주요 기능으로 이동하는 하단 탭 바  
  - '일정', '추천', '프로필' 세 가지 탭 구성  
  - 현재 '일정' 탭이 활성화 상태  

## 1.3. 상태 관리 (State Management)
- **schedules (Array):** API를 통해 받아온 오늘 일정 목록 데이터  
- **weather (Object):** 현재 위치의 날씨 정보  
- **alerts (Object 또는 Array):** 임박한 일정 기반 생성된 알림 데이터  
- **activeTab (String):** BottomNavigationBar에서 현재 활성화된 탭 상태 (기본값: '일정')  

## 1.4. 사용자 인터랙션 및 이벤트 처리 (User Interactions & Events)
- **ScheduleCard 탭:**  
  - 특정 일정을 탭 시 상세 정보 및 지도 화면으로 이동  

- **캘린더 아이콘 탭:**  
  - 일정 리스트 목록 페이지로 이동

- **BottomNavigationBar의 '추천' 또는 '프로필' 탭:**  
  - 각 기능에 해당하는 페이지로 화면 전환  

## 1.5. 예외 처리 (Edge Cases)
- **일정 없음:**  
  - 오늘 일정이 없을 경우, "오늘 등록된 일정이 없습니다." 안내 메시지 표시  

- **API 실패:**  
  - 날씨 또는 일정 정보 불러오기 실패 시  
  - "정보를 불러올 수 없습니다." 메시지와 함께 '새로고침' 기능 제공  

## 1.6. 접근성 (Accessibility)

## 1.7. 페이지 이미지
 ![페이지 이미지](front/Ui_images/main.png)

# 일간 상세 스케줄 (Daily Schedule) UI 개발 명세서

## 1.1. 페이지 개요 (Overview)
- **페이지 이름:** 일간 스케줄 리스트 /sch_list 
- **목적:** 사용자가 선택한 특정 날짜의 모든 일정을 시간 순서대로 상세하게 보여주고, 새로운 일정을 추가할 수 있도록 합니다.  
- **주요 기능:**  
  - 날짜별 일정 목록 조회  
  - 날짜 이동
  - 날짜 텍스트  클릭시 팝업 캘린더 이미지로 날짜 선택 가능  
  - 일정 완료 상태 표시  
  - 각 일정의 상세 정보(시간, 장소, 날씨, 출발지, 소요 시간) 확인  
  - 신규 일정 추가  

## 1.2. 컴포넌트 분석 (Component Breakdown)
- **Header**   
  - 현재 날짜 표시("2025년 9월 12일")  
  - 이전/다음 날로 이동하는 네비게이션 버튼 포함
  - 날짜 텍스트 클릭시 캘린더 팝업 

- **ScheduleDetailCard**  
  - 상세 일정 표시 카드 컴포넌트  
  - **Props:**  
    - `isCompleted` (Boolean)  
    - `startTime`, `endTime`  
    - `title`, `location`  
    - `weatherIcon`, `temperature`, `weatherText`  
    - `startPoint`, `transportModeIcon`, `travelTime`  
  - **설명:**  
    - 완료된 일정에는 체크마크 오버레이 표시  
    - 시간, 장소, 날씨, 출발지로부터의 이동 수단 및 소요 시간 정보 포함  

- **AddScheduleCard**  
  - 새 일정을 추가하는 + 아이콘 카드 형태 버튼  

- **BottomNavigationBar**  
  - 앱 주요 기능(일정, 추천, 프로필) 이동하는 하단 탭 바  

## 1.3. 상태 관리 (State Management)
- **selectedDate (Date):** 사용자가 선택한 현재 날짜로, 변경 시 해당 날짜 일정 목록을 재조회  
- **schedulesForDate (Array):** 선택 날짜에 해당하는 일정 객체 배열, 렌더링에 필요한 모든 데이터 포함  

## 1.4. 사용자 인터랙션 및 이벤트 처리 (User Interactions & Events)
- **이전/다음 날짜 버튼(<, >) 탭:**  
  - `selectedDate`를 하루 전/후로 변경  
  - 변경된 날짜 일정 목록 API 호출 및 새로고침  

- **ScheduleDetailCard 탭:**  
  - 해당 일정의 상세 정보 화면으로 이동  

- **AddScheduleCard (+ 버튼) 탭:**  
  - 신규 일정 추가 페이지로 이동  

- **뒤로 가기 슬라이딩:**  
  - 이전 화면(메인 대시보드)으로 돌아가기  

## 1.5. 예외 처리 (Edge Cases)
- **일정 없음:**  
  - 선택된 날짜에 일정이 없으면  
  - AddScheduleCard 만 화면에 표시

- **API 실패:**  
  - 서버에서 일정 정보 불러오기 실패 시  
  - 에러 메시지와 재시도 버튼 노출  

## 1.6. 접근성 (Accessibility)

## 1.7. 페이지 이미지
![페이지 이미지](front/Ui_images/sch_list.png)

# 일정 상세 정보 (Schedule Detail) UI 개발 명세서

## 1.1. 페이지 개요 (Overview)
- **페이지 이름:** 일정 상세 정보  / schedule_detail
- **목적:** 단일 일정에 대한 모든 상세 정보(제목, 시간, 경로, 교통수단)를 시각적으로 보여주고, 시간대별 날씨와 주변 장소 추천 등 부가 정보를 제공합니다.  
- **주요 기능:**  
  - 일정 이름 확인
  - 일정 시간 확인
  - 상세 경로 지도 확인  
  - 교통수단별 경로 조회  
  - 시간대별 날씨 예보 확인  
  - 일정 수정 및 삭제  
  - 주변 장소 추천 버튼 

## 1.2. 컴포넌트 분석 (Component Breakdown)
- **Header**  
  - 페이지 제목("아침 운동")  
  - '수정', '삭제' 기능 아이콘 버튼 포함  

- **RouteInfo**  
  - 일정 시간("09:00 ~ 09:30"), 출발지("집"), 목적지("뚝섬 한강 공원") 정보 표시  

- **TransportModeSelector**  
  - '대중교통', '승용차', '도보' 등 교통수단 선택 탭 컴포넌트  

- **MapView**  
  - 출발지부터 목적지까지 경로를 지도 위에 표시  

- **HourlyWeatherForecast**  
  - 특정 지역("인천광역시")의 시간대별 날씨 예보를 가로 스크롤 카드 형태로 표시  

- **BottomNavigationBar**  
  - 주요 섹션(일정, 추천, 프로필)으로 이동하는 하단 탭 바  

## 1.3. 상태 관리 (State Management)
- **scheduleData (Object):** 현재 페이지에 표시할 모든 일정 정보 객체  
- **selectedTransportMode (String):** 사용자가 선택한 교통수단 상태 ('도보', '대중교통' 등)  
  - 변경 시 MapView 경로 업데이트  
- **routeData (Object):** selectedTransportMode에 따른 API로 받은 지도 경로 데이터  
- **weatherData (Array):** 시간대별 날씨 예보 데이터 배열  

## 1.4. 사용자 인터랙션 및 이벤트 처리 (User Interactions & Events)
- **'수정' 아이콘 탭:**  
  - 현재 일정 데이터를 가지고 '새 일정 추가/수정' 페이지로 이동  

- **'삭제' 아이콘 탭:**  
  - "일정을 삭제하시겠습니까?" 확인 모달 표시  
  - 확인 시 일정 삭제 API 호출  

- **TransportModeSelector 탭 선택:**  
  - `selectedTransportMode` 상태 변경  
  - 선택된 교통수단에 맞는 경로 API 요청 및 MapView 업데이트  

## 1.5. 예외 처리 (Edge Cases)
- **경로 정보 없음:**  
  - 특정 교통수단 경로 정보가 없을 경우  
  - 지도 위에 "경로 정보를 찾을 수 없습니다." 메시지 표시  

- **API 실패:**  
  - 날씨 또는 지도 정보 불러오기 실패 시  
  - 해당 컴포넌트 영역에 에러 메시지와 재시도 버튼 노출  

## 1.6. 접근성 (Accessibility)

## 1.7. 페이지 이미지
![페이지 이미지](front/Ui_images/sch_detail.png)
