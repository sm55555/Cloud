# Windows 파일 시스템 확장

### 1. 중요한 데이터가 저장된 파일 시스템을 확장하려면 먼저 스냅샷

### 2. [실행(Run)] 대화 상자에 diskmgmt.msc를 입력하고 Enter

![image](https://user-images.githubusercontent.com/38831314/148308639-58d80c7e-781d-4583-9b64-229d4fb5d40d.png)

### 3. Action -> Rescan 통해서 추가 볼륨 확인
   (볼륨은 마스터 부트 레코드(MBR) 파티션 스타일을 사용하며 이미 크기가 2TB입니다. MBR을 사용하는 볼륨의 크기는 2TB를 초과할 수 없습니다.)
   
### 4. 확장된 드라이브를 오른쪽 클릭하여 컨텍스트 메뉴를 열고 볼륨 확장(Extend Volume)을 선택

![image](https://user-images.githubusercontent.com/38831314/148308788-4c33246b-ce92-4535-a4e4-1524a9e90bd2.png)

### 5. 강조된 부분은 최종 볼륨이 아니라 추가되는 볼륨의 양! 참고

![image](https://user-images.githubusercontent.com/38831314/148308865-f9e921db-91c5-4a53-8653-85249737ac58.png)

### 6. 확장 결과

![image](https://user-images.githubusercontent.com/38831314/148308957-bc46acd4-a8de-4f87-b2cc-dddd57743d99.png)




