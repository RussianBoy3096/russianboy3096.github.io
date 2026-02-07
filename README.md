# CaesarLibrary Documentation

**CaesarLibrary** is a framework for creating and adding custom content to Gladihoppers mods.

It provides structured systems for registering weapons, armor pieces, shields, and other equipment, allowing modders to expand the game without rewriting core logic.

**AbsoluteRoyal** (also known as Absolute Royality, or Royalhoppers) serves as a live example of a mod built using CaesarLibrary.

This documentation focuses on how to use CaesarLibrary to create your own items and integrate them into the game.

---

## What is CaesarLibrary?

CaesarLibrary is designed to:

- Provide reusable item creation systems
- Standardize how equipment is registered
- Support JSON-based content loading
- Reduce recompilation when tweaking assets
- Enable easier collaboration between modders

Instead of hardcoding every item in C#, you can define them in external `.json` files and load them dynamically.

---

## Framework Structure

Typical mod setup:

```
Mods/
|
|- CaesarLibrary.dll
|- Newtonsoft.Json.dll
|- YourMod.dll
|
|-- CaesarLibrary_Assets/
|-- Weapons.json
|-- Helmets.json
|-- Armors.json
|-- Shields.json
|-- Gloves.json
|-- Pants.json
|-- Shoes.json
```

Your mod reads from these JSON files and registers items through CaesarLibrary.

---

## Creating Items via JSON

Each equipment category has its own JSON file.

Example: `Helmets.json`

```json
[
  {
    "baseID": 29,
    "name": "Spartan Helmet",
    "price": 0,
    "armor": 16,
    "sprite": "spartan_helmet",
    "pivotFromID": 30,
    "offsetY": -10,
    "offsetX": 1
  }
]
```

When the mod loads:

1. JSON is read from disk
2. Entries are deserialized
3. CaesarLibrary registers each item

No recompilation required; just edit, save, restart the game.

**Field Reference** (helmet example)

| Field | Type | Description |
| ----- | ---- | ----------- |
| baseID | int |	Base game item used as template |
| name |	string |	Display name |
| price |	int |	Career mode shop price |
| armor |	int |	Armor (RESistance) value |
| sprite |	string |	Sprite asset name (must be only the name, the library already adds the .png extension) |
| pivotFromID	| int |	Reference pivot source (the id of the item this new item should copy its pivot from) |
| offsetY |	int |	Vertical sprite offset (in pixels) |
| offsetX |	int |	Horizontal sprite offset (in pixels) |

Other equipment types use similar schemas with minor variations.

---

## AbsoluteRoyal Example

AbsoluteRoyal demonstrates how to:
* Load JSON files
* Register custom equipment
* Apply sprite pivots and offsets
* Structure a CaesarLibrary-based mod
Use it as a reference implementation when building your own content.

---

## Recommendations
* When creating an armor piece (designing or drawing it), it's recommended that the sprite has the same width that any piece of armor of the same type that already exists in the game.
For example, many helmets have a 14px width, so it's recommended to work with that width. This is used to make a pixel-perfect placing more easy to achieve. The pivot system is still a work in progress, so it will improved to the point you don't really have to be careful with it anymore.

---

## Future Plans

Planned CaesarLibrary expansions include:
* Full support for Arcade Game Mode (changing the hordes, enemies, and more)
* Full support for Spartacus War (changing units, factions, and eventually even the map itself!)
* Advanced pivot inheritance
* Modular asset system

---

## Contributing / Community

The goal is to make Gladihoppers modding more accessible.
Artists, designers, and coders can collaborate by sharing JSON configs and sprite sheets without touching core code.
A public Discord server is planned for support and collaboration.

---

### Thanks to
**Pekka11208**: brotha u draw pretty damn well, you already made many sick sprites for many parts of my mods just because you wanted to, truly our goat

**aNtlers (AKA Anders Lundbjork)**: for making Gladihoppers, of course

**Dreamon Studio Discord Community**: for being there, giving out suggestions, ideas and feedback.

**Credits**

Framework: Russ (AKA Vastrael)
CaesarLibrary and Royalhoppers: Russ

