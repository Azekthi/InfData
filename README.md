# InfData
This is a repository for collecting aircraft data from *Ace Combat Infinity*, a free-to-play PlayStation 3 game developed by Bandai Namco Entertainment.

Forked from the original at https://github.com/InfBuild/InfData

## File Format

```
Column Name 1	Column Name 2	Column Name 3
Foo	0.5?	Bar,Baz
```

Each row is a new item (aircraft, mission, etc.) and each column is separated by tab characters. The first row is the header with the column names.

A question mark `?` after a value indicates that value is indeterminate.  
Please keep in mind that calculations performed with these values may not be entirely accurate.

Commas `,` can be used to separate multiple values in a single column.

Please refer below for explanations of each file and their columns.

### AircraftList
Aircraft information.

* `ID`
  A unique numerical value to refer to the aircraft.
* `Name`
  The aircraft's name.
* `Role`
  The aircraft's role. Can be `F`, `M`, `A`, `B`, or `PF` (Fighter, Multirole, Attacker, Bomber, Piston Fighter, respectively).
* `Base Cst.`
  The aircraft's base Cst value as listed in game.  
  When calculating attack power, the base Cst is rounded up to the nearest 50.  
  (examples: 525->550; 675->700)
* `Handicap`
  A value used to correct an aircraft's attack power.
* `Main`
  The aircraft's main weapon. If this is left blank, `MSL` is used by default.
* `SP.W 1`, `SP.W 2`, `SP.W 3`
  The aircraft's first, second, and third special weapons.
* `BODY`, `ARMS`, `MISC`
  The aircraft's BODY, ARMS, and MISC part slots at Lv.1.
* `Mod Cost`
  A value to calculate the price of equipping parts onto the aircraft.  
  Based on the price of equipping Enhanced Engine Nozzle S to the aircraft, or double the price of switching the aircraft's Datalink.

### AircraftCstTableList
A table used to calculate an aircraft's Cst. Any aircraft's Cst can be calculated with the below formula:
```
BaseCst +
  max(0, table["2-10"] * min(Lv - 1, 9)) +
  max(0, table["11-15"] * min(Lv - 10, 5)) +
  max(0, table["16"] * min(Lv - 15, 1)) +
  max(0, table["17-"] * (Lv - 16))
```

* `Name/Cst.`
  The target aircraft name or the target aircraft Base Cst. The following incremental Cst values are added to each level of the corresponding aircraft.
* `2-10`
  The value at which the Cst rises for Lv.2–10.
* `11-15`
  The value at which the Cst rises for Lv.11–15.
* `16`
  The value at which the Cst rises for Lv.16.
* `17-`
  The value at which the Cst rises for Lv.17–20.

### SpecialWeaponList
Standard and special weapon information.

* `ID`
  A unique numerical value to refer to the weapon.
* `Name`
  The weapon's name.
* `Role`
  The weapon's role. Must be one of: `A` (Anti-Air), `G` (Anti-Ground), or `O` (Other).
* `Category`
  The weapon's type. See the table for examples.
* `Air F`, `Air M`, `Air A`, `Air B`, `Air PF`
  A damage multiplier when this weapon is used against air targets when equipped by a Fighter, Multirole, Attacker, Bomber, or Piston Fighter. Leave the columns blank for the aircraft roles that cannot equip this weapon.
* `Ground F`, `Ground M`, `Ground A`, `Ground B`, `Ground PF`
  A damage multiplier when this weapon is used against ground targets when equipped by a Fighter, Multirole, Attacker, Bomber, or Piston Fighter. Leave the columns blank for the aircraft roles that cannot equip this weapon.
* `Strong Multiplier`
  A damage multiplier when this weapon is used against targets it is strong against.
* `Weak Divider`
  A damage divider when this weapon is used against targets it is weak against.
* `Max Simultaneous Attacks`
  The maximum number of times this weapon can be fired simultaneously.
