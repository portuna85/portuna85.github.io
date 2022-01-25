---
layout: single
title: "컬렉션 프레임워크(Collections Framework)"
---
## 컬렉션 프레임워크
### 컬렉션(Collection)
  - 여러 객체(데이터)를 모아 놓은 것
### 프레임 워크(Framework)
  - 표준화, 정형화된 체계적인 프로그래밍 방식
### 컬렉션 프레임워크(Collections Framework)
  - 컬렉션을 다루기 위한 표준화된 프로그래밍 방식
  - 컬렉션을 쉽고 편리하게 다룰 수 있는 다양한 클래스 제공
### 컬렉션 클래스(Collection class)
  - 다수의 데이터를 저장할 수 있는 클래스

## 컬렉션 프레임워크의 핵심 인터페이스

### Collection 인터페이스 (Collections와 다름 - 이건 클래스)
- List와 Set의 공통점을 모아둔 인터페이스다.

### List 인터페이스 - 순서 Ok, 중복 Ok
  - 순서가 있는 데이터의 집합, 데이터 중복 허용(대기자 명단 - wating list)
  
### ArrayList
  - 기존의 Vector를 개선한 것 
  - List인터페이스를 구현하므로, 저장순서가 유지되고 중복을 허용함.
  - 데이터의 저장공간으로 배열을 사용.
  - ArrayList.calss 소스에 Object[] (객체배열)이 있다.
  - 다형성, 모든종류의 객체 저장 가능.

#### 배열(Array)의 장단점
- 배열은 구조가 간단해서 데이터를 읽는데 걸리는 시간(접근시간, access time)이 짧다.
- 크기를 쉽게 변경할 수 없다.
- 크기를 변경해야 하는 경우 더 큰배열을 생성후 데이터를 복사한다.
- 비순차적인 데이터의 추가, 삭제에 시간이 많이 걸린다.


#### ArrayList에 저장된 객체의 삭제 과정 (배열기반 - 연속적)
  - ArrayList에 저장된 세번째 데이터(data[2])를 삭제하는 과정. list.remove(2);를 호출
  1. 삭제할 데이터 아래의 데이터를 한칸씩 위로 복사해서 삭제할 데이터를 덮어쓴다.
  2. 데이터가 모두 한 칸씩 이동했으므로 마지막 데이터는 null로 변경한다.  data[size - 1] = null;
  3. 데이터가 삭제되어 데이터의 개수가 줄었으므로 size의 값을 감소시킨다.  size--;
  4. 마지막 데이터 삭제시 복사 필요없이 바로 null 대입 시켜준다.
  

#### ArrayList에 저장된 객체의 전체 삭제 과정
  1. ArrayList에 저장된 첫 번째 객체부터 삭제하는 경우
  - 앞으로 하나씩 옮긴 후 마지막에 null 대입.(배열 복사 발생)
    for(int i = 0; i < list.size(); i++)
        list.remove();

  2. ArrayList에 저장된 마지막 객체부터 삭제하는 경우
  - 배열의 마지막부터 null값 대입(배열 복사 발생 안함)
    for(int i = list.size-1; i >= 0, i--)
        list.remove(i);

