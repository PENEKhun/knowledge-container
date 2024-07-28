# 위상 정렬
- 순서를 결정할때 사용하는 알고리즘.
- 방향이 있는 그래프지만, 사이클(순환)이 존재하면 적용할 수 없음.
	> 왜냐면 `Indegree`가 0이 되지 않아 아무 노드도 큐에 포함되지 않기 때문에.
- 한가지의 답으로만 나오진 않음.

## 구현 플로우
![[위상정렬.png]]
> 이미지 출처 : [바킹독 유튜브](https://www.youtube.com/watch?v=Th-gLZUrd04) 7분04초

1. 처음에 [[Indegree]]가 0인 모든 노드를 큐에 추가함.
2. 큐를 순회하면서, 인접 노드의 `indegree`를 1씩 감소함. 그리고 `indegree`가 0이면 큐에 추가함.

### 대충 소스코드
- [백준 : 줄 세우기](https://www.acmicpc.net/problem/2252)
	```java
/*  
  BAEKJOON 2252 줄 세우기  
  https://www.acmicpc.net/problem/2252  
*/  
  
public class Main {  
  
  static class Student {  
    int number = 0;  
    int indegree = 0;  
    List<Student> next = new ArrayList<>();  
  
    public Student(int number) {  
      this.number = number;  
    }  }  
  
  public static void main(String[] args) throws IOException {  
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
    StringBuilder result = new StringBuilder();  
  
    String[] NM = br.readLine().split(" ");  
    int n = Integer.parseInt(NM[0]);  
    int m = Integer.parseInt(NM[1]);  
  
    Student[] students = new Student[n + 1];  
    for (int i = 1; i <= n; i++) {  
      students[i] = new Student(i);  
    }  
    // A B -> A가 B학생보다 앞에서야함.  
    for (int i = 0; i < m; i++) {  
      String[] input = br.readLine().split(" ");  
      int frontStudentNum = Integer.parseInt(input[0]);  
      int backStudentNum = Integer.parseInt(input[1]);  
  
      students[backStudentNum].indegree++;  
      students[frontStudentNum].next.add(students[backStudentNum]);  
    }  
    Queue<Student> q = new LinkedList<>();  
    for (int i = 1; i <= n; i++) {  
      if (students[i].indegree == 0) {  
        q.add(students[i]);  
      }  
    }  
  
    while (!q.isEmpty()) {  
      Student student = q.poll();  
      result.append(student.number).append(" ");  
  
      for (Student next : student.next) {  
        next.indegree--;  
        if (next.indegree == 0) {  
          q.add(next);  
        }  
      }  
    }  
  
    System.out.println(result);  
  }  
}
	```
# Reference
[바킹독의 실전 알고리즘 0x1A강 - 위상 정렬](https://www.youtube.com/watch?v=Th-gLZUrd04)
 -> 진짜 맛도리 강의다