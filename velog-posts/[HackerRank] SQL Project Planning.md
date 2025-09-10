<p><a href="https://www.hackerrank.com/challenges/sql-projects/problem?isFullScreen=true">문제 링크</a></p>
<h4 id="순위-정하는-함수">순위 정하는 함수</h4>
<ul>
<li>ROW_NUMBER(), RANK(), DENSE_RANK()</li>
<li>() 안에 아무런 인자도 입력하지 않음</li>
</ul>
<p>ROW_NUMBER : 중복순위 X, EX) 1&gt;2&gt;3&gt;4
RANK() : 중복순위 O, EX) 1&gt;1&gt;3&gt;4&gt;4
DENSE_RANK() : 중복순위O, 빠지는 숫자 X, EX) 1&gt;1&gt;2&gt;3&gt;4&gt;4</p>


<hr />
<h4 id="💡문제조건">💡문제조건</h4>
<h4 id="목표--프로젝트-진행-일수에-따라-프로젝트의-시작-및-종료-날짜를-오름차순으로-출력">목표 : 프로젝트 진행 일수에 따라 프로젝트의 시작 및 종료 날짜를 오름차순으로 출력</h4>
<p>Project 테이블</p>
<ul>
<li>Task_ID</li>
<li>Start_Date</li>
<li>End_Date</li>
</ul>
<p>END_Date와 Start_Date 차이는 1일로 고정
작업의 종료일이 연속적이면 동일한 프로젝트
기준 -&gt; 프로젝트 시작 기준 오름차순</p>
<p><img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/6cbda108-a9a8-49f0-a907-762643fb298f/image.png" /></p>
<hr />
<h4 id="💡문제풀이">💡문제풀이</h4>
<p>1 . 순위</p>
<pre><code>SELECT START_DATE,
    ROW_NUMBER() OVER(ORDER BY START_DATE) AS RN
FROM PROJECTS</code></pre><p>결과는 이런식으로 나온다 <img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/fbfd5dc1-81cc-4e2c-8f66-74dac849d6e3/image.png" /></p>


<ol start="2">
<li>그룹으로 묵기 위한 과정<pre><code>SELECT START_DATE,
 END_DATE,
 START_DATE-ROW_NUMBER() OVER(ORDER BY START_DATE) AS RN
FROM PROJECTS</code></pre></li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/3b8d282d-1291-4338-a146-b995b741cbcb/image.png" /></p>
<p>같은 프로젝트끼리는 같은 값을 가지게 되는 걸 볼 수 있다</p>



<ol start="3">
<li>최종 코드<pre><code>SELECT MIN(START_DATE), MAX(END_DATE)
FROM(SELECT START_DATE,
 END_DATE,
 START_DATE-ROW_NUMBER() OVER(ORDER BY START_DATE) AS RN
FROM PROJECTS) PROJECTS
GROUP BY RN
ORDER BY DATEDIFF(MAX(END_DATE), MIN(START_DATE)), MIN(START_DATE)</code></pre></li>
</ol>
<p><img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/d2ac8cbe-2ca1-4c94-827b-e4cc2dc72577/image.png" /></p>
<hr />


다른 풀이

<pre><code>SELECT START_DATE, MIN(END_DATE)
FROM (SELECT START_dATE
     FROM PROJECTS
     WHERE START_DATE NOT IN (SELECT END_DATE FROM PROJECTS)) P1,
     (SELECT END_DATE
     FROM PROJECTS
     WHERE END_DATE NOT IN (SELECT START_DATE FROM PROJECTS)) P2
WHERE START_DATE &lt; END_DATE
GROUP BY START_DATE
ORDER BY DATEDIFF(MIN(END_DATE), START_DATE), START_DATE</code></pre>