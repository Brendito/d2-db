# Diablo 2 Item Database

WIP Database of Diablo 2 Items
All data is taken from Arreat Summit
http://classic.battle.net/diablo2exp

I do not own this data

## Structure

- basic

  - normal | exceptional | elite
    - armor
      - helm
      - armor
      - shield
      - glove
      - boot
      - belt
      - class
        - barbarian
          - helm
        - druid
          - helm
        - paladin
          - shield
        - necromancer
          - shield
    - weapon
      - axe
      - bow
      - crossbow
      - dagger
      - javelin
      - mace
      - polearm
      - scepter
      - stave
      - sword
      - thrown
      - wand
      - class
        - amazon
          - bow
          - spear
          - javelin
        - assassin
          - katar
        - sorceress
          - orb

- unique

  - normal | exceptional | elite
    - armor
      - helm
      - armor
      - shield
      - glove
      - boot
      - belt
      - class
      - barbarian
        - helm
      - druid
        - helm
      - paladin
        - shield
      - necromancer
        - shield
    - weapon
      - axe
      - bow
      - crossbow
      - dagger
      - javelin
      - mace
      - polearm
      - scepter
      - stave
      - sword
      - thrown
      - wand
      - class
      - amazon
        - bow
        - spear
        - javelin
      - assassin
        - katar
      - sorceress
        - orb

- set

  - set_name
    - items
      - set_item_1
      - set_item_2
      - ...etc

- gems
  .... to be defined
- runes
  ... to be defined
- runewords
  ... to be defined

## JSON Schema

- Entries have their spaces replaced with underscores, example "Skull Cap" -> skull_cap.
- Attributes are camelCase.

### Base JSON

Core item classification found in every entry

```json
{
  "item_id": {
    "name": "Display Name of Item",
    "itemClass": "armor | weapon | charm | socketable | jewelery",
    "itemType": "helm | armor | shield | glove | boot | belt | axe | bow | crossbow | dagger | javelin | mace | polearm | scepter | spear | stave | sword | thrown | wand | small | large | grand | ring | amulet | gem | rune | jewel",
    "quality": "normal | exceptional | elite | chipped | flawed | flawless | perfect",
    "rarity": "basic | magic | rare | unique | set",
    "requirements": {
      "str | dex | lvl": 0,
    },
    "durability": 0,
    "qlvl": 0,
    "imageUrl": "imageUrl",
    "versions": {
        "normal | exceptional | elite | chipped | flawed | flawless | perfect | unique | set" : "comma.delimeted.path.to.item.entry
    }
  }
}
```

### Armor JSON

```json
{
  "item_id": {
    "name": "Display Name of Item",
    "itemClass": "armor",
    "itemType": "helm | armor | shield | glove | boot | belt",
    "quality": "normal | exceptional | elite",
    "rarity": "basic | unique | set",
    "defense": {
      "min": 0,
      "max": 0
    },
    "requirements": {
      "str | dex | lvl": 0,
      "class": "barbarian | druid | necromancer | paladin"
    },
    "durability": 0,
    "sockets": 0,
    "qlvl": 0,
    "imageUrl": "imageUrl",
    "versions": {
      "normal | exceptional | elite |  unique | set": "comma.delimeted.path.to.item.entry"
    },
    // itemType === armor | shield
    "weight": "light | medium | heavy",
    // itemType === shield
    "blockChance": 0,
    "smiteDamage": {
      "min": 0,
      "max": 0
    },
    // itemType === boot
    "kickDamage": {
      "min": 0,
      "max": 0
    },
    // itemType === belt
    "slots": 0
  }
}
```

### Weapon JSON

```json
{
  "item_id": {
    "name": "Display Name of Item",
    "itemClass": "weapon",
    "itemType": "axe | bow | crossbow | dagger | javelin | mace | polearm | scepter | spear | stave | sword | thrown",
    "quality": "normal | exceptional | elite",
    "rarity": "basic | unique | set",
    "requirements": {
      "str | dex | lvl": 0,
      "class": "barbarian | druid | necromancer | paladin"
    },
    "range": 0,
    "durability": 0,
    "sockets": 0,
    "weaponSpeed": 0,
    "qlvl": 0,
    "imageUrl": "imageUrl",
    "versions": {
      "normal | exceptional | elite |  unique | set": "comma.delimeted.path.to.item.entry"
    },
    // one-hand / two hand
    "oneHandDamage | twoHandDamage": {
      "min": 0,
      "max": 0
    },

    // itemType === thrown | javelin
    "throwDamage": {
      "min": 0,
      "max": 0
    },

    // itemType === wand
    "affixes": ["50% Damage to Undead"]
  }
}
```

### Unique Items

```json
{
  "item_id": {
    // ...item class JSON
    "rarity": "unique",
    "baseName": "Name of Base Item",
    "baseItem": "comma.delimited.path.to.baseItem",
    "affixes": [
      "String array of affixes",
      "Only affixes without variations",
      "Example: +20 Strength"
    ],
    "variedAffixes": [
      {
        "affix": "Description of affix",
        "min": 0,
        "max": 0
      },
      //   Example
      {
        "affix": "% Enhanced Damage",
        "min": 170,
        "max": 220
      }
    ]
  }
}
```

### Set JSON

```json
{
  "aldurs_watchtower": {
    "name": "Aldur's Watchtower",
    "partialSetBonus": [
      {
        "items": 2,
        "affixes": ["150% Bonus to Attack Rating"]
      },
      {
        "items": 3,
        "affixes": ["50% Better Chance Of Geting Magic Items"]
      }
    ],
    "completeSetBonus": [
      "+3 To Druid Skills",
      "+350% Enhanced Damage",
      "150% Bonus To Attack Rating",
      "50% Better Chance Of Getting Magic Items",
      "10% Mana Stolen Per Hit",
      "All Resistances +50",
      "+150 Defense",
      "+150 To Mana",
      "Display Aura"
    ],
    "items": {
      "aldurs_stony_gaze": {
        // ...baseItem
        "rarity": "set",
        "setName": "Aldur's Watchtower",
        "set": "comma.delimited.path.to.set",
        "baseName": "Name of Base Item",
        "baseItem": "comma.delimited.path.to.baseItem",
        "affixes": [
          "String array of affixes",
          "Only affixes without variations",
          "Example: +20 Strength"
        ],
        "variedAffixes": [
          {
            "affix": "Description of affix",
            "min": 0,
            "max": 0
          },
          //   Example
          {
            "affix": "% Enhanced Damage",
            "min": 170,
            "max": 220
          }
        ],
        "setBonuses": [
          {
            "items": 2,
            "affixes": ["+15 To Energy"]
          },
          {
            "items": 3,
            "affixes": ["+15 To Energy"]
          },
          {
            "items": "Complete Set",
            "affixes": ["+15 To Energy"]
          }
        ]
      },
      "aldurs_advance": {
        /// ...etc
      }
    }
  }
}
```
