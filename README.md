# Fit-Got-U


#### poseEstimate 부분과 로컬 db연결
#### 데이터 분석 오류 수정
#### 인트로 시간 축소
#### 그외 자잘한 수








--------------------------------------------------------------------------------
Fitness For you

2019-03-21
그냥 기본인 com.example.myapplication 으로 만들었음.
SDK는 26(Oreo)를 이용.
자바는 JDK 8 이용.

Pose Estimation For Android 전체구조

CameraActivity.java 에서 시작 Camera2BasicFrgment 객체 호출

Camera2BasicFrgment에서 백그라운드 스레드로 카메라의 이미지를 처리한다. 

	Background Thread에서 RunnableperiodicClassify()를 반복적으로 호출
	
	RunnablePeriodicClassify()는 Classifyframe을 실행
	
	ClassifyFrame은 Camera로 캡쳐한 이미지를 PoseEstimationfloatInception의 classifyframe 으로 넘긴다. 
	
	PoseEstimationfloatInception.classifyframe에서 runinference()를 진행
	
	여기서 mace와 opencv를 통해 이미지를 처리한다. 
	
	여기서 걸린 시간을 측정된다. ( ex) 화면에 표시되는 37ms가 이 것)

mPrintpointArray에 mace를 통해 처리된 결과값이 들어간다.(post process 처리된것)

다시 Camera2BasicFrgment 여기로 돌와와서 이 값을 Drawview객체로 넘긴다. 
	
Drawview객체 내에서 넘겨받은 이 값을 setDrawviewpoint로 화면에 맞게 처리한다. 

좌표 값과 스켈레톤을 여기서 그린다. 

우리가 임시로 출력하는 값은 Camera2BasicFrgment 에서 출력되어 보여준다. 

json 형식 내의 좌표 정보 순서는 다음과 같다.

TOP(머리), NECK, R_SHOULDER, R_ELBOW, R_WRIST, L_SHOULDER< L_ELBOW, L_WRITST, R_HIP, R_KNEE, R_ANKLE, L_HIP, L_KNEE, L_ANKLE
로 총 14개의 KeyPoint

2019-05-02 카메라 전면부로 수정

2019-05-07 간단한 선택 UI 추가. PoseEstiamtion화면에 선택한 운동과 종료버튼 추가(다시 스켈레톤 보이게, sleep 500ms)
