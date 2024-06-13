## 목차

1. HTML5 새로운 기능
   - 그래픽 요소
   - 위치정보 활용
   - 로컬 스토리지
   - Custom Switches
   - Datalist
   - 색상 선택기
   - 아코디언
   - 다이얼로그 모달
2. 멀티미디어
   - 오디오 삽입
   - 비디오 삽입
   - 다양한 속성
3. 유효성 검사와 접근성
   - W3C 마크업 유효성 검사
   - 웹 접근성의 개념과 중요성
   - 적절한 대체 텍스트 제공
   - 키보드 내비게이션 지원
4. 실습 프로젝트
   - 간단한 게임 만들기
   - 대화형 웹 페이지 만들기

## 1. HTML5 새로운 기능

HTML5에서는 웹 페이지를 더욱 풍부하고 대화형으로 만들 수 있는 다양한 새로운 기능이 도입되었습니다. 이 섹션에서는 그 중 몇 가지 주요 기능에 대해 알아보겠습니다.

### 그래픽 요소

HTML5에서는 `<canvas>`와 `<svg>` 태그를 사용하여 그래픽을 그릴 수 있습니다.

- `<canvas>`: 자바스크립트를 사용하여 그래픽을 그리는 데 사용됩니다. 게임, 차트, 애니메이션 등 다양한 그래픽을 그릴 수 있습니다.
- `<svg>`: 벡터 그래픽을 삽입하는 데 사용됩니다. SVG는 확대/축소해도 이미지 품질이 유지되므로 아이콘, 로고 등에 적합합니다.

```html
<canvas id="myCanvas" width="400" height="400"></canvas>
<script>
  const canvas = document.getElementById("myCanvas");
  const ctx = canvas.getContext("2d");

  let x = 0;
  const speed = 1;

  function drawParabola() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    ctx.beginPath();
    ctx.moveTo(0, canvas.height);

    for (let i = 0; i < canvas.width; i++) {
      const y = Math.pow(i - x, 2) * 0.01;
      ctx.lineTo(i, canvas.height - y);
    }

    ctx.strokeStyle = "blue";
    ctx.lineWidth = 2;
    ctx.stroke();
    ctx.closePath();

    x += speed;
    if (x > canvas.width) {
      x = 0;
    }

    requestAnimationFrame(drawParabola);
  }

  drawParabola();
</script>

<svg width="100" height="100">
  <circle
    cx="50"
    cy="50"
    r="40"
    stroke="green"
    stroke-width="4"
    fill="yellow"
  />
</svg>
```

### 위치정보 활용

HTML5의 `<geolocation>` API를 사용하면 사용자의 위치 정보를 가져올 수 있습니다. 이를 활용하여 위치 기반 서비스를 제공할 수 있습니다.

```javascript
if (navigator.geolocation) {
  navigator.geolocation.getCurrentPosition(showPosition);
} else {
  console.log("Geolocation is not supported by this browser.");
}

function showPosition(position) {
  console.log("Latitude: " + position.coords.latitude);
  console.log("Longitude: " + position.coords.longitude);
}
```

### 로컬 스토리지

HTML5의 localStorage 객체를 사용하면 클라이언트 측에 데이터를 저장할 수 있습니다. 이를 통해 웹 페이지를 새로고침해도 데이터가 유지됩니다.

```javascript
localStorage.setItem("key", "value");
var data = localStorage.getItem("key");
localStorage.removeItem("key");
```

### Custom Switches

체크박스를 사용하여 사용자 정의 스위치를 만들 수 있습니다. CSS와 함께 사용하면 보다 시각적으로 매력적인 스위치를 만들 수 있습니다.

```html
<label class="switch">
  <input type="checkbox" />
  <span class="slider"></span>
</label>
```

```css
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  transition: 0.4s;
  border-radius: 34px;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  transition: 0.4s;
  border-radius: 50%;
}

input:checked + .slider {
  background-color: #2196f3;
}

input:checked + .slider:before {
  transform: translateX(26px);
}
```

### Datalist

`<datalist>` 태그를 사용하면 입력 필드에 자동완성 기능을 추가할 수 있습니다. 사용자가 입력할 때 미리 정의된 옵션 중에서 선택할 수 있습니다.

```html
<label for="browser">Choose your browser from the list:</label>
<input list="browsers" name="browser" id="browser" />

<datalist id="browsers">
  <option value="Edge"></option>
  <option value="Firefox"></option>
  <option value="Chrome"></option>
  <option value="Opera"></option>
  <option value="Safari"></option>
</datalist>
```

