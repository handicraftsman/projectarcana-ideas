
# Project Arcana

## Core idea

Player CANNOT get stronger, instead he/she adapts to the current situation and own skills.

## Health

As this is based on Minecraft mechanics, player has 20 HP, actually represented as a float in game.

## Energy

Player has 20 energy points to be used by forms, abilities and skills.

## Attributes

There are 6 stats and 6 affinities, called attributes in general.  
Every attribute starts with level 1 and can be raised to level 7.

At level 2 character gains a minor ability or skill which gets empowered up to level 7.  
At level 4 character gains a special ability or skill which gets empowered up to level 7.  
At level 7 character gains an ultimate ability or skill.

## Point distribution

Player can have a number power points to be invested into attributes.

Player has 6 charge points to be invested into power points. Using charge points drains energy.  
Player also has 6 life points to be invested into power points. Using them drains health.

Once player runs out of energy or health to maintain invested charge or life points,
all player forms and abilities get disabled and all invested points return as charge and life points.

Once player runs out of health, he/she actually dies. That should not be changed.

Non-natural player attributes should consume extra energy on use.  
Completely redestributing attributes should also consume health.

## Stats

* Strength
  Affects:
  * Damage dealt to others
  * General character size
* Dexterity
  Affects:
  * Character speed
  * Character height
  * Chance of dodging an attack
* Constitution
  Affects:
  * Damage taken
  * Character width
* Intelligence
  Affects:
  * Chance of ignoring an attack
  * General error amount in forms, skills and spells
  * Amount and frequency of aura particles
* Willpower
  Affects:
  * General skill and ability power
  * Aura speed and density
* Spirit
  Affects:
  * Energy consumption
  * Aura size

## Affinities

Every affinity point also increases amount of damage taken and dealt

* Fire
  Effects:
  * lvl2+:
    Melee: Fire punch - sets entities on fire
  * lvl4+:
    Aura: Blazing aura - sets entities on fire, at lvl7 also ignites blocks
  * lvl7:
    Aura: Blue flames
    Ability (Melee): Increased fire damage, entities burn until they die
* Water
  * lvl2+:
    Melee: Suffocating punches - makes minecraft treat target as in water for a while
  * lvl4+:
    Aura: Water bubbles aura - suffocates nearby entities and decreases their speed
  * lvl7: Ice
    Aura: Snow aura, overrides bubbles effects. Decreases entity speed and deals damage to them.
* Earth
  * lvl2+:
    Melee: Increased damage
  * lvl4+:
    Aura: slightly shakes image for everybody except for user, floating dirt particles around as an extra visual effect
  * lvl7:
    Skill (Melee): rock fist
* Air
  * lvl2+:
    Melee: extra knockback
  * lvl4+:
    Aura: wind effects and aura speed increase
  * lvl7+:
    Aura: pushes everybody around with wind gusts
* Lightning
  * lvl2+:
    Melee: deals extra damage for water-aligned entities and entities in water
  * lvl4+:
    Aura: Lightning effects, high aura speed, instant transmission to desired point in field of view with a cooldown
  * lvl7+:
    Aura: electrocuting sparks everywhere
* Light
  * lvl4+:
    Aura: simple very slow light aura, increases dodge chance
  * lvl7+:
    Ability (Aura):  
      No aura at all  
      On every attack: cancels it and deals one in response if target entity does not cancel damage too

## Forms
Form is described using a simple text script which configures how points should be redistributed.  
Form can be configured to have power levels.

A simple form script which invests into light, lightning and fire:

```
leveled $level 0 36 # This much points can be distributed between attributes
var $light $lightning $fire # We will use these variables
split $level $light $lightning $fire # Split points in first arguments between variables in next arguments

from all !light !lightning !fire # Take points from all attributes, use charge and life points, but do not touch these 3 elements
take $level # Actually consume points so they are available to the form
invest light $light lightning $lightning fire $fire # Actually invest points
```

Such a script can be compiled to a simple data structure like this:

```json
{
  "variables": {
    "$level": "<current form level>",
    "$light": 0,
    "$lightning": 0,
    "$fire": 0 
  },
  "split": [
    {"what": "$level", "between": ["$light", "$lightning", "$fire"]}
  ],
  "from": [
    "<here all attributes except for light, lightning and fire are listed>"
  ],
  "invest": [
    {"what": "$light", "into": "light"},
    {"what": "$lightning", "into": "lightning"},
    {"what": "$fire", "into": "fire"},
  ]
}
```

## Skills

Skills are simple text scripts too, like the one below:


<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGl0bGU6IFByb2plY3QgQXJjYW5hXG
5hdXRob3I6IE5pY2tvbGF5IElseXVzaGluXG5leHRlbnNpb25z
OlxuICBwcmVzZXQ6IGdmbVxuIiwiaGlzdG9yeSI6Wy0xNDYyND
EyMDA3XX0=
-->