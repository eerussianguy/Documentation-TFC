---
layout: page
title: "Ingredients"
permalink: /1.18.x/data/ingredients/
---

# Ingredients

An ingredient represents an input to a recipe or other piece of data. All vanilla and modded recipes should support ingredients and can use any of the following ingredients. It must be a JSON object with one of the following keys:

1. An `item` key with the registry name of an item.
2. A `tag` key with the registry name of an item tag.
3. A `type` key with the name of a custom ingredient type.

In addition to the two ingredients added by Minecraft, TFC adds a number of custom ingredients which can be used anywhere an `Ingredient` is required, even by other mod's recipes. TFC adds the following ingredient types:

- [Not Rotten](#not-rotten)
- [Has Trait](#has-trait)
- [Lacks Trait](#lacks-trait)
- [Heatable](#heatable)
- [Not](#not)
- [Fluid Item](#fluid-item)

<hr>

## Not Rotten

This is an ingredient which only accepts food items if they are not rotten. It has the following fields:

- `type`: `tfc:not_rotten`
- `ingredient`: An optional [Ingredient](../ingredients/), to which this is applied. If omitted, this will accept **all** non-rotten items.

#### Example:

```jsonc
// An ingredient which only accepts non-rotten minecraft:steak
{
    "type": "tfc:not_rotten",
    "ingredient": { "item": "minecraft:steak" }
}
```

<hr>

## Has Trait

This is an ingredient which only accepts food items if they have a specific trait. It has the following fields:

- `type`: `tfc:has_trait`
- `trait`: String. The registry name of a [Food Trait](../common-types/#food-traits) which must be present.
- `ingredient`: An optional [Ingredient](../ingredients/), to which this is applied. If omitted, this will accept **all** items with the provided trait.

#### Example

```jsonc
// An ingredient which only accepts a brined tfc:food/apple
{
    "type": "tfc:has_trait",
    "trait": "tfc:brined",
    "ingredient": { "item": "tfc:food/apple" }
}
```

<hr>


## Lacks Trait

This ingredient is the same as [Has Trait](#has-trait) but is inverted. It tests if a food lacks a specified trait.

- `type`: `tfc:lacks_trait`
- `trait`: String. The registry name of a [Food Trait](../common-types/#food-traits) which must be present.
- `ingredient`: An optional [Ingredient](../ingredients/), to which this is applied. If omitted, this will accept **all** items with the provided trait.

#### Example

```jsonc
// An ingredient which only accepts a tfc:food/apple which has not been brined
{
    "type": "tfc:lacks_trait",
    "trait": "tfc:brined",
    "ingredient": { "item": "tfc:food/apple" }
}
```

## Heatable

This is an ingredient which only accepts items if they are heatable, and optionally currently within a certain temperature range. It has the following fields:

- `type`: `tfc:heatable`
- `min_temp`: Optional integer. The minimum temperature this item must have, in degrees Celsius. Defaults to accepting any temperature.
- `max_temp`: Optional integer. The maximum temperature this item must have, in degrees Celsius. Defaults to accepting any temperature.
- `ingredient`: An optional [Ingredient](../ingredients/), to which this is applied. If omitted, this will accept **all** items with the provided heat.

#### Example

```jsonc
// An ingredient which only accepts minecraft:iron_ingots if they are heated between 300 and 400 C
{
    "type": "tfc:heatable",
    "min_temp": 300,
    "max_temp": 400,
    "ingredient": { "item": "minecraft:iron_ingot" }
}
```

<hr>

## Not

An ingredient which inverts an existing ingredient. It has the following fields:

- `type`: `tfc:not`
- `ingredient`: An optional [Ingredient](../ingredients/), to which this is applied. If omitted, this will accept **any** item.

#### Example

```jsonc
// An ingredient which accepts ANY rotten food
{
    "type": "tfc:not",
    "ingredient": {
        "type": "tfc:not_rotten"
    }
}
```

<hr>

## Fluid Item

An ingredient which expects an item to contain a fluid (such as a bucket). It has the following fields:

- `type`: `tfc:fluid_item`
- `ingredient`: An optional [Ingredient](../ingredients/), to which this is applied. If omitted, this will accept **any** item.
- `fluid_ingredient`: A [Fluid Stack Ingredient](../common-types/#fluid-stack-ingredients), which must match the fluid contained in the item.

```jsonc
// An ingredient which accepts a ceramic jug containing fresh water
{
    "type": "tfc:fluid_item",
    "ingredient": { "item": "tfc:ceramic/jug" },
    "fluid_ingredient": {
        "amount": 100,
        "ingredient": { "fluid": "minecraft:water" }
    }
}
```
