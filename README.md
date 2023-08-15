<!-- Improved compatibility of back to top link -->
<a name="top"></a>

<!-- PROJECT SHIELDS -->
[![MIT License][license-shield]][license]

<!-- PROJECT LOGO -->
<div align="center">
<h3 align="center">Ainalyst</h3>

  <p align="center">
    Context analysis system for stock firm reports
    <br />
    <a href="https://github.com/minocrafft/Ainalyst/tree/main/RELEASE.md"><strong>Explore the release notes »</strong></a>
    <br />
    <br />
    <a href="https://github.com/minocrafft/Ainalyst">Home</a>
    ·
    <a href="https://github.com/minocrafft/Ainalyst/issues">Issues</a>
    ·
    <a href="https://github.com/minocrafft/Ainalyst/pulls">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-the-project">About The Project</a></li>
    <li><a href="#getting-started">Getting Started</a></li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

Here is the [video](https://www.youtube.com/watch?v=EeRVhKxHqs8&ab_channel=%EB%A8%B8%EB%8B%88%EA%B7%B8%EB%9D%BC%ED%94%BCMoneygraphy) that inspired this project.

<div>
    <div align="left">
        <img src="https://github.com/minocrafft/Ainalyst/assets/title.png" alt="title">
    </div>
    <div align="right">
        <img src="https://github.com/minocrafft/Ainalyst/assets/home.png" alt="title">
    </div>
</div>

애널리스트가 작성한 증권사 리포트의 맥락을 분석해서 새로운 투자의견을 도출하는 인공지능 시스템을 구현합니다.  
Main contents는 다음과 같습니다.

* 경제, 금융 관련 리포트의 맥락 및 의도를 분석하는 Bert 기반의 Deep Learning Model 개발
* 맥락 분석 모델의 성능 향상을 위한 다양한 기법 적용
* 리포트 데이터 저장을 위한 데이터베이스 구축
* 시각화 및 전체 파이프라인 자동화

### Environments

|Types|Contents|
|---|---|
|OS|Ubuntu|
|Languages|Python|
|Databases|PostgreSQL|
|Frameworks|Numpy, Pandas, Scikit-learn, datasets <br>Pytorch, huggingface, transformers <br>Django|

<p align="right">(<a href="#top">back to top</a>)</p>



## Details

### Flowchart
![flowchart]

전체 흐름은 다음과 같습니다.

- 여러 증권사 리포트를 제공해주는 사이트를 통해 리포트 데이터를 스크래핑합니다.
- 수집된 리포트 데이터를 전처리를 통해 모델이 입력받을 수 있는 텍스트 형태로 변환하고 DB에 적재합니다.
- 변환된 데이터를 학습 및 검증 세트로 나누어 모델을 학습합니다.
- 학습된 모델을 통해 새롭게 작성되는 리포트에 대해 매수/매도 의견을 추론하고 웹페이지에 시각화합니다.

### Distributions of Data

학습에 사용된 데이터의 분포는 다음과 같습니다.

|Opinions|Number|
|---|---|
|강력 매수|약 1600개|
|매도|약 280개|
|중립 & 목표주가 하향|약 830개|
|계|약 2700개|


### Data augmentations

부족한 리포트 데이터의 증강을 위해 다음과 같은 방법을 적용했습니다.

1. Apply different way for preprocessing
    - 전처리를 최소화한 Raw data와 추가 전처리가 들어간 data를 별도의 데이터로 활용
    - Domain adaptation 진행 후 학습
2. Apply back translations
    - kakaobrain, pororo api, google translation 등을 활용해 다른 언어로 번역 후 한글로 재 번역 합니다.
    - kor :arrow_right: eng :arrow_right: kor, kor :arrow_right: zhcn :arrow_right: kor
    ![backtranslations]

결과적으로 기존 2,700개의 데이터셋을 약 4배 정도 증강했습니다.

### Models

KB에서 제공받은 KB-ALBERT, KoBERT, RoBERTa 등을 학습하며 최종적으로 성능이 좋은 KB-ALBERT 모델을 채택했으며 학습별 variation은 다음과 같습니다.

![performance-table]

### Web Server & Databases

Display를 위한 Web 및 리포트 데이터 저장을 위해 Django와 PostgreSQL을 사용합니다.


<!-- USAGE EXAMPLES -->
## Usage

Sadly, this project will not be updated...  
Official updates are no longer supported.

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## References

* for web: [Argon Dashboard Django][Argon]

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[license-shield]: https://img.shields.io/github/license/minocrafft/Ainalyst.svg?style=for-the-badge
[license]: LICENSE
[title]: assets/title.png
[home]: assets/home.png
[flowchart]: assets/flowchart.png
[blockdiagram]: assets/blockdiagram.png
[backtranslations]: assets/backtranslations.png
[performance-table]: assets/performance-table.png
[Argon]: https://www.creative-tim.com/product/argon-dashboard-django
[Release-Notes]: RELEASE.md
