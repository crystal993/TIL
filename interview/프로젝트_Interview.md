### ๐ฌ Debounce ์ Throttle ์ฐจ์ด์ 

<br>

๋๋ฐ์ด์ฑ์ ์ผ์  ์๊ฐ ๋ด์ ์์ฒญ์ด ๋ค์ด์ค๋๋๋ก ๋ฐ์์ฃผ์ง๋ง ๊ฒฐ๊ตญ ์คํํ๋ ๊ฑด ๊ฐ์ฅ ๋ง์ง๋ง ์์ฒญ์ด๊ณ , ์ฐ๋กํ๋ง์ ์ผ์  ์๊ฐ ๋ด์ ์์ฒญ์ ํ๋ฒ์ ํ๋๋ง ๋ค์ด์ค๋ค. ์ต์ด ์์ฒญ์ ์ํํ๋ ๋์ ๋ค๋ฅธ ์์ฒญ์ ๋ฐ์ ๋ค์ด์ง ์๋๋ค.
๋๋ ๋๋ฐ์ด์ฑ ๊ฒ์์ด api ํธ์ถ, ์ฐ๋ฒํผ ์ด๋ทฐ์ง์ ์ฌ์ฉํจ.
์ฐ๋กํ๋ง์ ์ฃผ๋ก ์คํฌ๋กค ์ด๋ฒคํธ์ ๋ง์ด ์ฌ์ฉํจ.

<br><br>

### useDebounce hook

useEffect๋ ์ปดํฌ๋ํธ๊ฐ ๋ ๋๋ง ๋  ๋ ์คํ๋๋ ํจ์์๋๋ค. ๋ฐ๋ผ์ useEffect ๋ด๋ถ์ ์ฝ๋๋ ์ปดํฌ๋ํธ๊ฐ ๋ ๋๋ง ๋  ๋ ๋ง๋ค ์คํ๋๋ค๊ณ  ์๊ฐํ์๋ฉด ๋ฉ๋๋ค. ์์ ์ฝ๋์์๋ setTimeout์ ์ฌ์ฉํ์ฌ ํน์  ์๊ฐ์ด ์ง๋ ํ ์ ๋ฌ ๋ฐ์ value์ ๊ฐ์ ๋ณ๊ฒฝํ๋ ๊ฒ์ ์ ์ ์์ต๋๋ค.

<br>

useEffect ๋ด๋ถ์์ return์ ํ๊ฒ ๋๋ฉด ์ปดํฌ๋ํธ๊ฐ ์ ๊ฑฐ ๋  ๋ ํด๋น ์ฝ๋๋ค์ด ์คํ๋ฉ๋๋ค. ์์ ์ฝ๋์์๋ ์ปดํฌ๋ํธ๊ฐ ์ ๊ฑฐ ๋  ๋ clearTimeout์ ํ์ฉํ์ฌ setTimeout์ ์๊ฐ์ ์ด๊ธฐํ ์ํต๋๋ค.

<br>

useEffect์ ๋ ๋ฒ์งธ ์ธ์๋ก ๋ฐฐ์ด์ ์ ๋ฌํ๊ฒ ๋๋ฉด ๋ฐฐ์ด์ ํฌํจ๋ ๊ฐ์ด ๋ณํ  ๋๋ง useEffect๋ฅผ ํธ์ถํ๊ฒ ๋ฉ๋๋ค. ์์์๋ value๊ฐ์ด ๋ณํ  ๋๋ง useEffect๋ฅผ ํธ์ถํ๊ฒ ๋  ๊ฒ์๋๋ค.

<br>

โญโญ 0.5์ด ์์ ๋ค๋ฅธ ์ด๋ฒคํธ๊ฐ ๋ฐ์ํ์ง ์๋๋ค๋ฉด setDebouncedValue๊ฐ ์คํ๋์ด ๋ฐ๋ ๊ฐ์ด return ๋๊ณ  ๋ค๋ฅธ ์ด๋ฒคํธ๊ฐ ๋ฐ์ํ๋ฉด ๊ธฐ์กด ๊ฐ์ด ๊ทธ๋๋ก return ๋ฉ๋๋ค.

