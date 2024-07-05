# HTML,CSS를 사용하여 깔끔한 이력서 웹 페이지를 디자인하고 구조화
# HTML 기본 구조

```html
<!DOCTYPE html>
<html lang="ko">
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
  </body>
</html>
```

### <!DOCTYPE html>

- DOCTYPE은 문서의 내용이 시작되기 전에 해당 문서가 어떤 마크업 언어 형식으로 작성되었는지를 명시하는 역할
- DOCTYPE의 뒤에 html이라고 쓰여 있는 것은 이 문서가 HTML5로 작성되었음을 명시

### <html>

- 문서 형식 선언 이후 실제 문서의 내용을 표시하는 태그, 여는 태그와 닫는 태그는 각각 문서의 시작과 끝을 알린다.
- 위와 같이 언어 코드를 속성값으로 줄 수 있다.

### <head>

- <html> 태그 안에는 <head>와 <body>라는 두 개의 하위 태그가 있는데 보통 <head>태그에는 문서의 정보를 전달하는 다양한 설정 태그가 존재한다.

### <meta>

- <meta> 태그는 문서의 키워드 또는 설정 등 문서와 관련된 여러가지 항목들을 지정할 때 사용하는 태그이다.
- 그 중 대표적인 항목이 위와 같이  문서의 인코딩 방식을 설정해주는 문자셋이다.

### <title>

- 브라우저 탭 메뉴에 표시되는 문서의 제목

### <Body>

- 화면에 표시될 컨텐츠

# CSS 구조

- Cascading Style Sheets의 약자로 HTML, XHML, XML 같은 문서의 스타일을 꾸밀 때 사용하는 스타일 시트 언어
- HTML이 웹사이트에서 화면에 표시되는 정보라면 CSS는 웹 사이트에서 화면에 표시되는 정보들을 꾸며주는 역할

## Flexbox, Grid

### Flexbox

- Flexbox는 1차원 레이아웃 모델로서, 요소들이 컨테이너 안에서 배치되고 정렬되는 방식을 간단하고 직관적으로 조정할 수 있게 해줌
- Flexbox는 요소들을 세로 또는 가로로 정렬할 때, 요소들 간의 간격을 일정하게 유지할 때, 요소들을 중앙 정렬할 때 주로 사용

### 주요 속성

1. **flex-container**
    - `display: flex;`를 사용하여 컨테이너를 플렉스 컨테이너로 설정
2. **flex-direction**
    - 주 축의 방향을 설정, 기본값은 `row`(가로 방향)
    
    ```css
    .container {
        display: flex;
        flex-direction: column; /* 세로 방향 */
    }
    
    ```
    
3. **justify-content**
    - 주 축을 따라 요소들을 정렬 예를 들어, 중앙에 배치하고 싶다면 `center`를 사용
    
    ```css
    .container {
        display: flex;
        justify-content: center;
    }
    
    ```
    
4. **align-items**
    - 교차 축을 따라 요소들을 정렬 예를 들어, 세로 중앙에 배치하고 싶다면 `center`를 사용
    
    ```css
    .container {
        display: flex;
        align-items: center;
    }
    
    ```
    

### Grid

- Grid는 2차원 레이아웃 모델로서, 행과 열을 모두 사용하여 요소들을 배치할 수 있음

### 주요 속성

1. **grid-container**
    - `display: grid;`를 사용하여 컨테이너를 그리드 컨테이너로 설정
2. **grid-template-columns / grid-template-rows**
    - 열과 행의 크기를 정의
    
    ```css
    .container {
        display: grid;
        grid-template-columns: repeat(3, 1fr); /* 3개의 동일한 너비의 열 */
        grid-template-rows: auto; /* 행의 높이는 자동으로 설정 */
    }
    
    ```
    
3. **grid-gap**
    - 그리드 아이템들 사이의 간격을 설정
    
    ```css
    .container {
        display: grid;
        grid-gap: 10px; /* 10픽셀 간격 */
    }
    
    ```
    
4. **grid-area**
    - 그리드 아이템의 위치를 지정
    
    ```css
    .item {
        grid-area: 1 / 1 / 2 / 3; /* 시작 행 / 시작 열 / 끝 행 / 끝 열 */
    }
    
    ```
    

### Flex와 Grid의 차이

### Flex와 Grid의 차이

### 1. 레이아웃 모델

- **Flexbox**
    - Flexbox는 1차원 레이아웃 모델이며 이는 요소를 한 방향(가로 또는 세로)으로 정렬하고 배치하는 데 최적화되어 있음을 의미
    - Flexbox는 주로 요소를 가로로 나열하거나 세로로 정렬할 때 사용
    
    ```css
    .container {
        display: flex;
        flex-direction: row; /* 가로 방향 */
    }
    
    ```
    
