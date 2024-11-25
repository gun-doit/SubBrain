## **주의 사항 및 순서**

**연결을 할때 모든 선을 연결하고 전원을 줄것  
KY6를 연결할때 방향을 확인할 것  
**

1. watchdog flag를 0으로 설정할 것
2. File - RunScript - 실행하고자 하는 Workspace/T32/start.cmmㅇ
    
    ![[image 25.png|image 25.png]]
    
3. FLASH.Erase.all
4. RE - Reset
5. WF - write flash ( fbl → app 순)
6. WM - watch Memory
7. Run  
      
    

  

  

[함수 수행 시간을 측정하고 싶습니다. - TRACE32](https://trace32.com/wiki/index.php/%ED%95%A8%EC%88%98_%EC%88%98%ED%96%89_%EC%8B%9C%EA%B0%84%EC%9D%84_%EC%B8%A1%EC%A0%95%ED%95%98%EA%B3%A0_%EC%8B%B6%EC%8A%B5%EB%8B%88%EB%8B%A4.)