#### MapReduce 과정
1. Map        
입력데이터(정형/반정형/비정형)를 Key-value 데이터로 바꿔주는 과정 (Mapper가 이를 수행)

2. Combiner
Mapper를 통해 생성된 데이터들을 Key를 기준으로 데이터를 병합함 (데이터의 양을 줄여 Network bottle-nect 현상을 줄여줄 수 있는 과정)

3. Suffle, Partitioner
Combiner에 의해 병합된 각각의 데이터들을 처리할 Node로 보내주는 역할 (Partitioner이 suffle을 수행함)

4. Sort
Reduce에서 더욱 효율적으로 Computing하기 위해 정렬을 수행 (Suffle을 통해 데이터를 전달받은 Reducer가 Reduce과정을 수행하기 전 전처리)

5. Reduce
사용자에 의해 정의된 연산을 수행

#### MapReduce를 사용한 Word Count 예제 
![예제](https://www.researchgate.net/profile/K_Srinivasa/publication/281768670/figure/fig3/AS:282303059251209@1444317702935/Different-phases-of-map-reduce-in-word-count-example.png)

###### - &nbsp;[참고자료 1](https://m.blog.naver.com/PostView.nhn?blogId=alice_k106&logNo=220462251435&proxyReferer=https%3A%2F%2Fwww.google.com%2F)