- **Grid**
    - Grid는 2차원 레이아웃 모델이며 이는 요소를 행과 열을 사용하여 배치할 수 있음을 의미
    - Grid는 복잡한 레이아웃을 설계하고, 다양한 크기의 행과 열을 조정할 때 유용
    
    ```css
    .container {
        display: grid;
        grid-template-columns: repeat(3, 1fr); /* 3개의 동일한 너비의 열 */
        grid-template-rows: auto; /* 행의 높이는 자동으로 설정 */
    }
    
    ```
    

### 2. 요소 배치 방법

- **Flexbox**
    - Flexbox는 주 축(main axis)과 교차 축(cross axis)을 사용하여 요소를 배치
    - 주 축은 `flex-direction` 속성에 따라 가로 또는 세로 방향으로 설정됨, (교차 축은 주 축에 수직인 방향을 의미)
    
    ```css
    .container {
        display: flex;
        flex-direction: column; /* 주 축: 세로 */
        align-items: center; /* 교차 축: 가로 중앙 정렬 */
    }
    
    ```
    
- **Grid**
    - Grid는 명시적으로 행과 열을 정의하여 요소를 배치
    - 각 그리드 아이템은 그리드 셀에 위치하게 되며, 행과 열을 통해 보다 정밀한 레이아웃 구성 가능
    
    ```css
    .container {
        display: grid;
        grid-template-columns: 1fr 2fr 1fr; /* 열 정의 */
        grid-template-rows: 100px auto; /* 행 정의 */
    }
    
    ```
    

# 웹 폰트 사용

## 웹 폰트 사용

- 웹 폰트는 웹사이트의 텍스트를 보다 아름답게 만들기 위해 사용하는 폰트
- 웹 폰트를 사용하면 사용자의 시스템에 설치된 폰트에 구애받지 않고, 모든 사용자에게 동일한 폰트 스타일을 제공할 수 있음

### **1. 폰트 선택 및 임포트 링크 복사**

원하는 폰트에서 제공되는 `<link>` 태그를 복사

```html
<link rel="preconnect" href="https://statics.goorm.io" crossorigin="anonymous" />
<link rel="preload" as="style" crossorigin href="https://statics.goorm.io/fonts/GoormSans/v1.0.0/GoormSans.min.css" />
<link rel="stylesheet" href="https://statics.goorm.io/fonts/GoormSans/v1.0.0/GoormSans.min.css" />
```

### **2. HTML 파일의 `<head>` 섹션에 링크 추가**

복사한 `<link>` 태그를 HTML 파일의 `<head>` 섹션에 추가

```html
<head>
<meta charset="UTF-8">
<link rel="preconnect" href="https://statics.goorm.io" crossorigin="anonymous" />
<link rel="preload" as="style" crossorigin href="https://statics.goorm.io/fonts/GoormSans/v1.0.0/GoormSans.min.css" />
<link rel="stylesheet" href="https://statics.goorm.io/fonts/GoormSans/v1.0.0/GoormSans.min.css" />
<style>@import url(styles.css);</style>
<title> 김민제 이력서 </title>
</head>

```

### **3. CSS에서 폰트 import**

CSS 파일에서 가져온 폰트 import

```css
@import url("https://statics.goorm.io/fonts/GoormSans/v1.0.0/GoormSans.min.css");
```

### 4. font 적용

- CSS 파일에 font 적용
    
    ```css
    .info-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        grid-gap: 20px;
        font-family: 'GoormSans', sans-serif;
        font-weight: 500;
        font-style: normal;
    }
    ```
    

# 반응형 디자인

- 반응형 디자인은 다양한 디바이스와 화면 크기에서 웹 페이지가 잘 보이도록 하는 웹 디자인 방식

## 1. 뷰포트 설정

뷰포트 메타 태그로 브라우저에게 웹 페이지의 너비와 초기 스케일을 설정하는 방법을 명시

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

## 2-1. 미디어 쿼리 사용

미디어 쿼리로 반응형 디자인을 구현

```css
@media (max-width: 700px) {
    .info-grid {
        grid-template-columns: repeat(auto-fit, minmax(50%, 1fr));
    }
}
```

## 2-2. 유연한 이미지 사용

이미지의 너비를 100%로 설정하면 컨테이너의 크기에 맞게 자동으로 조정됩니다.

```css
img {
  width: 100%;
  height: auto;
}

```

## 2-3. CSS Grid와 Flexbox 사용

CSS Grid와 Flexbox는 요소를 정렬하고 배치하는 데 도움을 준다.

### Flexbox 예시

```css
.container {
  display: flex;
  flex-wrap: wrap;
}

.item {
  flex: 1 1 100%; /* 기본적으로 전체 너비 사용 */
}

@media (min-width: 768px) {
  .item {
    flex: 1 1 48%; /* 화면 너비가 768px 이상일 때 절반 너비 사용 */
    margin: 1%;
  }
}

```

### Grid 예시

```css
.container {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
}

@media (min-width: 768px) {
  .container {
    grid-template-columns: repeat(2, 1fr); /* 2개의 동일한 열 */
  }
}

@media (min-width: 1024px) {
  .container {
    grid-template-columns: repeat(3, 1fr); /* 3개의 동일한 열 */
  }
}

```
