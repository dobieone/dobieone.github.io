## Character Health Calculations

When you look at a lot of games the player character will have a Health bar. A lot of games will increase the health when you level up. What if your equipment had modifiers that allowed you to increase your max health by wearing an item. How do you manage the equipping/removing of an item with this modifier.

When you read a lot of implementations online and especially tutorials for Unity a lot of them have one thing in common - they all have a component that manages health disconnected from the rest of the systems. It allows you to "damage" the character (I am assuming that the component is attached to a character and not some other "thing"). The component does not allow for changes in level or modifiers. They tend to be very simple.

This is one solution I came up with...

We don't store the actual health, we store the maximum and the amount of damage taken. Then when we apply a modifier we calculate the new Maximum Health using the Base Max Health. The apply the amount of Damage that has been taken to get the Current Health.

_All code is Pseudocode and will not run_

### Variables

```
var BaseMaxHealth = 100         // The unmodified base for the maximum health value
var MaxHealth = 100             // The maximum health value after modifiers have been applied
var DamageTaken = 0             // The amount of damage that this character has taken

var CurrentHealth = MaxHealth   // The health this character current has
```

### Methods

```
func Damage(amount)
    DamageTaken + amount
    if DamageTaken >= MaxHealth
        NotifyDead
```

```
func Heal(amount)
    DamageTaken - amount
    Clamp(DamageTaken, 0)
```

```
func SetMax(amount)
    BaseMaxHealth + amount
    CalculateMaxHealth
```

```
func CurrentHealth  
    CalculateMaxHealth
    return CurrentHealth
```

```
func CalculateMaxHealth
    Modifiers = GetHealthModifiers 
    Max = BaseMaxHealth

    ForEach Modifier in Modifiers
        Max + Modifier

    MaxHealth = Max
    CurrentHealth = MaxHealth - DamageTaken
```

### Events

Possible events that could be implemented

* Monitor Modifiers for one being added that would changed Health
* Notify listeners of any change to Health

