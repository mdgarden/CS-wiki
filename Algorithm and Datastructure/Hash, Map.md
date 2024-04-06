---
tags:
  - Algorithm
  - Datastructure
  - Hash
  - Map
---

> [!abstract] Abstract, Summary, Tldr
> Hash는 함수고 Map은 자료구조다.
> 해시 테이블은 개념적인 자료구조고 Map은 ES6에서부터 표준이 된 기본 자료구조다.

## Hash

## 해시 테이블
### 예제: 체이닝을 사용한 해시 테이블

체이닝 방식에서는 해시 테이블의 각 인덱스에 연결 리스트를 할당하여 충돌이 발생했을 때 해당 인덱스의 리스트에 요소를 추가합니다. 이 방법은 충돌을 효율적으로 관리할 수 있으며, 해시 테이블의 로드 팩터(저장된 엔트리 수 / 테이블의 총 슬롯 수)가 높아질 때 유용합니다.

```ts
class HashTable<K, V> {
  private table: Array<Array<[K, V]>>;
  private size: number;

  constructor(size: number = 100) {
    this.table = new Array(size);
    for (let i = 0; i < size; i++) {
      this.table[i] = [];
    }
    this.size = size;
  }

  private hash(key: K): number {
    let hashValue = 0;
    const stringKey = JSON.stringify(key);
    for (let i = 0; i < stringKey.length; i++) {
      hashValue += stringKey.charCodeAt(i);
    }
    return hashValue % this.size;
  }

  public set(key: K, value: V): void {
    const index = this.hash(key);
    const bucket = this.table[index];
    const found = bucket.find(([k]) => k === key);

    if (found) {
      found[1] = value;
    } else {
      bucket.push([key, value]);
    }
  }

  public get(key: K): V | undefined {
    const index = this.hash(key);
    const bucket = this.table[index];
    const found = bucket.find(([k]) => k === key);

    return found ? found[1] : undefined;
  }
}

```