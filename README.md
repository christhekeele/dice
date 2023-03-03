# Dice

> ***An RPG dice engine and notation language for `Elixir`.***

## Dice Notation

### Basics

Dice expressions let you describe rolling multiple dice of different sizes, and modifying the results. You can:

- Roll dice with any number of sides (`dS`)
- Add or subtract a constant value from the results (`dS ± C`)
- Roll multiple dice with the same number of sides and add their results together as a pool (`NdS`)
- Add or subtract multiple pools and constants together (`NdS + MdT + C`)

| Operation | Expression | Interpretation | Example | Meaning | Notes |
| :---: | ---: | :--- | ---: | :--- | :--- |
| ***Roll*** | `dS` | Roll a die with `S` sides. | `d20` | Roll 1 `d20`. | Equivalent to ***Roll Many***: `1dS`. Equivalent to ***Range Die***: `d{1..20}`. |
| ***Addition*** | `dS + C` | Roll `N` dice with `S` sides, and add a constant value `C` from the result. | `d20 + 5` | Roll 1 `d20` and add `5` to the result. |  |
| ***Subtraction*** | `dS - C` | Roll `N` dice with `S` sides, and subtract a constant value `C` from the result. | `d20 - 2` | Roll 1 `d20` and subtract `2` from the result. |  |
| ***Roll Many*** | `NdS` | Roll `N` dice with `S` sides and add the results. | `3d6` | Roll 3 `d6` and add the results. |  |
| ***Roll Different*** | `NdS + MdT + C` | Roll `N` dice with `S` sides, `M` dice with `T` sides, and add all together plus `C`. | `3d6 + d4 + 2` | Roll 3 `d6`, one `d4`, and add `2` to the results. |  |

### Roll Modifiers

Roll modifiers let you describe rolling a pool of dice, and doing something with the results before factoring them into the calculation. Multiple modifiers stack, and are applied in order.

#### Keep

***Keep*** (`K`) lets you only hold on to certain dice in a pool before adding them together.

By default, random dice are kept. This can be further modified to:

- Keep the highest rolls (***Keep Highest***: `KH`)
- Keep the lowest rolls (***Keep Lowest***: `KL`)
- Explicitly keep random rolls ***Keep Random***: (`KR`)

| Operation | Expression | Interpretation | Example | Meaning | Notes |
| :---: | ---: | :--- | ---: | :--- | :--- |
| ***Keep*** | `NdSK` | Roll `N` dice with `S` sides, and keep a random die. | `2d20K` | Roll 2 `d20` and keep one at random. | Equivalent to ***Keep Random***: `NdSK1R`. |
| ***Keep Many*** | `NdSKM` | Roll `N` dice with `S` sides, and keep `M` random dice. | `3d20K2` | Roll 3 `d20` and keep `2` at random. | Equivalent to ***Keep Random***: `NdSKMR`. |
| ***Keep Random*** | `NdSKMR` | Roll `N` dice with `S` sides, and keep `M` random dice. | `3d20K2R` | Roll 3 `d20` and keep `2` at random. | Equivalent to ***Keep Many***: `NdSKM`. |
| ***Keep Highest*** | `NdSKH` | Roll `N` dice with `S` sides, and keep the highest result. | `2d20KH` | Roll 2 `d20` and keep the highest result. |  |
| ***Keep Many Highest*** | `NdSKMH` | Roll `N` dice with `S` sides, and keep the highest `M` results. | `3d20K2H` | Roll 3 `d20` and keep the `2` highest. |  |
| ***Keep Lowest*** | `NdSKL` | Roll `N` dice with `S` sides, and keep the lowest result. | `2d20KL` | Roll 2 `d20` and keep the lowest result. |  |
| ***Keep Many Lowest*** | `NdSKML` | Roll `N` dice with `S` sides, and keep the lowest `M` results. | `3d20K2L` | Roll 3 `d20` and keep the `2` lowest. |  |

#### Drop

***Drop*** (`D`) lets you discard certain dice from a pool before adding them together.

By default, random dice are dropped. This can be further modified to:

- Drop the highest rolls (***Drop Highest***: `DH`)
- Drop the lowest rolls (***Drop Lowest***: `DL`)
- Explicitly drop random rolls (***Drop Random***: `DR`)