<br><br>

### ํด๋ผ์ฐ๋ ํ๋ก ํธ

CloudFront๋ AWS์์ ์ ๊ณตํ๋ CDN ์๋น์ค ์๋๋ค. ๋ฉ๋ฅ๋ง์ผ์ด๋ผ๋ ํ๋ก์ ํธ๋ฅผ ์งํํ  ๋ ์ ์ ์ ํ์ฌ ์์น๋ฅผ ๋ฐ์์ค๊ธฐ ์ํด์๋ HTTPS๋ฅผ ์ฌ์ฉํด์ผ๋ง ํ์ต๋๋ค. S3๋ HTTP๋ง ์ง์์ด ๋๋ ๋ฐ๋ฉด์ cloud front๋SSL์ธ์ฆ์๋ฅผ ๋ฐ๊ธ๋ฐ์ผ๋ฉด HTTPS๋ก ๋ฆฌ๋ค์ด๋ ํธ๊ฐ ๊ฐ๋ฅํ๋ค๋ ์ฅ์ ์ด ์์์ต๋๋ค. ๊ทธ๋ฆฌ๊ณ  CDN์ ํตํ ํ์ด์ง ์๋ต ์๋๊ฐ ๋น ๋ฅด๊ธฐ ๋๋ฌธ์ ์ฌ์ฉํ๊ฒ ๋์์ต๋๋ค.

โญ ํด๋ผ์ฐ๋ ํ๋ก ํธ๋ ์งง์ ์ง์ฐ์๊ฐ๊ณผ ๋น ๋ฅธ ์ ์ก ์๋๋ก
๋ฐ์ดํฐ, ๋์์, ์ ํ๋ฆฌ์ผ์ด์ ๋ฐ API๋ฅผ
์ ์ธ๊ณ ๊ณ ๊ฐ์๊ฒ ์์ ํ๊ฒ ์ ์กํ๋
๊ณ ์ ์ฝํ์ธ  ์ ์ก ๋คํธ์ํฌ ์๋น์ค์ด๋ค.

<br>

โญ ์ฝํ์ธ ๋ฅผ ์ ๊ณตํ๋ ์๋ฒ์
์ค์  ์์ฒญ ์ง์ ๊ฐ์ ๊ฑฐ๋ฆฌ๊ฐ ๋งค์ฐ ๋จผ ๊ฒฝ์ฐ,
ํต์  ํ๊ฒฝ์ด ์ ์ข์ ๊ฒฝ์ฐ

<br>

โญ cloud front ์๋น์ค๋
์ฃ์ง ๋ก์ผ์ด์(์ปจํ์ธ ๊ฐ ์บ์ฑ๋๊ณ  ์ ์ ์๊ฒ ์ ๊ณต๋๋ ์์ )์ ํตํด ์ฝํ์ธ ๋ฅผ ์ ๊ณตํ๋ค.

<br><br>

### ์ํ ๋ฏน ๋์์ธ ํจํด์ ์ฅ๋จ์ 

    ๊ฐ์ฅ ์์ ์ปดํฌ๋ํธ ๋จ์๋ฅผ ์์๋ก ์ค์ ํ๊ณ  ๋จ๊ณ๋ณ๋ก ์ถ์์ ์ธ ๊ฒ์์ ๊ตฌ์ฒดํํ๋ ๋จ๊ณ๋ฅผ ๊ฐ์ง๋ค. ์ด ๊ณผ์ ์ ํตํด ํ์ฅํ๋ฉด์ ์ต์ข ์ฝํ์ธ ๋ฅผ ๋ณด์ฌ์ค ์ ์๋ค.
    ์์(atom) -> ๋ถ์(molecule) -> ์ ๊ธฐ์ฒด(organism) -> ํํ๋ฆฟ(template) -> ํ์ด์ง(page)

