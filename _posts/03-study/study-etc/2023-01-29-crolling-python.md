---
title: /etc/ 파이썬으로 네이버뉴스 크롤링(+엑셀에 넣기)
author: ggggraceful
date: 2023-01-29
categories: [03.STUDY, etc]
tags: [STUDY]
---

<br/>
<br/>

{: .prompt-warning }
> ✔️ 크롤링 주의사항  
> - 상업적으로 이용하면 안된다.  
> - 크롤링 대상 서버에 부담을 주면 안된다.  
> 　: 대형 웹사이트에는 무리를 주지 않겠지만,   
> 　작은 사이트에 과도한 크롤링 요청은 트래 픽 초과등의 악영향을 줄 수 있고,    
> 　심하면 서버가 멈출 위험성이 있다. 심하면 영업방해로 인한 처벌도 가능하다. 

<br/>
<br/>

# 1. 파이썬으로 엑셀파일 생성

---

```python
import openpyxl

# 1. 엑셀 만들기
wb = openpyxl.Workbook()

# 2. 엑셀 시트 만들기
ws = wb.create_sheet('네이버뉴스')

# 3) 데이터 추가하기
ws['A1'] = '기사 제목'
ws['B1'] = '기사 url'

# 4) 엑셀파일 저장하기
wb.save('네이버뉴스_data.xlsx')

```

<br/>

작성후 실행하면  
네이버뉴스_data의 이름을 가진 엑셀파일 하나가 생성된다.

파일 안에는 '네이버뉴스'라는 시크가 추가되어있고, 
그안에 A1셀에 '기사 제목'을, B1셀에는 '기사 url'이 추가된 것을 확인할 수 있다.

<br/>

![사진](https://user-images.githubusercontent.com/109974940/215439083-b8be789b-621d-4238-99bb-3a1b9ea84065.png)

<br/>
<br/>

# 2. 파이썬으로 크롤링해 엑셀시트 채우기

---

```python
import requests
from bs4 import BeautifulSoup 
import pyautogui # 창을 띄워 입력값을 받을 때 사용
import openpyxl # 엑셀 사용시 필요

fpath = '네이버뉴스_data.xlsx' 
wb = openpyxl.load_workbook(fpath)
ws = wb['네이버뉴스'] # 해당 시트 선택

keyword = pyautogui.prompt("검색어를 입력하세요>>>") # 검색어 입력창
lastpage = pyautogui.prompt("마지막 페이지번호를 입력해 주세요.") # 마지막 페이지번호 입력창

pageNum = 1
row = 2

# 크롤링하려는 페이지의 url이 1, 11. 21, .. 패턴으로 생겨서, 10씩 곱한값으로 출력
for i in range(1, int(lastpage) * 10, 10):
    url = f"https://search.naver.com/search.naver?where=news&sm=tab_jum&query={keyword}&start={i}" # 크롤링 해올 사이트의 url
    response = requests.get(url)
    html = response.text 
    soup = BeautifulSoup(html, 'html.parser') # html 번역을 도와줌
    links = soup.select(".news_tit") # 결과는 리스트
    for link in links:
        title = link.text # 태그 안에 텍스트요소를 가져옴
        url = link.attrs['href'] # href의 속성값을 가져옴
        print(title, url) # 콘솔창에서 프린트에 결과값 미리보기
        ws[f'A{row}'] = title # 엑셀파일 A열에 title 입력
        ws[f'B{row}'] = url   # 엑셀파일 B열에 url 입력
        row = row +1 # 다음 행
    pageNum = pageNum + 1 # 다음 페이지

wb.save(fpath) # 엑셀파일에 내용을 저장
```

<br/>

![사진](https://user-images.githubusercontent.com/109974940/215476201-20630a34-cf39-4876-b299-1cc9fdcf62e6.png)

## 크롤링에 자주 사용하는 html 태그 종류

---

<br/>

| 태그명    | 역할                |
|--------|-------------------|
| div    | 구역 나누기, a태그의 부모태그 |
| a      | 링크, div태그의 자식태그   |
| h1     | 제목                |
| p      | 문단                |
| ul, li | 목록                |

<br/>
<br/>

## CSS 선택자

---

### 태그 선택자

HTML 
```html
<h1>제목입니다</h2>
<!-- 선택자 : h1 -->
```

### id 선택자

HTML
```html
<div id="articleBody">본문 내용입니다.</div>
<!-- 선택자 : #articleBody -->
```

### class 선택자

HTML
```html
<div class="info_group">뉴스 목록</div>
<!-- 선택자 : .info_group -->
```
### 자식 선택자

- 보통 내가 원하는 태그에 별명이 없을 때 사용
- 바로 아래에 있는 태그를 선택

HTML
```html
<div class="logo_sports"> 
  <span>스포츠</span>
</div>
<!-- 선택자 : .info_group > span -->
```

HTML
```html
<div class="news_headline"> 
  <h4>제목</h4>
</div>
<!-- 선택자 : .news_headline > h4 -->
```

{: .prompt-tip }
> class = /
> id = #

<br/>
<br/>

---

(참고)

- [intellij에서 python 환경 구축](https://pearlluck.tistory.com/310)
- [[Python] Selenium과 BeautifulSoup을 활용하여 네이버 뉴스 기사 크롤링하는 방법!](https://somjang.tistory.com/entry/Python-selenium%EA%B3%BC-BeautifulSoup%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%98%EC%97%AC-%EB%84%A4%EC%9D%B4%EB%B2%84-%EB%89%B4%EC%8A%A4-%EA%B8%B0%EC%82%AC-%ED%81%AC%EB%A1%A4%EB%A7%81%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)
- [Selenium을 이용한 네이버 기사 10페이지 제목 리스트 스크레이핑!(크롤링)](https://twosb.github.io/2018/06/27/Selenium%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EA%B8%B0%EC%82%AC%20%EC%8A%A4%ED%81%AC%EB%A0%88%EC%9D%B4%ED%95%91/)
- [[구글 스프레드시트] 뉴스 기사 가져오기 (뉴스 크롤링)](https://heecheoldo.tistory.com/67)
- 인프런 이것이 진짜 크롤링이다 - 기본편

<br/>
<br/>

<span style="font-size: 12px; color:  #cbce91"> 공부한 내용을 여러글과 책 읽은 내용을 바탕으로 정리하고 있습니다.</span>  
<span style="font-size: 12px; color:  #cbce91"> 좋은 글로 저의 공부에 도움을 주시는 분들께 감사드립니다. </span>  

