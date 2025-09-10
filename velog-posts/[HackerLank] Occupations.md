<p><a href="https://www.hackerrank.com/challenges/occupations/problem?isFullScreen=true">문제 링크</a></p>
<h4 id="💡-문제-조건">💡 문제 조건</h4>
<p>이름 | 직업 구조인 테이블을
직업별로 묶고 직업에 해당하는 이름을 알파벳순으로 직업 아래에 표시되도록
ex)
직업1 | 직업2 | 직업3
a        c        j
b        d        null
null    f        null
</p>
<h4 id="💡-문제-풀이">💡 문제 풀이</h4>
<ol>
<li>직업별로 알파벳 순으로 순위 매기기<pre><code>SELECT OCCUPATION,
     NAME,
     ROW_NUMBER() OVER(PARTITION BY OCCUPATION ORDER BY NAME) AS NR</code></pre><img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/55ff93f4-58eb-4b3e-a3fb-43e0f7fac5af/image.png" /></li>
</ol>


<ol start="2">
<li>피벗을 위해 CASE 문 사용<pre><code>SELECT NR,
     CASE WHEN OCCUPATION = 'Doctor' THEN NAME END,
     CASE WHEN OCCUPATION = 'Professor' THEN NAME END,
     CASE WHEN OCCUPATION = 'Singer' THEN NAME END,
     CASE WHEN OCCUPATION = 'Actor' THEN NAME END
FROM(SELECT OCCUPATION,
     NAME,
     ROW_NUMBER() OVER(PARTITION BY OCCUPATION ORDER BY NAME) AS NR
FROM OCCUPATIONS) AS T</code></pre><img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/e2795390-d615-4f16-b8f6-5eb420878a8d/image.png" /></li>
</ol>

3. Group By, Order By
- select 절의 집계는 어떤 것이든 상관 없음
```
SELECT MIN(CASE WHEN OCCUPATION = 'Doctor' THEN NAME END),
        MIN(CASE WHEN OCCUPATION = 'Professor' THEN NAME END),
        MIN(CASE WHEN OCCUPATION = 'Singer' THEN NAME END),
        MIN(CASE WHEN OCCUPATION = 'Actor' THEN NAME END)
FROM(SELECT OCCUPATION,
        NAME,
        ROW_NUMBER() OVER(PARTITION BY OCCUPATION ORDER BY NAME) AS NR
FROM OCCUPATIONS) AS T
GROUP BY NR
ORDER BY NR
```

<p><img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/bc3dcc80-9dd0-4b05-afda-da1951053a32/image.png" /></p>