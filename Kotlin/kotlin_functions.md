# 코틀린 함수들

### Slice

- 배열을 어떤 특정 범위만큼 자른다.
- 자른 뒤, list를 반환한다.
- Usage

```kotlin
val arr = arrayOf(1,2,3,4,5)
println(arr.slice(1..3))
// 결과
[2,3,4]
```

### sorted

- 기본적으로 사용할 수 있는 정렬 함수다.
- Collection에 대해서 사용한다.

### sortedDescending

- 내림차순 정렬을 지원한다.
- Collection에 대해서 사용한다.

### sortedWith

- Comparator를 인자로 전달받아 사용자 정의 타입에 대해서 사용자가 정렬 기준을 정의할 수 있다.
- compareBy()를 전달할 수 있다.
    - 이때는 compareBy() 함수의 인자로 여러 개의 람다를 전달할 수 있다.
- usage

1) Comparator

```kotlin
private fun solution(strings: Array<String>, n: Int): Array<String> {
        return strings.sortedWith(Comparator { o1, o2 ->
            if (o1[n] == o2[n]) o1.compareTo(o2)
            else o1[n] - o2[n]
        }).toTypedArray()
    }
```

2) compareBy()

```kotlin
private fun solution2(strings: Array<String>, n: Int): Array<String> {
        val result = strings.sortedWith(compareBy({ it[n] }, { it }))
        println(result)
        return result.toTypedArray()
    }
```

- 첫 번째 인자로 전달받은 람다를 기준으로 정렬한다.
- 첫 번째 람다로 정렬했을 때, 두 문자열이 동일하다면 두 번째 람다를 기준으로 정렬한다.

### joinToString

- Collection에 대해서 사용할 수 있다.
- list 내에 포함된 자료들을 사용자가 지정한 구분자와 함께 하나의 문자열로 표현할 수 있는 함수이다.
- prefix, postfix 등 여러 인자를 사용하여 다양하게 활용할 수도 있다.
- usage

```kotlin
val list = listOf("lee", "jung", "park")
println(list) // [lee, jung, park]
println(list.joinToString("")) // leejungpark
println(list.joinToString(" - ")) // lee - jung - park
```

### subList

- fromIndex ~ toIndex까지 list를 잘라서 반환한다.
- fromIndex는 포함하고, toIndex는 포함하지 않는다.