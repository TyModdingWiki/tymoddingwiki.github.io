---
layout: default
title: exe Variables
nav_order: 1
parent: Ty 1
---

# exe Variables
{: .no_toc } 
[//]: <> (This makes it so its not included in the table of contents)

All known variables that are hardcoded in the exe. All offsets are from the newest exe version of Ty (version  1.44)

## Table of contents
{: .no_toc .text-delta }

* TOC
{:toc}

---

## Game Totals Hex Values:

>### Totals Screen
>
>| Variable | Variable Type | Hex Offset | Notes
>| - | - | - | -
>| Opals | int | 0xE6A91 | 
>| Rainbow Scales | int | 0xE6AB6 | Value for the totals screen, make sure to edit the other one for Rainbow Cliffs too
>| Talismans | int | 0xE6ACF | 
>| Cogs | int | 0xE6AE8 | 
>| Bilbies | int | 0xE6B01 | 
>| Thunder Eggs | int | 0xE6B1A | 
>| Frames | int | 0xE6B33 | 

>### Totals for Each Level
>
>| Variable | Variable Type | Hex Offset | Notes
>| - | - | - | -
>| Level Total Opals | int | 0xE5277 | Total amount for all levels
>| RC Rainbow Scales | int | 0xE527C | Value for Rainbow Cliffs, doesn't affect totals screen

Would be nice to have the golden cogs and picture frame values but unfortunately haven't found them yet

---

## Requirements

| Variable | Variable Type | Hex Offset | Notes
| - | - | - | -
| TE Machine Opal Requirement | int | 0x136904 | Requirement for all levels

---

## Level Variables

| Variable | Variable Type | Hex Offset | Notes
| - | - | - | -
| Aurora's Kids Total Count | int | 0xD3947 | Just the amount for the UI