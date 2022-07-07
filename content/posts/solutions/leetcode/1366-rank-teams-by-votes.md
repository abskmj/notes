---
title: "LeetCode - Rank Teams by Votes"
date: 2022-07-07T00:00:00+05:30
tags: ["LeetCode","Solution","JavaScript"]
---

Solution to [LeetCode: Rank Teams by Votes](https://leetcode.com/problems/rank-teams-by-votes/)

# Solution
- Use a map of arrays (2 dimensional data structure) to accumulate the vote counts per position per team
- Sort the map based on the vote counts per position and team name

```javascript
/* Solution to LeetCode: Rank Teams by Votes
 * URL: https://leetcode.com/problems/rank-teams-by-votes/
 */

const rankTeams = (votes) => {
    // map to hold vote count per team
    const rankings = new Map()

    // loop through each vote
    for (const vote of votes) {
        //console.log(vote)

        // loop through each team position in a vote
        for (let position = 0; position < vote.length; position++) {
            const team = vote[position]

            // update the vote count for the team at the position
            let ranking = rankings.get(team)

            // create an empty array, if not already
            if (!ranking) ranking = new Array(vote.length).fill(0)

            // record the vote
            ranking[position]++

            // console.log(team, ranking)
            rankings.set(team, ranking)
        }
    }

    // sort the teams based on the votes
    const sorted = [...rankings].sort((a, b) => {
        const rankingA = a[1]
        const rankingB = b[1]

        for (let position = 0; position < rankingA.length; position++) {
            // if vote count is same, check for next position
            if (rankingA[position] == rankingB[position]) continue

            // return team with highest vote count
            else return rankingB[position] - rankingA[position]
        }

        // break tie based on team name
        return a[0] - b[0]
    })

    // join the sorted teams
    const result = sorted.map((ranking) => ranking[0]).join('')

    // console.log(result)

    return result

}

// test case
console.assert(rankTeams(["ABC", "ACB", "ABC", "ACB", "ACB"]) === 'ACB')

// test case
console.assert(rankTeams(["WXYZ","XYZW"]) === 'XWYZ')

// test case
console.assert(rankTeams(["ZMNAGUEDSJYLBOPHRQICWFXTVK"]) === 'ZMNAGUEDSJYLBOPHRQICWFXTVK')

```