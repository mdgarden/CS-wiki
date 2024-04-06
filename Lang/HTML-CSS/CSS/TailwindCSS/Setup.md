- **패키지 json에 tailwind,postcss 등등 추가**
`$ npm install -D tailwindcss postcss autoprefixer`

- **tailwind init**
`$ npx tailwindcss init -p`

- **tailwind.config.js에서 tailwind를 사용할 파일 설정**

```jsx
module.exports = {

	content: [
		// 예시
		"./pages/**/*.{js,jsx,ts,tsx}",
		"./components/**/*.{js,jsx,ts,tsx}",
	],

	theme: {
		extend: {},
	},
	plugins: [require("@tailwindcss/forms")],
};
```

> [!warning] 
> node_modules내부도 스캔하므로 전체 추가는 피할 것
> https://tailwindcss.com/docs/content-configuration#pattern-recommendations

> [!note]
> content안의 확장자명 사이에는 띄어쓰기를 넣지 않는다.

- globals.css 내용 삭제 후 수정
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```