### 색상 선택기

`<input type="color">`를 사용하면 색상 선택 인터페이스를 만들 수 있습니다. 사용자는 시각적으로 색상을 선택할 수 있습니다.

```html
<label for="favcolor">Select your favorite color:</label>
<input type="color" id="favcolor" name="favcolor" value="#ff0000" />
```

### 아코디언

`<details>`와 `<summary>` 태그를 사용하면 아코디언 UI를 만들 수 있습니다. 사용자는 `<summary>` 태그를 클릭하여 추가 정보를 확장하거나 축소할 수 있습니다.

```html
<details>
  <summary>Details</summary>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris vitae turpis
    vitae lacus faucibus efficitur.
  </p>
</details>
```

### 다이얼로그 모달

`<dialog>` 태그를 사용하면 모달 창을 만들 수 있습니다. 사용자는 모달 창을 통해 페이지와 상호작용할 수 있습니다.

```html
<dialog id="myDialog">
  <p>This is a dialog box.</p>
  <button id="closeDialog">Close</button>
</dialog>

<button id="openDialog">Open Dialog</button>

<script>
  var dialog = document.getElementById("myDialog");
  var openButton = document.getElementById("openDialog");
  var closeButton = document.getElementById("closeDialog");

  openButton.addEventListener("click", function () {
    dialog.showModal();
  });

  closeButton.addEventListener("click", function () {
    dialog.close();
  });
</script>
```

## 2. 멀티미디어

HTML5에서는 `<audio>`와 `<video>` 태그를 사용하여 멀티미디어 콘텐츠를 삽입할 수 있습니다.

### 오디오 삽입

`<audio>` 태그를 사용하면 오디오 파일을 웹 페이지에 삽입할 수 있습니다. `controls` 속성을 추가하면 재생 컨트롤이 표시됩니다.

```html
<audio src="audio.mp3" controls>
  Your browser does not support the audio element.
</audio>
```

### 비디오 삽입

`<video>` 태그를 사용하면 비디오 파일을 웹 페이지에 삽입할 수 있습니다. `width`와 `height` 속성을 사용하여 비디오의 크기를 조정할 수 있습니다.

```html
<video src="video.mp4" controls width="640" height="360">
  Your browser does not support the video element.
</video>
```

### 다양한 속성

`<audio>`와 `<video>` 태그에는 다음과 같은 속성을 사용할 수 있습니다.

- `autoplay`: 페이지가 로드될 때 자동으로 재생을 시작합니다.
- `loop`: 미디어 파일을 반복 재생합니다.
- `muted`: 오디오를 음소거합니다.

```html
<audio src="audio.mp3" autoplay loop muted>
  Your browser does not support the audio element.
</audio>

<video src="video.mp4" autoplay loop muted>
  Your browser does not support the video element.
</video>
```

## 3. 유효성 검사와 접근성

웹 페이지를 만들 때는 유효성 검사와 웹 접근성을 고려해야 합니다. 이를 통해 모든 사용자가 웹 페이지에 접근하고 사용할 수 있도록 합니다.

### W3C 마크업 유효성 검사

W3C에서 제공하는 마크업 유효성 검사 서비스를 사용하면 HTML 문서의 유효성을 검사할 수 있습니다. 유효한 HTML 문서는 브라우저 호환성을 높이고 오류를 줄일 수 있습니다.

### 웹 접근성의 개념과 중요성

웹 접근성은 장애인, 고령자 등 모든 사용자가 웹 콘텐츠에 접근하고 이용할 수 있도록 보장하는 것을 말합니다. 웹 접근성을 고려하여 웹 페이지를 제작하면 모든 사용자에게 평등한 기회를 제공할 수 있습니다.

### 적절한 대체 텍스트 제공

이미지에는 `alt` 속성을 사용하여 적절한 대체 텍스트를 제공해야 합니다. 대체 텍스트는 이미지를 볼 수 없는 사용자에게 이미지의 내용을 전달합니다.

```html
<img src="image.jpg" alt="대체 텍스트" />
```

### 키보드 내비게이션 지원

모든 사용자가 키보드만으로도 웹 페이지를 탐색할 수 있도록 해야 합니다. 탭 키를 사용하여 링크, 버튼, 폼 컨트롤 등을 이동할 수 있어야 하며, 포커스 표시가 명확해야 합니다.

