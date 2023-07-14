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

To Do: Check variable type

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
>| Opals | Short? | 0xE6A91 | Could potentially be a int
>| Thunder Eggs | Byte? | 0xE6B1A | Could potentially be a int
>| Talismans | Byte? | 0xE6ACF | Could potentially be a int
>| Cogs | Byte? | 0xE6AE8 | Could potentially be a int
>| Bilbies | Byte? | 0xE6B01 | Could potentially be a int
>| Frames | Short? | 0xE6B33 | Could potentially be a int

>### Totals for Each Level
>
>| Variable | Variable Type | Hex Offset | Notes
>| - | - | - | -
>| Level Total Opals | int | 0xE5277 | Total amount for every level
>| Total Rainbow Scales | int | 0xE527C | 

---

## Requirements

| Variable | Variable Type | Hex Offset | Notes
| - | - | - | -
| TE Machine Opal Requirement | int | 0x136904 | Requirement for all levels

---

## Level Variables

| Variable | Variable Type | Hex Offset | Notes
| - | - | - | -
| Aurora's Kids Total Count | int | 0xD3947 | 