## ๐ฌ React 18์ ํต์ฌ ๋ณ๊ฒฝ์ 

1. ์๋ ๋ฐฐ์น(Automatic Batching)
2. ๋์์ฑ(Concurrent) ๊ธฐ๋ฅ
   : startTransition์ด๋ ์ ํ์ (Selective) Hydration ๋ฑ์ ๋์์ฑ(Concurrent)๊ธฐ๋ฅ์ด ์ถ๊ฐ๋์์ต๋๋ค.
3. ์์คํ์ค(Suspense)๋ฅผ ์ง์ํ๋ ์๋ก์ด ์๋ฒ์ฌ์ด๋ ๋ ๋๋ง ์ํคํ์ฒ
   : ์๋ก์ด ์๋ฒ ์ฌ์ด๋ ๋ ๋๋ง ์ํคํ์ฒ๊ฐ ๋์๋์์ต๋๋ค. ์ด ์ํคํ์ฒ์์๋ <Suspense>์ React.lazy๋ฅผ ์ง์ํ๋ฉฐ, ๊ธฐ์กด ์๋ฒ์ฌ์ด๋ ๋ ๋๋ง์ ๊ทผ๋ณธ์ ์ธ ๋ฌธ์ ๋ฅผ ํด๊ฒฐํ์ต๋๋ค.
4. ReactDOM.render()๊ฐ Deprecated๋๊ณ  ์๋กญ๊ฒ ReactDom.createRoot() API๊ฐ ๊ทธ ์๋ฆฌ๋ฅผ ์ด์ด๊ฐ๋๋ค.

<br>
<br>


- ์ฐธ๊ณ  ๋งํฌ

https://kormelon.com/post/14/React(%EB%A6%AC%EC%95%A1%ED%8A%B8)%2018%EB%B2%84%EC%A0%84%20%EC%97%85%EB%8D%B0%EC%9D%B4%ED%8A%B8%20%EC%A0%95%EB%A6%AC