* `Initial Power`
  A value used to calculate the weapon's damage at Lv.1.
* `Power Increment`
  The value at which the weapon's damage increases by with each level.
* `Fixed Base Cst.`
  If the weapon uses a special Base Cst value for damage calculation instead of the aircraft's Base Cst, list it here.
* `Related Damage`
  If the weapon has multiple stages of attack (ex: the MPBM's shockwave), this refers to the weapon name of the next successive attack stage.
* `Cst.`
  The weapon's Cst values for all of its levels, separated by commas `,`.

### PartsList
Aircraft part information.

* `ID`
  A unique numerical value to refer to the part.
* `Name`
  The part's name in Japanese.
* `English Name`
  The part's name in English.
* `Cst.`
  The part's Cst value.
* `Category`
  A classification for the part.
* `Group`
  A group identifier. Only one part from a group can be equipped at any time.
* `SP.W`
  The special weapons the part affects. The part can only be equipped if one of its corresponding special weapons is equipped. If left blank, the part can be equipped regardless of special weapon.
* `Role`
  The aircraft roles the part is restricted to. If left blank, the part can be equipped by any aircraft.
* `Slot`
  The slot category the part is equipped to: `BODY`, `ARMS`, or `MISC`.
* `Slot Usage`
  The number of slots the part consumes.
* `Power`
  A damage multiplier that is applied when the part is equipped.
* `Hits`
  The number of additional hits added to the corresponding weapon's Max Simultaneous Attacks when the part is equipped.

### DataLink
Datalink bonus information.

* `Name`
  The datalink's Japanese name.
* `English Name`
  The datalink's English name.
* `Cst.`
  The datalink's Cst before version 2.09.  
  As of version 2.09 released on November 18, 2015, datalinks no longer add Cst. 

### EnemyList
Enemy unit information.

* `Name`
  The enemy unit's name.
* `Role`
  An indicator of whether the enemy is an air enemy `A` or a ground enemy `G`.
* `Color`
  The enemy's color on the radar. Must be `Y` (Yellow), `O` (Orange), `R` (Red), or `TGT`.
* `Score`
  The number of points the enemy is worth.
* `HP`
  The enemy's endurance.
* `Soft Target`
  If this is set to `TRUE`, the weapon multiplier for the Fighter role is used regardless of the player's aircraft.
* `Hard Multiplier`
  An endurance multiplier the enemy receives on HARD missions. If blank, the default is `1.2`.
* `Weakness`
  A list of weapons the enemy is weak to, separated by commas `,`.
* `Strongness`
  A list of weapons the enemy is strong against, separated by commas `,`.
* `Stages`
  A list of missions the enemy appears in, separated by commas `,`. If a normal mission is listed, its HARD variant is therefore implied.

### StageList
Mission information.

* `ID`
  A unique numerical value to refer to the mission.
* `Key`
  An abbreviation of the mission's name, to be used for HARD missions and the [EnemyList](#enemylist) table.
* `Name`
  The mission's full name.
* `HARD`
  If set to `TRUE`, indicates that this mission is a HARD variant.
* `Original`
  If `HARD` is set to `TRUE`, the key of the original version of this mission.
* `Special Raid`
  If set to `TRUE`, indicates that this mission is a Special Raid.


## Special Thanks
This data could not be collected without the cooperation of many people. Thanks to:
* the blog owner of [Berkut Method](http://berkut.blog.jp/) who discovered the underlying data calculations
* mfakane for creating the original repo and bringing all of this data to the community
* Tukimi Rina for helping on data collection and calculation
* everyone who used and borrowed this data and the original website to keep it alive and updated
* members of the Ace Combat Reddit Discord server for further data collection

## License
[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed.ja)  
The files and data included in both the original InfData repo and this fork are released under the CC0 license.  
Anyone can use this information freely.

## Contact Information
Azekthi <<https://twitter.com/Azekthi>>

[Click here for the original repo by mfakane.](https://github.com/InfBuild/InfData)
