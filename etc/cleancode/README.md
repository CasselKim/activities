# Clean code

# 의미있는 있는 이름

1. 의도를 분명히 밝혀라

- 주석이 필요하다면 의도가 분명하지 않다는 뜻이다

```python
# Bad
def getThem() :
	list1 = []
	for x in theList :
		if x[0] == 4 : list1.add(x)
	return list1
```

```python
# Better
def getFlaggedCells() :
	flaggedCells = []
	for cell in gameBoard :
		if cell[STATUS_VALUE] == FLAGGED : flaggedCells.add(cell)
	return flaggedCells
```

```python
# Best
def getFlaggedCells() :
	flaggedCells = []
	for Cell in gameBoard :
		if Cell.cell.isFlagged() : 
			flaggedCells.add(Cell.cell)
	return flaggedCells
```

2. 그릇된 정보를 피하라

- 널리 쓰이는 의미의 단어는 그 의미대로 쓰자

  `accountList(x)` `accountGroup(o)` `bunchOfAccounts(o)` `Accounts(o)`

- 서로 흡사한 이름은 사용하지 않는다

  `XYZControllerForEfficientHandlingOfString, XYZControllerForEfficientStorageOfStrings (x)`

- 이름만 보고 정확한 정보를 파악하게 하라

  `a = l, a = 1 (x)` `if ( O == l ) (x)` → 소문자 L과 1, 대문자 O와 숫자 0을 구분하기 힘듬

3. 의미있게 구분하라

- 이름이 다르면 의미도 달라야 한다

```python
# Bad, a1과 a2가 정보를 전혀 제공해주지 못함
def copyChars(a1, a2) :
	for i in range(0,len(a1)) :
		a2[i] = a1[i]	

# Better, 역할을 충분히 설명해줌
def copyChars(source, destination) :
	for i in range(0,len(a1)) :
		destination[i] = source[i]
```

- 불용어를 추가한 이름은 정보를 제공하지 못한다

  `Product, ProductInfo, ProductData` 는 개념을 구분하지 못한 사례이다

4. 발음하기 쉬운 이름을 사용하라

- `genymdhms(generate data, year, month, day, hour, minute, second)` 는

  읽을 때 `젠 와이 엠 디 에이치 엠 에스` 라고 읽어야되므로 소통 시 굉장히 불편하다

5. 검색하기 쉬운 이름을 사용하라