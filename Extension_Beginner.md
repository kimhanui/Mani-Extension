
## Command 실행 위치
![image](https://user-images.githubusercontent.com/30483337/114295798-6bfd9780-9ae2-11eb-92b6-84b21dcb604a.png)  
- `package.json`의 `"contributes">"commands"` 위치에 커맨드를 등록할 수 있다.  

  
![image](https://user-images.githubusercontent.com/30483337/114295871-fd6d0980-9ae2-11eb-824d-7f51037da109.png)     
- 커맨드에 연결된 활성화 이벤트가 동작하려면 해당 커맨드 이름을 확장 프로그램의 핸들러에 등록해주어야한다.  
- `extension.ts` 파일을 확인하면 `registerCommand` 함수를 이용해 커멘드 이름, 실행할 기능이 연결돼있는 것을 알 수 있음.


#### 참고 링크
http://www.santacodes.com/?p=211