<br>

    (1) ์ฅ์ 
    - ๋์์ธ ์์คํ ๊ตฌ์ฑ์ ์์ด์ ๊ฐ์ด๋๋ผ์ธ์ผ๋ก ํ์ฉํ  ์ ์๋ค.
    - ์ ํ๋ฆฌ์ผ์ด์๊ณผ ๋ถ๋ฆฌํ์ฌ ์ปดํฌ๋ํธ๋ฅผ ๊ฐ๋ฐํ๊ณ  ํ์คํธํ  ์์๊ณ 
    ์คํ์ผ ๊ฐ์ด๋์ ๊ฐ์ ๋๊ตฌ์์ ๋ณผ ์์๋ค.
    - ์ปดํฌ๋ํธ ์ฌ์ฌ์ฉ์ฑ์ด ๊ทน๋ํ๋๋ค.

<br>

    (2) ๋จ์  - ์์กด์ฑ์ด ๋ณต์กํ๋ค.

<br><br>

### ๐ฌ CSS in JS(styled component)์ ์ฅ๋จ์ ์ ๋ํด์ ์ค๋ชํ์ธ์.

<br>

#### - ์ฅ์ 

- class ๋ช์ด ๋น๋์ ์ ๋ํฌํ ํด์๊ฐ์ผ๋ก ๋ณ๊ฒฝ๋๊ธฐ ๋๋ฌธ์ ๊ธฐ์กด์ ๋ณต์กํ class ๋ช๋ช ๊ท์น์ ํด๊ฒฐํด์ค๋๋ค.
- ์ปดํฌ๋ํธ ๋จ์๋ก ์ถ์ํ๋๊ธฐ ๋๋ฌธ์ css ํ์ผ ๊ฐ์ ์์กด์ฑ์ ์ ๊ฒฝ์ฐ์ง ์์๋ ๋ฉ๋๋ค.
- ์ปดํฌ๋ํธ์ css๊ฐ ๋์ผํ ๊ตฌ์กฐ๋ก ๊ด๋ฆฌ๋๊ธฐ ๋๋ฌธ์ ๋ถํ์ํด์ง css๋ฅผ ๊ด๋ฆฌํ๊ธฐ ์ํด์ ๋ณ๋์ ๋ฆฌ์์ค๋ฅผ ํฌ์ํ  ํ์๊ฐ ์์ต๋๋ค.
- css ์ปดํฌ๋ํธ ์ค์ฝํ์์๋ง ์ ์ฉ๋๊ธฐ ๋๋ฌธ์ ์ฐ์ ์์ ๋ฌธ์ ๊ฐ ๋ฐ์ํ์ง ์์ต๋๋ค.

<br>

#### - ๋จ์ 

- ๋ฒ๋ค์ ํฌ๊ธฐ๊ฐ ์ปค์ง๋ค๋ ๋จ์ ์ด ์์ต๋๋ค. CSS in JS๋ฅผ ์ฌ์ฉํ๊ธฐ ์ํด์๋ ์ฌ๋ฌ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ฌ์ฉํ๋๋ฐ ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ถ๊ฐ๋ ๊ณง ๋ฒ๋ค ์ฌ์ด์ฆ๊ฐ ์ฆ๊ฐํจ์ ์๋ฏธํฉ๋๋ค.
- ๋ฒ๋ค ์ฌ์ด์ฆ๊ฐ ์ปค์ง๊ฒ ๋๋ฉด ๋ค์ด๋ก๋ ์๊ฐ๋ ์ค๋ ๊ฑธ๋ฆฌ๊ธฐ ๋๋ฌธ์ ์ฌ์ฉ์ ๊ฒฝํ์ ์น๋ช์ ์ด๊ฒ ๋ฉ๋๋ค.
- CSS in JS๋ ์๋ฐ์คํฌ๋ฆฝํธ๊ฐ ๋ชจ๋ ๋ก๋ฉ๋ ํ css ์ฝ๋๊ฐ ์์ฑ๋๊ธฐ ๋๋ฌธ์ ๋ ๋๋ ค์ง๋๋ค.

๋๊ฐ ์์ฑ๋๊ธฐ ๋๋ฌธ์ ๋ ๋๋ ค์ง๋๋ค.

<br><br>

### Css-in-js : ์๋ฐ์คํฌ๋ฆฝํธ ์ฝ๋์์ css๋ฅผ ์์ฑํ๋ ๋ฐฉ์์ ์๋ฏธ

