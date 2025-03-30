---
title: Standard Deviation
notetype: unfeed
date: 06-01-2022
---
Standard deviation describes how values are spread around the [[Mean]]. Low standard deviation means that the values are tightly clustered around mean (think a spiked graph), while high standard deviation means that the values are spread far apart (think more of like a bell curve).

If you have a group of people with the following heights:
- 160
- 170
- 175
- 180
- 201

The [[Mean]] height of the group is `(160+170+175+180+201)/5 = 177.2`

To calculate standard deviation, we first calculate each height's square deviation (the sqare of it's difference from the mean):
- `(177.2-160)^2 = 295.84`
- `(177.2-170)^2 = 51.84`
- `(177.2-175)^2 = 4.84`
- `(177.2-180)^2 = 7.84`
- `(177.2-201)^2 = 566.44`

Next, we calculate Average Variance by averaging all the square deviations: `(295.84+51.84+4.84+7.84+566.44)/5 = 185.36`

Finally, taking the square root of average variance gives us the standard deviation: `sqrt(185.36) = 13.6146979401`

If we add 2 people to the group, who are the shortest and tallest persons in the world, our standard deviation would rise to `50.68`. If all the people in the group had the same height, standard deviation would be `0`.

-----

Status: #🌲 


