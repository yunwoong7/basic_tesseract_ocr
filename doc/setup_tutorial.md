<h2 align="center">
OCR 개발환경 구성
</h2>

### **1. Tesserct Engine 설치**

#### **1) macOS에 Tesseract 설치**

[Homebrew](https://brew.sh/) 패키지 관리자 를 사용하면 macOS에 Tesseract OCR 엔진을 설치하는 것이 매우 간단합니다 . Homebrew가 아직 설치되어 있지 않다면 위의 링크를 사용하여 시스템에 Homebrew를 설치하시기 바랍니다.

```
$ brew install tesseract
```

#### **2) Ubuntu에 Tesseract 설치**

Ubuntu 18.04에 Tesseract를 설치하는 것은 간단합니다. apt-get 패키지 관리자는 Tesseract에 필요한 필수 라이브러리 또는 패키지를 자동으로 설치합니다.

```
$ sudo apt install tesseract-ocr
```

#### **3) Windows에 Tesseract 설치**

a) Windows용 Tesseract 설치 프로그램을 [사이트](https://github.com/UB-Mannheim/tesseract/wiki)로 이동하여 다운로드합니다.

![img](https://blog.kakaocdn.net/dn/5laOo/btrnN1hiIsq/LAbbs4toWwuf5UDTPU0yo1/img.png)

b) 설치파일을 실행 합니다.

![img](https://blog.kakaocdn.net/dn/di4fyE/btrnLIbe3Z0/tN0TktKk2mx7ytMj7Av6lk/img.png)

![img](https://blog.kakaocdn.net/dn/p8dlj/btrnCQ2yOgH/qzQaDg0eBawHcqZD3R7RGK/img.png)

c) 한국어를 추가합니다.

![img](https://blog.kakaocdn.net/dn/dx63Dm/btrnBzULJ6M/ks8G3Zxv2Ne1hM9ueMHkok/img.png)

d) 설치 경로의 경우 Python의 가상환경이 존재하는 드라이브로 설치하는 것을 권장합니다. (다른 드라이브에 존재하는 경우 ucrtbase.DLL 모듈 오류가 발생 할 수 있습니다.)

![img](https://blog.kakaocdn.net/dn/bBKe6A/btrnGk3hmYK/U8KQCeT7BNW8Gib4gIR60K/img.png)

![img](https://blog.kakaocdn.net/dn/bJWknl/btrnEJIGVJl/vsZ9IT4RNdFZQXLeslQmO1/img.png)

5.0 이전에는 환경변수에 Path를 추가하는 옵션이 있었는데, 자동으로 추가 할 경우 일부 문제가 있어서 5.0부터는 없어졌습니다. 수동으로 추가가 필요합니다. Python에서 직접 경로를 입력하여 호출 할 거라면 Path를 추가하지 않으셔도 됩니다.

![img](https://blog.kakaocdn.net/dn/bLYqZA/btrnCPCDeZd/hmYNTthkieR91xd4AWXyy1/img.png)

### **2. OpenCV와 PyTesseract 설치**

PyTesseract 설치 전에 안정적인 개발환경을 위해서 OCR을 위한 [Python 가상환경](https://yunwoong.tistory.com/3?category=839341)을 만들고 진행 하시기를 권장합니다.

```
(ocr_env) pip install numpy opencv-contrib-python (ocr_env) pip install pytesseract
```

------

이제 컴퓨터에 Tesseract OCR 엔진 설치가 완료되었고, 또한 OCR, 컴퓨터 비전 및 이미지 처리를 수행하는 데 필요한 필수 Python 패키지를 설치가 완료되었습니다.

### **3. Trained Data Download**

| **Trained models**                                           | **Speed**                                                    | **Accuracy**              | **Supports legacy**                       | **Retrainable** |      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------- | ----------------------------------------- | --------------- | ---- |
| [tessdata](https://github.com/tesseract-ocr/tessdata)        | Legacy + LSTM (integerized tessdata-best)                    | Faster than tessdata-best | Slightly less accurate than tessdata-best | Yes             | No   |
| [tessdata-best](https://github.com/tesseract-ocr/tessdata_best) | LSTM only (based on [langdata](https://github.com/tesseract-ocr/langdata)) | Slowest                   | Most accurate                             | No              | Yes  |
| [tessdata-fast](https://github.com/tesseract-ocr/tessdata_fast) | Integerized LSTM of a smaller network than tessdata-best     | Fastest                   | Least accurate                            | No              | No   |