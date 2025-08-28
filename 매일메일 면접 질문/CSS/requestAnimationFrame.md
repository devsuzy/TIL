# requestAnimationFrame

> 유튜브 1분코딩 - requestAnimationFrame 사용법

### window.requestAnimationFrame()
- 브라우저에게 수행하기 원하는 애니메이션을 알리고, 다음 리페인트가 진행되기 전에 해당 애니메이션을 업데이트 하는 함수를 호출
- 애니메이션 최적화 기법
- 1초당 60회를 목표로 요청
- 이전에 `setInterval()`로 했던 방식의 단점을 극복

### 사용 예시

```html
<body>
    <img class="image" src="image.png" alt="image" />
    <div class="value">requestAnimationFrame</div>

    <script>
        const img = document.querySelector(".image");
        const value = document.querySelector(".value");
        let yPos = 0;
        let rafId;

        function render() {
            img.style.transform = `translateY(${-yPos})`;
            yPos += 10;

            // 애니메이션 실행
            rafId = requestAnimationFrame(render);

            // 애니메이션 중지 2
            if (rafId >= 500) {
              cancelAnimationFrame(rafId);  
            }
        }
        render();

        // 애니메이션 중지 2
        window.addEventListener('click', () => {
            cancelAnimationFrame(rafId);
        })
    </script>
</body>
```