(1) ์ฅ์ 

โญ js ์ css ์ฌ์ด์ ์์๋ ํจ์ ์ํ ๊ณต์  ๊ฐ๋ฅ!!!
โญ css ๊ฐ์ ์์กด๊ด๊ณ๋ฅผ ๊ด๋ฆฌ
โญ ํด๋์ค ์ด๋ฆ ์์ฑ ์ํด๋๋จ!! => ์ ๋ํฌํ ํด์๊ฐ์ผ๋ก ๋ณํ
ํ
โญ css ๋ชจ๋ธ์ ๋ฌธ์๋ ๋ฒจ์ด ์๋ ์ปดํฌ๋ํธ ๋ ๋ฒจ๋ก ์ถ์ํ

<br>

(2) ๋จ์ 
โญ ๋ฌ๋์ปค๋ธ
โญ ๋ณ๋์ ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ค์น
โญ ๋ฒ๋ค ํฌ๊ธฐ ์ฆ๋ -> ํผํฌ๋จผ์ค๊ฐ ๋๋ฆผ.

์ฌ์ฉ์ ๊ฒฝํ์ด ๋ ์ค์ํ  ๊ฒฝ์ฐโฆ

๋ค๋ง ๋ณธ์ธ์ ๊ฒฝํ์ ๋น์ถ์ด ๋ดค์ ๋ ์์์์ ์ฑํฅ์ด๋ ํ๋จ์ด ํ์ํ ๋ถ๋ถ์ด๋ ๊ฐ๋ฐ ํจ์จ์ฑ์ ์ค์ ์ ๋ ์ปดํฌ๋ํธ ์์ฃผ์ ํ๋ก์ ํธ๋ผ๋ฉด CSS-in-JS๋ฅผ ๊ณ ๋ คํ๋ ๊ฒ์ด ์ข๋ค. ํ์ํ ์ปดํฌ๋ํธ ํ์ด์ง์ CSS ์คํ์ผ ์์๋ง ๋ก๋ฉํ๊ธฐ ๋๋ฌธ์ด๋ค. ๋ฐ๋ฉด ์ฌ์ฉ์ ํธ์์ ๋ฐฉ์ ์ ๋ ์ธํฐ๋ ํฐ๋ธํ ์น ํ๋ก์ ํธ๋ผ๋ฉด ๋๋๋ง ์ ๋ชจ๋  CSS ์คํ์ผ ์์๋ฅผ ๋ก๋ฉํ๋ CSS-in-CSS ๋ฐฉ์์ ๊ถ์ฅํ๋ ๋ฐ์ด๋ค.

<br><br>

### ๋ฆฌ๋์ค๋ฅผ ์ฌ์ฉํ ์ด์ ??

    1. Context API๋ฅผ ์ฌ์ฉํด์ ์ํ ๊ด๋ฆฌ๋ฅผ ํ๋ฉด ๋ถ๋ถ์ ์ธ ์ํ ๋ณ๊ฒฝ์ด ์ด๋ ค์์ง๋ค.
    ๋ณ๋์ Provider๋ฅผ ์ด์ฉํ์ฌ ๋ ๋๋ง์ ์ ์ดํ๋ ค๊ณ  ํด๋ ์์ ์์๋ค ์ ์ฒด๊ฐ ๋ค์ ๋ ๋๋ง ํด์ผํ๋ ๋ฌธ์ ๊ฐ ์๊ธด๋ค.
    - ์ปดํฌ๋ํธ ์ํ๋ฅผ ๊ณตํต๋ ์์ ์ปดํฌ๋ํธ๊น์ง ๋์ด์ฌ๋ ค ๊ณต์ ํ  ์ ์์ง๋ง
    ์ด ๊ณผ์ ์์ ๊ฑฐ๋ํ ํธ๋ฆฌ๊ฐ ๋ฆฌ๋ ๋๋ง ๋๊ธฐ๋ ํ๋ค.

<br>

    2. ๋ฆฌ๋์ค ํดํท
    ๋ฆฌ๋์ค๋ณด๋ค ๋ณด์ผ๋ฌํ๋ ์ดํธ๋ฅผ ์ค์ฌ์ค๋ค.

    Redux๋ Flux ์ํคํ์ฒ ๊ธฐ๋ฐ(๋ฐ์ดํฐ ํ๋ฆ์ด ๋จ๋ฐฉํฅ )