```java
public class ArrayList {
    public static void main(String[] args) {
        // 기본길이 (size)가 10인 ArrayList 객체 생성
        ArrayList list1 = new ArrayList(10);

        // ArrayList에는 객체만 저장가능
        // autoboxing에 의해 기본형이 참조형으로 자동변환
        list1.add(5);                               // list1.add(new Integer(5));  new Integer()  <- 생략
        list1.add(new Integer(4));
        list1.add(new Integer(1));
        list1.add(new Integer(0));
        list1.add(new Integer(2));
        list1.add(new Integer(3));

        // ArrayList(Collection c)
        ArrayList list2 = new ArrayList(list1.subList(1, 4));       // sublist(1번이상 index, 4번미만 index)는 ArrayList의 일부를 뽑아 새로운 List 생성
        print(list1, list2);

        /*
        여긴 Collection이 아님 Collections - 이건 클래스
        Collections.sort를 사용하여 list1, list2 정렬
        */
        Collections.sort(list1);
        Collections.sort(list2);
        print(list1, list2);

        // list1에 list2가 포함되어 있는지 확인 메소드
        System.out.println("list1.containsAll(list2) : " + list1.containsAll(list2));

        // list2에 index : 3 자리에 element : A 추가
        list2.add('B');
        list2.add('C');
        list2.add(3, 'A');
        print(list1, list2);

        // list2에 index : 3 자리에 elemlnt : AAA 로 set으로 변경
        list2.set(3, "AAA");
        print(list1, list2);

        // list1에 index : 0 자리에 element : String 타입의 "1" 추가
        list1.add(0, "1");

        // indexOf()는 지정된 객체의 위치(index)를 알려준다.
        System.out.println("index = " + list1.indexOf(new Integer("1")));
        print(list1, list2);

        // list1에 index : 1 자리의 객체 삭제  list1
        list1.remove(1);                        // 인덱스가 1인 객체 삭제  new Integer()의 사용유무 철처확인
        print(list1, list2);
        // list1에 new Integer(1) element 삭제
        list1.remove(new Integer(1));           // 1을 삭제 new Integer()의 사용유무 철처확인
        print(list1, list2);

        // list1에서 list2와 겹치는 부분만 남기고 나머지 삭제.
        System.out.println("list1.retainAll(list2) : " + list1.retainAll(list2));
        print(list1, list2);

        /*
        list2에서 list1에 포함된 객체들을 삭제
        1. get(i)로 list2에서 하나씩 꺼낸다.
        2. contains()로 꺼낸 객체가 list1에 있는지 확인
        3. remove(i)로 해당객체를 list2에서 삭제
        */
        for (int i = list2.size()-1; i >= 0; i--) {
            if(list1.contains(list2.get(i)))
                list1.remove(i);
        }
        print(list1, list2);
    }

    static void print(ArrayList list1, ArrayList list2) {
        System.out.println("list1 : " + list1);
        System.out.println("list2 : " + list2);
        System.out.println("---------------------------------------------");
    }
}
```
### LinkedList - 연결 리스트, 데이터 접근성 나쁨  (연결기반 - 불연속적)
  - 배열과 달리 Linked List는 불연속적으로 존재하는 데이터를 연결(link)
  - 뒤쪽의 참조 주소연결
  - 데이터의 삭제 : 한번의 참조변경으로 가능
  - 데이터의 추가 : 한번의 Node 객체생성과 두번의 참조변경만으로 가능
  - 연결리스트 데이터 접근성이 나쁨
  - 바로 다음 객체만 알고 있어 하나씩 차례로 접근해야함
### Doubly Linked List - 이중 연결리스트, 접근성 향상
  - 더블 링크드 리스트(Doubly Linked List) - 이중 연결리스트, 접근성 향상
  - 앞뒤로 참조 주소 연결
### Doubly circular Linked List  - 이중 원형 연결리스트
  - 맨 앞 요소에서 맨마지막 요소로 접근가능 ( 반대로도 가능 )
  
### ArrayList vs LinkedList 비교
  1. 순차적으로 데이터 추가 / 삭제 - ArrayList가 빠름
  2. 비순차적으로 데이터 추가 / 삭제 - LinkedList가 빠름
  3. 접근시간(access time) - ArrayList가 빠름
```java
class Node {                // Node 객체 
    Node next;              // 다음 요소
    Object obj;
}
class Node {
  Node next;                // 다음 요소
  Node previous;            // 이전 요소
  Object obj;
}
```
## 스택과 큐 (Stack & Queue)
### 스택(Stack) : LIFO(Last In First Out)구조. 마지막에 저장(push)된것을 제일 먼저 꺼내게(pop) 된다.
   - 클래스다. 객체 생성 가능
   - 배열, ArrayList가 적합.
   - boolean empty()      Stack이 비어있는지 알려줌
   - Object peek()        Stack의 맨 위에 저장된 객체를 반환. pop()과 달리 꺼내지 않음
   - Object pop()         Stack의 맨 위에 저장된 객체 꺼냄
   - Object push()        Stack의 객체(item)를 저장
   - int search(Object o) Stack에서 주어진 객체(o)를 찾아서 그 위치를 반환. 못찾으면 -1을 반환
ex) - 수식계산, 수식괄호검사, 워드프로세서의 undo/redo, 웹브라우저의 뒤로가기/앞으로가기
   