| Operation | Expression | Interpretation | Example | Meaning | Notes |
| :---: | ---: | :--- | ---: | :--- | :--- |
| ***Drop*** | `NdSD` | Roll `N` dice with `S` sides, and drop a random die. | `2d20D` | Roll 2 `d20` and drop one at random. | Equivalent to ***Drop Random***: `NdSD1R`. |
| ***Drop Many*** | `NdSDM` | Roll `N` dice with `S` sides, and drop `M` random dice. | `3d20D2` | Roll 3 `d20` and drop `2` at random. | Equivalent to ***Drop Random***: `NdSDMR.` |
| ***Drop Random*** | `NdSDMR` | Roll `N` dice with `S` sides, and drop `M` random dice. | `3d20D2R` | Roll 3 `d20` and drop `2` at random. | Equivalent to ***Drop Many***: `NdSKM`. | 
| ***Drop Highest*** | `NdSDH` | Roll `N` dice with `S` sides, and drop the highest result. | `2d20DH` | Roll 2 `d20` and drop the highest result. |  |
| ***Drop Many Highest*** | `NdSDMH` | Roll `N` dice with `S` sides, and drop the highest `M` results. | `3d20D2H` | Roll 3 `d20` and drop the `2` highest. |
| ***Drop Lowest*** | `NdSDL` | Roll `N` dice with `S` sides, and drop the lowest result. | `2d20DL` | Roll 2 `d20` and drop the lowest result. |  |
| ***Drop Many Lowest*** | `NdSDML` | Roll `N` dice with `S` sides, and drop the lowest `M` results. | `3d20D2L` | Roll 3 `d20` and drop the `2` lowest. |  |

#### Count

***Count*** (`C`) lets you change a dice pools output from being a sum of dice rolls, to the count of rolled dice that meet a certain criteria.

By default, all dice are counted. This can be further modified to:

- Count rolls higher than a number (***Count Greater Than***: `C>`)
- Count rolls lower than a number (***Count Lower Than***: `C<`)
- critical success, failure, explosions?

| Operation | Expression | Interpretation | Example | Meaning | Notes |
| :---: | ---: | :--- | ---: | :--- | :--- |
| ***Drop*** | `NdSD` | Roll `N` dice with `S` sides, and drop a random die. | `2d20D` | Roll 2 `d20` and drop one at random. | Equivalent to ***Drop Random***: `NdSD1R`. |
| ***Drop Many*** | `NdSDM` | Roll `N` dice with `S` sides, and drop `M` random dice. | `3d20D2` | Roll 3 `d20` and drop `2` at random. | Equivalent to ***Drop Random***: `NdSDMR.` |
| ***Drop Random*** | `NdSDMR` | Roll `N` dice with `S` sides, and drop `M` random dice. | `3d20D2R` | Roll 3 `d20` and drop `2` at random. | Equivalent to ***Drop Many***: `NdSKM`. | 
| ***Drop Highest*** | `NdSDH` | Roll `N` dice with `S` sides, and drop the highest result. | `2d20DH` | Roll 2 `d20` and drop the highest result. |  |
| ***Drop Many Highest*** | `NdSDMH` | Roll `N` dice with `S` sides, and drop the highest `M` results. | `3d20D2H` | Roll 3 `d20` and drop the `2` highest. |
| ***Drop Lowest*** | `NdSDL` | Roll `N` dice with `S` sides, and drop the lowest result. | `2d20DL` | Roll 2 `d20` and drop the lowest result. |  |
| ***Drop Many Lowest*** | `NdSDML` | Roll `N` dice with `S` sides, and drop the lowest `M` results. | `3d20D2L` | Roll 3 `d20` and drop the `2` lowest. |  |

#### Explode

***Explode*** (`!`) lets you roll extra dice into a pool before adding them together, based on previous rolls.

By default, only the maximum possible roll triggers an explosion. This can be further modified by providing an explicit threshold at which to explode (***Explode At***: `!N`).

By default, an explosion adds another die of the same sides to the pool. This can be further modified by specifying a die to explode with (***Explode With***: `!dT`)

By default, re-rolls do not trigger explosions. This can be further modified by specifying that re-rolls can keep exploding (***Keep Exploding***: `!!`, ***Keep Exploding At***: `!!N`).

> ***Keep Exploding*** (`!!`) will not trigger on 1-sided dice, or dice with a single value on all sides. ***Keep Exploding At*** (`!N`) will not explode dice where no side is less than `N`. Other safeguards exist to ensure no explosion chain is allowed to run forever.

| Operation | Expression | Interpretation | Example | Meaning | Notes |
| :---: | ---: | :--- | ---: | :--- | :--- |
| ***Explode*** | `dS!` | Roll one die with `S` sides, and if the die rolls `S`, roll another `dS` to the pool. | `d20!` | Roll one `d20` and add another `d20` roll to the pool if the first rolls `20`. | Equivalent to ***Explode At***: `dS!S`. |
| ***Explode At*** | `dS!N` | Roll one die with `S` sides, and if the die rolls higher than or equal to `N`, roll another `dS` to the pool. | `d20!18` | Roll one `d20` and add another `d20` roll to the pool if the first rolls `18` or higher. |  |
| ***Explode With*** | `dS!dT` | Roll one die with `S` sides, and if the die rolls higher than or equal to `N`, roll a `dT` to the pool. | `d20!d4` | Roll one `d20` and add a `d4` roll to the pool if the first rolls `20`. |  |
| ***Keep Exploding*** | `dS!!` | Roll one die with `S` sides, and if the die rolls `S`, roll another `dS` to the pool. If ***that*** die rolls `S`, repeat... | `d20!!` | Roll one `d20` and add another `d20` roll to the pool if the first rolls `20`, and another if ***that*** rolls `20`... | Equivalent to ***Keep Exploding At***: `dS!!S`. |
| ***Keep Exploding At*** | `dS!!N` | Roll one die with `S` sides, and if the die rolls higher than or equal to `N`, roll another `dS` to the pool. If ***that*** die rolls `S`, repeat... | `d20!!18` | Roll one `d20` and add another `d20` roll to the pool if the first rolls `18` or higher, and another if ***that*** rolls `18` or higher... |  |

