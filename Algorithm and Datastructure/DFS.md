```ts
function factorial(n: number) {
	if (n === 0) return 1;
	
	return n * factorial(n - 1)
}
```