### 큐(Que) : FIFO(First In First Out)구조. 먼저 저장(offer)한것을 먼저 꺼내게(poll) 된다.
   - 인터페이스다. 직접 객체 생성 불가.    Queue que = new LinkedList(); (LinkedList가 Que를 implements 받음)
   - LinkedList가 적합(삭제시 자리이동 없음)
   - boolean add(Object o)  객체를 Que에 추가 저장공간 부족하면 예외 발생
   - Object remove()        객체를 제거 예외 발생
   - Object element()       삭제 없이 요소를 읽어온다. peek과 달리 예외 발생
   - boolean offer()        Que에 객체를 저장. true나 fals 반환
   - Object poll()          Que에 객체를 꺼내 반환. 비어있으면 null을 반환
   - Object peek()          삭제없이 요소를 읽어온다. Que가 비어있으면 null을 반환
#### ex) - 최근 사용문서, 인쇄작업 대기목록
```java
public class StackQueue {
    public static void main(String[] args) {
        Stack st = new Stack();
        Queue que = new LinkedList();

        st.push("1");
        st.push("2");
        st.push("3");

        que.offer("1");
        que.offer("2");
        que.offer("3");

        System.out.println("= Stack =");
        while (!st.empty()) {                      // 스택에서 비었는지 확인
            System.out.println(st.pop());         // 스택에서 요소를 하나씩 꺼낸다.  출력 3, 2, 1
        }

        System.out.println("= Queue =");
        while (!que.isEmpty()) {                    // 큐에서 비었는지 확인
            System.out.println(que.poll());       // 큐에서 요소를 하나씩 꺼낸다.    출력 1, 2, 3
        }
    }
}
```
### Iterator, ListIterator, Enumeration
  - 컬렉션에 저장된 데이터를 접근하는데 사용되는 인터페이스
  - Enumeration은 Iterator의 구버전
  - ListIterator는 Ilterator의 접근성을 향상시킨 것(단방향 -> 양방향)  previous() 메소드도 있음
  - 컬렉션에 저장된 요소들을 읽어오는 방법을 표준화한 것
  - iterator()를 호출햇 Iterator를 구현한 객체를 얻어서 사용

  - Map에는 iterator()가 없다. keySet(), entrySet(), values()를 호출해야한다.
  - Map map = new HashMap();
  - Iterator it = map.entrySet().iterator(); 

#### Iterator 메소드
  - boolean hasNext()           읽어올 요소가 남아있는지 확인
  - Object next()               다음 요소를 읽어온다. next()를 호출하기 전 hasNext()를 호출해서 읽어 올 요소가 있는지 확인하는게 안전
  
  - boolean hasMoreElements()   Enumerationd의 메소드
  - Object nextElements()       Enumerationd의 메소드
```java
public class Test {
    public static void main(String[] args) {
        Collect list = new ArrayList();                // 다른 컬렉션으로 변경할 때는 이부분만 고치면됨.
        list.add("1");
        list.add("2");
        list.add("3");
        list.add("4");
        list.add("5");

        Iterator it = list.iterator();              
        while (it.hasNext()) {                      // 읽어올 요소 확인.
            Object obj = it.next();                 // 요소 읽어오기
            System.out.println(obj);                 
        }
    }
}
```
#### Arrays 클래스
 - 배열을 다루기 편리한 메서드(static) 제공
  1. 배열 출력 - toString()
  2. 배열의 복사 - copyOf(), copyOfRange()
  3. 배열 채우기 - fill(), setAll()
  4. 배열의 정렬과 검색 - sort(), binarySearch();
```java
public class Test {
    public static void main(String[] args) {
        int[] arr = {3, 2, 0, 1, 4};
        int idx1 = Arrays.binarySearch(arr, 2);   // 이진탐색(정렬된 배열에만 가능) idx1 = -5 잘못된 결과.
        
        Arrays.sort(arr);                              // 정렬 [0,1,2,3,4]
        int idx2 = Arrays.binarySearch(arr, 2);   
        System.out.println(idx1);                       // idx2 = 2;
    }
}
```
  5. 다차원 배열의 출력 - deepToString();
  6. 다차원 배열의 비교 - deepEquals();
  7. 배열을 List로 변환 - asList(Object... a)
