## Combat Maths

Simple maths to check for attack success and damage

### Stats

To use these calculations you need these base stats

#### Attacker
* Attack
* Damage
* Critical Chance
* Critical Damage

#### Defender
* Defense


### Hit/Miss Calculation

Attack success is `Attack - Defense + Rnd[1-100]`

To work out the Damage multiplier refer to this table;

| Result | Outcome | Damage Multiplier |
|--------|---------|--------|
| < 30   | Miss    | 0%     |
| < 60   | Graze   | 50%    |
| < 100  | Hit     | 100%   |
| >= 100 | Hit + Critical Chance | 100% + Critical Damage |

Damage done is then the `Damage * Damage Multiplier`. 

### Adding Critical Chances

If the result is 100 or greater we also check for critical and add the critical damage multiplier.

If the critical chance fails then the result is `Hit`, if it is successful then it is `Critical`
