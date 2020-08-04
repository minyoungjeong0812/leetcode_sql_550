# leetcode_sql_550

* Leetcode: Game Play Analysis IV                                :BLOG:Medium:
#+STARTUP: showeverything
#+OPTIONS: toc:nil \n:t ^:nil creator:nil d:nil
:PROPERTIES:
:type:     sql, classic
:END:
---------------------------------------------------------------------
Game Play Analysis IV
---------------------------------------------------------------------
#+BEGIN_HTML
<a href="https://github.com/dennyzhang/code.dennyzhang.com/tree/master/problems/game-play-analysis-iv"><img align="right" width="200" height="183" src="https://www.dennyzhang.com/wp-content/uploads/denny/watermark/github.png" /></a>
#+END_HTML
Similar Problems:
- [[https://code.dennyzhang.com/game-play-analysis-i][LeetCode: Game Play Analysis I]]
- [[https://code.dennyzhang.com/game-play-analysis-ii][LeetCode: Game Play Analysis II]]
- [[https://code.dennyzhang.com/game-play-analysis-iii][LeetCode: Game Play Analysis III]]
- [[https://code.dennyzhang.com/game-play-analysis-iv][LeetCode: Game Play Analysis IV]]
- [[https://cheatsheet.dennyzhang.com/cheatsheet-mysql-A4][CheatSheet: SQL & MySql]]
- [[https://cheatsheet.dennyzhang.com/cheatsheet-leetcode-A4][CheatSheet: Leetcode For Code Interview]]
- [[https://cheatsheet.dennyzhang.com/cheatsheet-followup-A4][CheatSheet: Common Code Problems & Follow-ups]]
- Tag: [[https://code.dennyzhang.com/review-sql][#sql]], [[https://code.dennyzhang.com/tag/classic][#classic]]
---------------------------------------------------------------------
Table: Activity
#+BEGIN_EXAMPLE
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| player_id    | int     |
| device_id    | int     |
| event_date   | date    |
| games_played | int     |
+--------------+---------+
(player_id, event_date) is the primary key of this table.
This table shows the activity of players of some game.
Each row is a record of a player who logged in and played a number of games (possibly 0) before logging out on some day using some device.
#+END_EXAMPLE
 
Write an SQL query that reports the fraction of players that logged in again on the day after the day they first logged in, rounded to 2 decimal places. In other words, you need to count the number of players that logged in for at least two consecutive days starting from their first login date, then divide that number by the total number of players.

The query result format is in the following example:
#+BEGIN_EXAMPLE
Activity table:
+-----------+-----------+------------+--------------+
| player_id | device_id | event_date | games_played |
+-----------+-----------+------------+--------------+
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-03-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |
+-----------+-----------+------------+--------------+

Result table:
+-----------+
| fraction  |
+-----------+
| 0.33      |
+-----------+
Only the player with id 1 logged back in after the first day he had logged in so the answer is 1/3 = 0.33
#+END_EXAMPLE

Github: [[https://github.com/dennyzhang/code.dennyzhang.com/tree/master/problems/game-play-analysis-iv][code.dennyzhang.com]]

Credits To: [[https://leetcode.com/problems/game-play-analysis-iv/description/][leetcode.com]]

Leave me comments, if you have better ways to solve.
---------------------------------------------------------------------
- Solution:

#+BEGIN_SRC sql
# https://code.dennyzhang.com/game-play-analysis-iv
select round(sum(case when t1.event_date = t2.first_event+1 then 1 else 0 end)/count(distinct t1.player_id), 2) as fraction
from Activity as t1 inner join
    (select player_id, min(event_date) as first_event
    from Activity
    group by player_id) as t2
on t1.player_id = t2.player_id
#+END_SRC

#+BEGIN_HTML
<div style="overflow: hidden;">
<div style="float: left; padding: 5px"> <a href="https://www.linkedin.com/in/dennyzhang001"><img src="https://www.dennyzhang.com/wp-content/uploads/sns/linkedin.png" alt="linkedin" /></a></div>
<div style="float: left; padding: 5px"><a href="https://github.com/dennyzhang"><img src="https://www.dennyzhang.com/wp-content/uploads/sns/github.png" alt="github" /></a></div>
<div style="float: left; padding: 5px"><a href="https://www.dennyzhang.com/slack" target="_blank" rel="nofollow"><img src="https://www.dennyzhang.com/wp-content/uploads/sns/slack.png" alt="slack"/></a></div>
</div>
#+END_HTML