```java
  public class Test {
  public static void main(String[] args) {
    int[] arr = {0, 1, 2, 3, 4};
    // int[][] arr2D = {{11, 12, 13}, {21, 22, 23}};

    System.out.println(Arrays.toString(arr));
    System.out.println(Arrays.toString(arr2D));    // 이중배열 출력하면 주소값 나옴
    System.out.println(Arrays.deepToString(arr2D));

    int[] arr2 = Arrays.copyOf(arr, 5);
    int[] arr3 = Arrays.copyOfRange(arr, 2, 4);
    int[] arr4 = Arrays.copyOfRange(arr, 0, 7);

    System.out.println("arr2 : " + Arrays.toString(arr2));
    System.out.println("arr3 : " + Arrays.toString(arr3));
    System.out.println("arr4 : " + Arrays.toString(arr4));

    int[] arr5 = new int[5];
    Arrays.fill(arr5, 9);
    System.out.println("arr5 : " + Arrays.toString(arr5));

    Arrays.setAll(arr5, i -> (int)(Math.random()*6+1));
    System.out.println("arr5 : " + Arrays.toString(arr5));
  }
}
```
#### Comparable과 Comparator
  - 객체 정렬에 필요한 메소드(정렬기준 제공)를 정의한 인터페이스
    1. Comparable : 기본 정렬기준을 구현하는데                  -기본 Default
    2. Comparator : 기본 정렬기준 외 다른 기준으로 정렬하고자 할 떄 사용
```java
public interface Comparator {
    int compare(Object o1, Object o2);         // o1, o2 두 객체를 비교
    boolean equals(Object obj);                // equals를 오버라이딩 하라는 뜻
}

public interface Comparable {
    int compareTo(Object o);                    // 주어진 객체(o)를 자신과 비교
}
```

### Set 인터페이스(집합) - 순서 X, 중복 X
  - 순서가 없는 데이터의 집합, 데이터 중복 허용하지 않음(육식동물 - 사자, 호랑이, 치타, 호랑이X)
  - 반환 타입은 boolean(Collection에 변화 있으면 true, 아니면 false)
#### HashSet
  - Set인터페이스를 구현한 대표적인 컬렉션 클래스
  - 순서를 유지할려면, LinkedHashSet클래스 사용
  - 주요 메소드
    1. HashSet()                    
    2. HashSet(Collection c)                                  
    3. HashSet(int initialCapacity)      
    4. HashSet(int intalCapacity, float loadFactor)
  - HashSet은 객체를 저장하기전 기존에 같은 객체가 있는지 확인, 같은 객체가 없으면 저장, 있으면 저장 안함
  - boolean add(Object o)는 저정할 객체의 equals()와 hashCode()를 호출 
    - equals()와 hashCode()가 오버라이딩 되어 있어야함
```java
public class Test {
    public static void main(String[] args) {
        Object[] objArr = {"1", new Integer(1), "2", "2", "3", "3", "4", "4", "4",};
        Set set = new HashSet();

        for (int i = 0; i < objArr.length; i++) {
          // HashSet에 objArr으 요소들을 저장.
          System.out.println(objArr[i] + " : " + set.add(objArr[i]));
        }

        // HashSet에 저장된 요소 출력
        System.out.println(set);

        // HashSet에 저장된 요소 출력(Iterator이용)
        Iterator it = set.iterator();
        while(it.hasNext()) {
            System.out.println(it.next());
        }
    }
}
```
```java
public class Test {
    public static void main(String[] args) {
        Set set = new HashSet();

        for (int i = 0; i < 6; i++) {
            int num = (int) (Math.random() * 45) + 1;
            
            // set.add(new Integer(num));
            set.add(num);
        }

        System.out.println(set);

        List list = new LinkedList(set);
        Collections.sort(list);
        System.out.println(list);
    }
}
```

