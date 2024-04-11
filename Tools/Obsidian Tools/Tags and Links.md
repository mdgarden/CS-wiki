## Links
### Internal Link
[[Callouts]]
### External Link

### Embed files
##### 기본적인 사용방법
노트를 임베딩 하기 위해서는 `![[내부링크]]`로 작성 가능함 (이미지를 넣는 것과 같은 원리)

>[!example]
>![[Artifact]]
##### 노트 안에 있는 리스트 임베딩하기(block identifier)사용

```
- list itme 1
- list item2

^my-list-id
```

`![[노트이름#^my-list-id]]`

>[!example]
>![[License#MIT 라이센스]]


### Add and alias to a note
노트 Properties에 `aliases` property를 추가해야함
별칭은 항상 YAML의 리스트 형태로 작성되어야함.

```yaml
---
aliases:
	- Doggo
	- Woofer
	- Yapper
---
```

>[!example]
> [[Callouts|콜아웃]]


### 출처
https://forum.obsidian.md/t/a-guide-on-links-vs-tags-in-obsidian/28231
https://help.obsidian.md/Linking+notes+and+files/Embed+files