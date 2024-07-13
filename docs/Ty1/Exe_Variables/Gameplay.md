# Gameplay

All known gameplay related variables that are hardcoded in the exe. All offsets are for the newest version of Ty (version  1.44)

---

### Charge Bite Requirement
>
>Charge bites work by having a separate hidden value that counts up for every opal that you collect, when trying to charge bite it checks if the requirement is less than the amount on the hidden counter. 
>After using a charge bite the hidden counter then gets minused by a set amount 
>
>The charge bite is a bit limited with how you can edit it because of it using a SAR ((bit)Shift Arithmetically Right) for dividing, 
>assuming the compiler for the game chose that as it's probably more optimised than using a divide opcode but its more limited with how many possible values it can divide by.
>
>The only possible values with the SAR are:
>
>| SAR Amount of Bits to Shift | Opal Requirement for Charge Bite
>| :-: | :-:
>| 0 | 3.125
>| 1 | 6.25
>| 2 | 12.5
>| 3 | 25
>| 4 | 50
>| 5 | 100
>
>Unfortunately SAR 6 isn't possible as it gives a value of 200 and the amount to minus and charge bite requirement values are both signed bytes which can only go up to 127.
>
>Values below 3 aren't really useful as they're not a whole number. Eg. if you used a SAR value of 2 the first charge bite shown on the UI would be at 13, as the requirement for charge bites needs to be less than the hidden counter, 
the second one would be 12 (total of 25 on the hidden counter), then the next would be 13 (total of 38), next would be 12 (total of 50), etc. The inconsistent amount would make the charge bite requirement and minusing value not match up since its a whole number
>
>The offsets for all the charge bite values are listed below
>
>| Variable | Variable Type | Hex Offset | Notes
>| - | :-: | - | -
>| Amount to Minus After Using Charge Bite | byte | 0x2829D | The amount that gets minused from the hidden counter for the charge bite
>| Charge Bite Requirement | byte | 0x29847 | If you have more than or equal to this amount on the hidden counter the game will let you charge bite
>| Charge Bite UI Opal Glow | byte (SAR) | 0xFB632 | The SAR operation that checks if you have enough on the hidden counter to show the brighter glow around the opal
>| Display Charge Bite Amount | byte (SAR) | 0xFB82E | Same as the glow one but shows the number for how many charge bites you have (See the value below to edit the count in the UI)
>| Max Charge Bites Displayed | int | 0xFC8A8 | By default this is 9, just documenting this even though couldn't ever really edit the requirement to make it have more than 9
>| Charge Bite Count | byte (SAR) | 0xFC8AE | This is the SAR that will count the charge bites for the count on the UI
>
>Last Value for the charge bite is related to the -tydev and -eadev launch options, these will set the amount of charge bites you have with them
>
>| Variable | Variable Type | Hex Offset
>| - | :-: | - 
>| -tydev Charge Bite Amount | int | 0x10C62C 
>| -eadev Charge Bite Amount | int | 0x10C657 

---

## Level Variables

| Variable | Variable Type | Hex Offset | Notes
| - | :-: | - | -
| Aurora's Kids Total Count | int | 0xD3947 | Just the amount for the UI, the amount for the actual objective is counted from the amount of kids present in the lv2

---

## Boomerangs

Most of the values for boomerangs are in the global.model file

| Variable | Variable Type | Hex Offset | Notes
| - | :-: | - | -
| Doomerang Duration | float | 0x1F95AC

---