#### Advantage/Disadvantage

***Advantage*** (`dS+`) lets you treat a roll as if you had rolled it twice, and taken the better roll. Conversely, ***Disadvantage*** (`dS-`) takes the worse roll.

> **NOTE** that this works differently from just rolling twice as many dice with ***Keep High***/***Keep Low***, when rolling more than one die with **Advantage**/**Disadvantage**! `KH`/`KL` will remove the worst/best rolls from the entire pool, whereas **Advantage**/**Disadvantage** treats each roll as a pool of two before proceeding, allowing more good/poor rolls to contribute to the total. In practice, this means that `NdS+` will have more variance and average lower results than `2NdSKHN`, and `NdS-` will have more variance and average higher results than `2NdSKLN`.

| Operation | Expression | Interpretation | Example | Meaning | Notes |
| :---: | ---: | :--- | ---: | :--- | :--- |
| ***Advantage*** | `dS+` | Roll two dice with `S` sides, and take the better roll. | `d20+` | Roll two `d20` and take the better result. | Equivalent to ***Keep Highest***: `2dSKH`. |
| ***Multiple Advantage*** | `NdS+` | Roll two dice with `S` sides, and take the better roll `N` times. | `4d20+` | Roll two `d20` and take the better result, `4` times. | ***NOT*** equivalent to ***Keep Highest***: `2NdSKHN`! See **NOTE** above. |
| ***Disadvantage*** | `dS-` | Roll two dice with `S` sides, and take the worse roll. | `d20-` | Roll two `d20` and take the worse result. | Equivalent to ***Keep Lowest***: `2dSKL`. |
| ***Multiple Disadvantage*** | `NdS-` | Roll two dice with `S` sides, and take the worse roll `N` times. | `4d20-` | Roll two `d20` and take the worse result, `4` times. | ***NOT*** equivalent to ***Keep Highest***: `2NdSKLN`! See **NOTE** above. |

#### Maximize/Minimize

***Maximize*** (`M`) lets you make the highest possible rolls for a given pool. Conversely, ***Minimize*** (`m`) ensures every roll is the lowest possible.

| Operation | Expression | Interpretation | Example | Meaning | Notes |
| :---: | ---: | :--- | ---: | :--- | :--- |
| ***Maximize*** | `dSM` | Roll one die with `S` sides, and assume you rolled `S`. | `d20M` | Ignore the dice roll and assume you rolled a `20`. |  |
| ***Minimize*** | `dSm` | Roll one die with `S` sides, and assume you rolled a `1`. | `d20m` | Ignore the dice roll and assume you rolled a `1`. |  |

### Other Dice

#### Custom Numeric Dice

While `dS` syntax describes a die with `S` sides, with numbers `1`-`S` on those sides, you can in fact model dice with any number of sides, with any values on those sides.

| Die | Expression | Interpretation | Example | Meaning | Notes |
| :---: | ---: | :--- | ---: | :--- | :--- |
| ***Range Die*** | `d[X..Y]` | Roll one die with `|Y - X| + 1` sides, with the integers `Y`, `X`, and all integers in between them on those sides. | `d[-1..1]` | Roll a 3-sided die, with numbers `-1`, `0`, and `1` on those sides. | Equivalent to ***List Die***: `d{-1, 0, 1}`. |
| ***List Die*** | `d{X, Y, Z}` | Roll a die with the integers specified in the list on each side. | `d{1, 1, 100}` | Roll a die with a 2/3 chance of coming up `1`, and 1/3 chance coming up `100`. |  |

#### Alias Dice

Common custom die have shortcut aliases for easier use.

| Die | Expression | Interpretation | Notes |
| :---: | ---: | :--- | ---: | :--- | :--- |
| ***Percent Die*** | `d%` | Roll a `d100` to represent a probabilistic outcome. | Equivalent to ***Roll***: `d100`. |
| ***Standard Fudge Die*** | `dF` | Roll a 3-sided die with values `-1`, `0`, and `1` on the sides. | Equivalent to ***Range Die***: `d[-1..1]`. |
| ***Fudge Die*** | `dFN` | Roll a `2N + 1`-sided die with values between `-S` and `S`, including `0`. | Equivalent to ***Range Die***: `d[-S..S]`. |
