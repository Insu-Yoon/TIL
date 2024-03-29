# Web에 Font 첨부하는 법
## 만약 웹페이지에 적용하려는 폰트가 만약 pc에 설치되지않은 font라면?  
-> 해당 폰트로 보여지지 않고, 브라우저가 제공하는 기본 폰트로 보일것   
**따라서, 의도한 화면을 보여주기 위해선 폰트를 첨부할 필요가 있다.**

```css
파일 최상단에 @font-face{ font family : '임의로 작명'; src : url();
/*CSS File*/
@font-face{
  font-family : '임의로 작명(사용할 폰트명 등)';
  src : url(폰트 파일의 경로);
}
/* 폰트 파일 (ttf, woff, woff2 등의 파일을 같이 업로드 했다면 상대경로 입력)*/
/* 또는 구글 폰트(https://fonts.google.com/) 등 폰트 디렉터리 활용*/
```

## 용량 줄이기
용량을 줄이려면 ttf대신 .woff 또는 .woff2 사용하는 것이 좋음  
특히 한글 폰트는 용량 엄청 잡아먹으므로, 첨부하더라도 한두개 선에서 끝낼 것

## 호환성 
예~전엔 IE 환경에서 폰트관련 추가 설정이 필요했다고 하는데, 최근엔 신경쓸 필요 없는 듯

## 트래픽 절약
위에서 언급한 .woff, .woff2를 활용하거나, 구글 폰트 등을 활용하여 트래픽을 절약할 수 있음

# 폰트 안티앨리어싱 
p, h4, h3, h2, h1, span 등 다 싸잡아서 폰트 자체를 살짝 회전시켜서 부드럽게 만들 수 있음   

예시코드
```css
p, h4, h3, h2, h1, span{ transform: rotate(0.03deg)}
```
