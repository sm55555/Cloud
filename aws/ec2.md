# 인스턴스 종료

인스턴스 실수로 종료 막기 -> disableApiTermination 속성을 true

리눅스 shutdown -h or Window shutdown 막으려면 -> instanceInitiatedShutdownBehavior 인스턴스 속성을 stop이나 terminate 설정
