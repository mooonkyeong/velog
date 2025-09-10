<p><a href="https://www.hackerrank.com/challenges/placements/problem?isFullScreen=true">문제링크</a></p>
<h4 id="💡문제조건">💡문제조건</h4>
<ul>
<li>Students, Friends, Packages라는 세개의 테이블 제공<ul>
<li>Students : ID, NAME</li>
<li>Friends : ID, Friends_ID</li>
<li>Packages : ID, SALARY</li>
</ul>
</li>
<li>친구가 자신보다 더 높은 급여 제안받은 학생들의 이름 출력하는 쿼리 작성</li>
<li>이름은 친구에게 제안된 급여를 기준</li>
</ul>
<hr />
<h4 id="💡문제풀이">💡문제풀이</h4>
<ol>
<li>테이블 JOIN</li>
</ol>
<pre><code>SELECT S.NAME
FROM STUDENTS S
JOIN FRIENDS F ON S.ID = F.ID
JOIN PACKAGES P ON S.ID = P.ID
JOIN PACKAGES FP ON F.FRIENDS_ID = FP.ID
</code></pre><ol start="2">
<li><p>WHERE 조건문</p>
<pre><code>WHERE FP.SALARY &gt; P.SALARY</code></pre></li>
<li><p>정렬</p>
<pre><code>ORDER BY FP.SALARY</code></pre></li>
</ol>
<h4 id="결과">결과</h4>
<p><img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/5988c36d-ae73-406c-819e-75bdfa3c5b47/image.png" /></p>