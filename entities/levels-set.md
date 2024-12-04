### Levels Set

A "level set" in Reldens is a container group of ["levels"](https://github.com/damian-pastorini/reldens-docs/blob/master/entities/level.md).

As part of a "level set" you will find two properties that can be specified to help with the "levels" creation: 
- "Autofill ranges": to automatically generate virtual gaps between the assigned levels.
- "Autofill experience multiplier": which is the value used to increase the experience required between the levels.

But the recommendation is to keep these disabled and use the ["levels" generator](https://github.com/damian-pastorini/reldens-docs/blob/master/generators/players-experience-per-level.md).

Here's an example on how these properties would work:
- Created Level 1, required experience 1.
- Created Level 2, required experience 10.
- Created Level 5, required experience 100.

The "Autofill ranges" will create virtual levels for 3 and 4.
The "Autofill experience multiplier" will be used as multiplied for the previous level required experience, like:
```
Math.round(this.levels[n-1].requiredExperience * this.autoFillExperienceMultiplier);
```
So if you have 1.5 as multiplier, then virtual level 3 experience will be 15 and for virtual level 4 will be 22.5.

As you can see it can be helpful but also risky since in a few levels the number can get high pretty quick.

Also, this value will be "unique" for every level, so if you have a gap for example between level 45 and 48 it will still be using the same multiplier. 
