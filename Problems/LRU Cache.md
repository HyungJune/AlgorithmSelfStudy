
#### LRU Cache
#### Writer: Hyungjune Shin
#### Refer: LeetCode

## 문제 설명
Least Recently Used (LRU) cache를 구성하고, 구현하는 문제입니다. Get과 Put 연산자를 지원해야합니다.

 - Get(key) : cache에 key가 존재할 경우 key에 대응되는 양수인 value를 return해야하고, 만약 없을 경우 -1을 return 해야합니다.
 - Put(key, value) : 만약 key가 cache에 존재하지 않을 경우 key와 value를 cache에 넣어야합니다. 만약 cache가 설정된 공간(capacity)보다 많은 수의 데이터를 가지고 있을 경우, 새로운 데이터를 넣기 전에 가장 적게 최근에 사용된 데이터 (least recently used)를 지워야합니다. cache는 초기에 양수의 공간으로 초기화됩니다.

 - 참고: https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU
### 조건
 - Get과 Put 연산자를 O(1) 복잡도로 구현을 해봅시다.
 
### Example

```
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

## 솔루션
```
type pair struct {
    key int
    value int
}

type LRUCache struct {
    items map[int]*list.Element
    discardedList *list.List    
    capacity int
}

func Constructor(capacity int) LRUCache {
    cache := LRUCache{}
    cache.items = make(map[int]*list.Element, 2)
    cache.discardedList = list.New()
    cache.capacity = capacity
    return cache
}


func (this *LRUCache) Get(key int) int {
    ele, exist := this.items[key]
    if !exist {
        return -1
    } else {
        this.discardedList.MoveToFront(ele)
        return ele.Value.(*pair).value
    }
}


func (this *LRUCache) Put(key int, value int) {
	ele, exist := this.items[key]
    
    if exist {
        this.discardedList.MoveToFront(ele)
        ele.Value.(*pair).value = value
        return
    }
    
    if this.discardedList.Len() == this.capacity {
        discard := this.discardedList.Back()
        discardedKey := discard.Value.(*pair)
        delete(this.items, discardedKey.key)
        this.discardedList.Remove(discard)
    } 
    
    putValue := &pair{key, value}
    putValueEle :=this.discardedList.PushFront(putValue)
    this.items[key] = putValueEle
}


/**
 * Your LRUCache object will be instantiated and called as such:
 * obj := Constructor(capacity);
 * param_1 := obj.Get(key);
 * obj.Put(key,value);
 */
```
- 처음에는 list를 안쓰고 해보려고 했는데, get이나 put으로 인해 기존에 있던 데이터가 hit 되었을 경우 우선순위를 낮춰야 하므로 많이 복잡했습니다.
- list를 사용하였고, 특히 PushFront함수, MoveToFront함수를 통하여 구현 복잡성이 많이 줄어들었습니다.
- 데이터를 담는 items map 뿐만 아니라 discarded order를 저장할 수 있는 list를 가지고 구현했습니다.
- 기본적이로 데이터가 hit 되었을 경우에는 moveToFront로 list의 맨 앞으로 가져오고, 새로운 데이터가 추가되었을 경우에도 hit이므로 맨 앞으로(PustFront) 데이터를 넣었습니다.
- 만약 capacity가 넘어갈 경우에는 맨 마지막 element를 뽑아서 key를 구하고 해당 key에 대응되는 items를 지우고 새로 추가된 데이터를 넣는 방식으로 구현했습니다.