```css
a:focus,
button:focus,
input:focus {
  outline: 2px solid blue;
}
```

## 4. 실습 프로젝트

### 간단한 게임 만들기

HTML5의 `<canvas>` 태그를 사용하여 간단한 게임을 만들어 보겠습니다. 이 게임은 캔버스 위에서 공을 움직이고 충돌 감지를 수행합니다.

```html
<canvas id="gameCanvas" width="400" height="400"></canvas>
<script>
  const canvas = document.getElementById("gameCanvas");
  const ctx = canvas.getContext("2d");
  let x = canvas.width / 2;
  let y = canvas.height - 30;
  let dx = 2;
  let dy = -2;
  const ballRadius = 10;

  function drawBall() {
    ctx.beginPath();
    ctx.arc(x, y, ballRadius, 0, Math.PI * 2);
    ctx.fillStyle = "#0095DD";
    ctx.fill();
    ctx.closePath();
  }

  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    drawBall();
    x += dx;
    y += dy;

    if (x + dx > canvas.width - ballRadius || x + dx < ballRadius) {
      dx = -dx;
    }
    if (y + dy > canvas.height - ballRadius || y + dy < ballRadius) {
      dy = -dy;
    }
  }

  setInterval(draw, 10);
</script>
```

위 코드는 캔버스 위에서 공을 그리고 움직입니다. 공이 캔버스의 경계에 부딪히면 반대 방향으로 이동합니다.

### 대화형 웹 페이지 만들기

HTML5의 `<dialog>` 태그와 `<geolocation>` API를 사용하여 대화형 웹 페이지를 만들어 보겠습니다. 이 페이지는 사용자의 위치 정보를 가져와 모달 창에 표시합니다.

```html
<button id="openDialog">위치 정보 보기</button>

<dialog id="myDialog">
  <p>현재 위치:</p>
  <p id="location"></p>
  <button id="closeDialog">닫기</button>
</dialog>

<script>
  const dialog = document.getElementById("myDialog");
  const openButton = document.getElementById("openDialog");
  const closeButton = document.getElementById("closeDialog");
  const locationElement = document.getElementById("location");

  openButton.addEventListener("click", function () {
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(showPosition);
    } else {
      locationElement.textContent =
        "Geolocation을 지원하지 않는 브라우저입니다.";
    }
    dialog.showModal();
  });

  closeButton.addEventListener("click", function () {
    dialog.close();
  });

  function showPosition(position) {
    locationElement.textContent = `위도: ${position.coords.latitude}, 경도: ${position.coords.longitude}`;
  }
</script>
```

위 코드는 "위치 정보 보기" 버튼을 클릭하면 `<geolocation>` API를 사용하여 사용자의 위치 정보를 가져옵니다. 그리고 `<dialog>` 태그를 사용하여 모달 창을 열고 위치 정보를 표시합니다. "닫기" 버튼을 클릭하면 모달 창이 닫힙니다.

이렇게 HTML5의 새로운 기능을 활용하여 보다 풍부하고 대화형 웹 페이지를 만들 수 있습니다. `<canvas>`로 그래픽과 애니메이션을 구현하고, `<geolocation>`으로 위치 정보를 활용하며, `<dialog>`로 모달 창을 만드는 등 다양한 기능을 조합하여 사용자 경험을 향상시킬 수 있습니다.

## 마치며

이 글에서는 HTML5의 새로운 기능, 멀티미디어, 유효성 검사와 접근성에 대해 알아보았습니다. 또한 실습 프로젝트로 간단한 게임과 대화형 웹 페이지를 만들어 보았습니다.

HTML5는 웹 개발자에게 많은 가능성을 제공합니다. 그래픽, 위치 정보, 로컬 스토리지, 멀티미디어 등 다양한 기능을 활용하여 보다 향상된 사용자 경험을 제공할 수 있습니다. 또한 웹 접근성을 고려하여 모든 사용자가 웹 페이지에 접근하고 사용할 수 있도록 해야 합니다.

이제 여러분은 HTML5의 새로운 기능과 웹 접근성에 대한 이해를 바탕으로 보다 풍부하고 대화형 웹 페이지를 만들 준비가 되었습니다. 실습 프로젝트를 통해 배운 내용을 활용하여 창의적이고 혁신적인 웹 페이지를 만들어 보세요.
