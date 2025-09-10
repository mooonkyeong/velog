<p><a href="https://www.hackerrank.com/challenges/the-pads/problem?isFullScreen=true">문제 링크</a>

</p>
<h3 id="알고-가자">알고 가자!</h3>
<ul>
<li>CONCAT : 문자열 병합</li>
<li>LEFT(컬럼, N), 컬럼의 왼쪽 부터 N번째 문자 출력 </li>
<li>SELECT 두개 이상일땐 끝에 ; 꼭 붙이기


</li>
</ul>
<hr />


<h4 id="💡문제-조건">💡문제 조건</h4>
<ol>
<li><p>이름(직업의 첫글자) 출력
 Name 기준으로 정렬</p>
</li>
<li><p>There are a total of [occupation_count] [occupation]s.
 Count, Occupation 기준으로 정렬</p>


</li>
</ol>
<hr />
<h4 id="💡문제-풀이">💡문제 풀이</h4>
<ol>
<li>이름(직업 첫글자)<pre><code>SELECT CONCAT(NAME, '(', LEFT(OCCUPATION, 1), ')')
FROM OCCUPATIONS
ORDER BY NAME;</code></pre><img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/fdba6370-6820-489a-9d4e-9e8c15fb90a6/image.png" /></li>
</ol>


<ol start="2">
<li>There are a total of [occupation_count] [occupation]s.</li>
</ol>
<ul>
<li>철자 틀리지 않게.. 주의...<pre><code>SELECT CONCAT('There are a total of ', COUNT(NAME), ' ', LOWER(OCCUPATION), 's.')
FROM OCCUPATIONS
GROUP BY OCCUPATION
ORDER BY COUNT(NAME), OCCUPATION;</code></pre><img alt="" src="https://velog.velcdn.com/images/mooonkyeong/post/b3d163b3-615f-49e7-a67e-0e7cc3a9aac5/image.png" /></li>
</ul>