#### TreeSet
  - 범위 검색과 정렬에 유리한 컬렉션 클래스
  - HashSet보다 데이터 추가, 삭제 보다 오래 걸림
  - 각 요소(node)가 나무(tree)형태로 연결(LinkedList의 변형)
  - 이진 탐색 트리(binary search tree)로 구현. 범위 탐색과 정렬에 유리
  - 이진 트리는 모든 노드가 최대 2개의 하위 노드를 가짐
    1. 이진탐색트리(biinary search tree)
    - 부모보다 작은 값은 왼쪽 큰 값은 오른쪽에 저장
    - 데이터가 많아질 수록 추가, 삭제에 시간이 더 걸림(비교 횟수 증가)
    - 데이터 저장 과정 boolean add(Object o)
    - 루트부터 트리를 따라 내려가며 값을 비교, 작으면 왼쪽, 크면 오른쪽으로 비교하면서 저장
  - 주요 메소드
    1. Object first()               정렬된 순서에 천 번째 객체를 반환       - 오름차순
    2. Object last()                정렬된 순서에 마지막 객체를 반환        - 오름차순
    3. Object ceiling(Object o)     지정된 객체와 같은 객체를 반환, 없으면 큰 값을 가진 객체중 제일 가까운 값의 객체를 반환
    4. Object floor(Object o)       지정된 객체와 같은 객체를 반환, 없으면 작은 값을 가진 객체중 제일 가까운 값의 객체를 반환
    5. Object higer(Object o)       지정된 객체보다 큰 값을 가진 객체 중 제일 가까운 값의 객체를 반환.
    6. Object lower(Object o)       지정된 객체보다 작은 값을 가진 객체 중 제일 가까운 값의 객체를 반환.

```java
public class TreeNode {
  TreeNode left;              // 왼쪽 자식 노드
  Object element;             // 저장할 객체 노드
  TreeNode Right;             // 오른쪽 자식 노드
}
```
```java
public class TreeSetEx1 {
  public static void main(String[] args) {
    TreeSet set = new TreeSet();               // 정렬 필요 없음
    // Set set = new HashSet();            // 정렬 필요

    int from = 1;
    int to = 2;

    for (int i = 0; set.size() < 15; i++) {
      int num = (int) (Math.random() * 300) + 1;
      set.add(num);
    }

    System.out.println(set);
    System.out.println("rang search : from" + from + " to " + to);
    System.out.println("result1 : "+set.subSet(1, to));
    System.out.println("result1 : "+set.subSet(from, 3));
    System.out.println("50보다 작은 값" + set.headSet(50));
    System.out.println("50보다 큰 값" + set.tailSet(50));
    System.out.println("40과 80 사이의 값 : "+set.subSet(40,80));
  }
}
```

### Map 인터페이스 - 순서 X, 중복(키 X, 값 Ok)
  - 키(Key)와 값(value)의 쌍(pair)으로 이루어진 데이터 집합 (Key와 Value를 합쳐서 Entry라고 부름)
  - 순서가 없고, 키는 중복 허용하지 않고, 값은 중복 허용함(전화번호(지역번호) - 02 서울, 아이디/비밀번호 - 아이디는 중복허용X, 비밀번호 중복가능)
#### HashMap과 HashTable
  - Map 인터페이스를 구현, 데이터를 키와 값을 쌍으로 저장
  - HashMap(동기화X)는 Hashtable(동기화Ok)의 신버젼
  - 순서를 유지할려면, LinkedHashMap클래스 사용
  - 해싱(hashing)기법으로 데이터를 저장. 데이터가 많아도 검색 빠름
    1. 키(key) : 컬렉션 내의 키(key) 중에서 유일해야 함
    2. 값(value) : 키(key)와 달리 데이터의 중복 허용
    3. 해쉬함수(hash function)를 이용해 데이터를 읽어오기 & 저장하기
    4. 해쉬함수(hash function)로 해시테이블(hash table)에 데이터를 저장, 검색
      ※ 해시테이블(Hashtable)은 배열과 링크드 리스타 조합된 형태.(2차원 배열과 유사)
        - 배열의 장점 : 접근성
        - 링크드리스트 장점 : 변경유리
  
## Collections
### Collections클래스  - 컬렉션을 위한 메서드(static)를 제공
  - 컬랙션 채우기, 복사, 정렬, 검색 - fill(), copy(), sort(), binarySearch() 등
  - 컬렉션 동기화 - synchronized ~~~()        쓰레드에서 사용
    - List syncList = Collections.synchronizedList(new ArrayList(~~~));
  - 변경불가(readOnly) 컬렉션 만들기 - unmodifiable~~~()
  - 싱글톤 컬렉션 만들기 - singleton~~~()
  - 한 종류의 객체만 저장하는 컬렉션 만들기 - checked~~~()

#### TreeMap
  - TreeSet와 같은 특성
  - 범위 검색과 정렬에 유리한 컬렉션 클래스
  - HashMap보다 데이터 추가, 삭제에 시간이 더 걸림