<br>

    3. ๋ฆฌ์ฝ์ผ
    โญ ๋ฆฌ์ฝ์ผ์ es5 ๋ฌธ๋ฒ์ผ๋ก ๋ณํ๋์ง ์๋ค๋ ๋จ์ ์ด ์๊ธฐ ๋๋ฌธ์
    ์ฌ์ฉ x,

    ์ํ ๋ฐ์ดํฐ๊ฐ atoms -> selectors -> ์ปดํฌ๋ํธ ์์๋ก ํ๋ฅด๋ ๊ฒ์ ๋งํ๋ค.

<br>

    1. Recoil์ Atomic ๋ชจ๋ธ ๊ธฐ๋ฐ(Atom -> selector๋ฅผ ๊ฑฐ์ณ ์ปดํฌ๋ํธ๋ก ์ ๋ฌ๋๋ ํ๋์ data-flow๋ฅผ ๊ฐ์ง๊ณ  ์์ด, ๋ณต์กํ์ง ์์ ์ํ ๊ตฌ์กฐ๋ฅผ ๊ฐ์ง๊ณ  ์๋ค.)

<br>

    2. Atom -> selector๋ฅผ ๊ฑฐ์ณ ์ปดํฌ๋ํธ๋ก ์ ๋ฌ๋๋ ํ๋์ data-flow๋ฅผ ๊ฐ์ง๊ณ  ์๊ธฐ ๋๋ฌธ์
    ๋ณต์กํ์ง ์์ ์ํ๊ตฌ์กฐ๋ฅผ ๊ฐ์ง๊ณ  ์๋ค.

<br>

    3. Atom๊ณผ selector๋ง ์๊ณ ๋ ์ด๋ ์ ๋ ๊ตฌํ์ด ๊ฐ๋ฅํ๊ธฐ ๋๋ฌธ์ ๋ฌ๋์ปค๋ธ๊ฐ ๋น๊ต์  ๋ฎ๋ค.

<br>

    4. Store์ ๊ฐ์ ์ธ๋ถ ์์ธ์ด ์๋ React ๋ด๋ถ์ ์ํ๋ฅผ ํ์ฉํ๊ณ 
    Context API๋ฅผ ํตํด ๊ตฌํ๋์ด ์๊ธฐ ๋๋ฌธ์ ๋ ๋ฆฌ์กํธ์ ๊ฐ๊น์ด ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ด๋ค.

<br><br>

### Intersection Observer API

    - intersection Observer API๋ target๊ณผ root์ ๊ต์ฐจ ๋ฐ์์ ๋น๋๊ธฐ์ ์ผ๋ก ๊ด์ฐฐํ๋ web API์๋๋ค.

    - ๋ฉ์ธ thread์ ์ํฅ์ ์ฃผ์ง ์๊ณ , Callback์ ์คํํ๊ธฐ์ ๋งค๋ฒ layout์ ์๋ก ๊ทธ๋ ค render tree๋ฅผ ์๋ก ๋ง๋ค์ง ์๊ธฐ ๋๋ฌธ์ ๋ธ๋ผ์ฐ์ ์ ์ฑ๋ฅ์ ํฅ์์ํฌ ์ ์์ต๋๋ค.

    - ์ฃผ๋ก ๋ฌดํ ์คํฌ๋กค์ ๊ตฌํํ  ๋ ์์ฃผ ์ฌ์ฉ๋๋ api์๋๋ค.

<br><br>

### useReducer , useState

    - useState๋ ์ปดํฌ๋ํธ ๋ด๋ถ์์  state๋ฅผ ๋ณ๊ฒฝํ๋ ๊ฒ์ด ๊ฐ๋ฅ
    - useReducer๋ ์ปดํฌ๋ํธ ์ธ๋ถ์์ state๋ฅผ ๋ณ๊ฒฝํ๋ ๊ฒ์ด ๊ฐ๋ฅํ๋ค.

<br><br>
