# Collectables

All known collectable related variables that are hardcoded in the exe. All offsets are for the newest version of Ty (version  1.44)

---

### Totals Screen
>
>| Variable | Variable Type | Hex Offset | Notes
>| - | :-: | - | -
>| Opals | int | 0xE6A91 | 
>| Rainbow Scales | int | 0xE6AB6 | Value for the totals screen, make sure to edit the other one for Rainbow Cliffs too
>| Talismans | int | 0xE6ACF | 
>| Cogs | int | 0xE6AE8 | 
>| Bilbies | int | 0xE6B01 | 
>| Thunder Eggs | int | 0xE6B1A | 
>| Frames | int | 0xE6B33 | 

### Totals for Each Level
>
>| Variable | Variable Type | Hex Offset | Notes
>| - | :-: | - | -
>| Level Total Opals | int | 0xE5277 | Total amount for all levels
>| RC Rainbow Scales | int | 0xE527C | Value for Rainbow Cliffs, doesn't affect totals screen

Would be nice to have the max golden cogs value but unfortunately haven't found them yet

## Requirements

| Variable | Variable Type | Hex Offset | Notes
| - | :-: | - | -
| TE Machine Opal Requirement | int | 0x136904 | Requirement for all levels

## Picture Frames

Picture frames work quite differently from the other variables, their IDs get kept track of per level, and counted in a unique way. 
They all get counted from the address assigned in the LEA(load effective address) up until the address ebp -20, except for the bonus levels which work a bit differently, they instead count up until address ebp -136.

Increasing the amount of per level isn't fully possible but can be done with some trickery, decreasing the amount per level is much easier though, custom code or figuring out how to shuffle values around for each level without crashing would really help with being able to increase them

To edit which picture frames are assigned to which level just edit the ID at the offset, its even possible to have 2 levels have the same ID.

To `lower` the amount per level just go to the LEA offset and change the value to a lower variable pointer address, eg. if you wanted to change Rainbow cliffs to have 7 picture frames instead of 9 you would change the LEA from -52, to -44.
Also keep in mind which variables will be cut off from lowering the amount and reassign the IDs as needed.

`Increasing` the amount of IDs is a bit more complex and quite limited, it requires setting a level that is assigned IDs before another level (all the levels below are ordered) to have the same amount or less than the usual amount the next level would have.
eg. setting Rainbow cliffs LEA to -44 you can then set Two ups LEA up to -52 and use IDs at address -52 and -48 where Rainbow cliffs sets them for Two up as they have already been assigned a value and are no longer being used for Rainbow cliffs. 
This will then make Rainbow cliffs have 7 IDs and Two up have either 8 or 9.

But for something like Lyre Lyre which only has 5 and the level before it, snow worries, has 24, you would need to lower snow worries down to at least 5 IDs to then be able to add new unique IDs to Lyre to not have any overlap between the two levels

You could even go across multiple levels to increase the amount of ID, eg. could set Rainbow Cliffs and Two up to 6 frames, to then be able to increase the amount in Walk in the Park up to 9, just keep in mind you would need to set the ID at -44 with Two Ups addresses

To `disable` picture frames showing on the totals screen for a level just change the LEA to -16 (F0).

Below is offsets for each picture frame ID (all IDs are ints), the levels they are assigned to by default, and the pointer address for the local variable the IDs are located by default (reference for editing the LEA opcode)

### Rainbow Cliffs (Z1)

Total frames: 9

>LEA Value Offset: 0x210E

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 0 | 0x2107 | ebp -52
| 1 | 0x2112 | ebp -48
| 2 | 0x211f | ebp -44
| 3 | 0x2126 | ebp -40
| 4 | 0x212d | ebp -36
| 5 | 0x2134 | ebp -32
| 6 | 0x213b | ebp -28
| 7 | 0x2142 | ebp -24
| 8 | 0x2149 | ebp -20

### Two Up (A1)

Total frames: 7

>LEA Value Offset: 0x21D7

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 9 | 0x21d0 | ebp -44
| 10 | 0x21db | ebp -40
| 11 | 0x21e3 | ebp -36
| 12 | 0x21ea | ebp -32
| 13 | 0x21f1 | ebp -28
| 14 | 0x21f8 | ebp -24
| 15 | 0x21ff | ebp -20

### Walk in the Park (A2)

Total frames: 6

>LEA Value Offset: 0x2242

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 16 | 0x223b | ebp -40
| 17 | 0x2246 | ebp -36
| 18 | 0x224e | ebp -32
| 19 | 0x2255 | ebp -28
| 20 | 0x225c | ebp -24
| 21 | 0x2263 | ebp -20

### Ship Rex (A3)

Total frames: 9

>LEA Value Offset: 0x22F7

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 22 | 0x2291 | ebp -52
| 23 | 0x2298 | ebp -48
| 24 | 0x229f | ebp -44
| 25 | 0x22a6 | ebp -40
| 26 | 0x22ad | ebp -36
| 27 | 0x22b4 | ebp -32
| 28 | 0x22bb | ebp -28
| 29 | 0x22c2 | ebp -24
| 30 | 0x22c9 | ebp -20

### Bridge on the River Ty (B1)

Total frames: 20

>LEA Value Offset: 0x2341

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 31 | 0x233a | ebp -96
| 32 | 0x2345 | ebp -92
| 33 | 0x234d | ebp -88
| 34 | 0x2354 | ebp -84
| 35 | 0x235b | ebp -80
| 36 | 0x2362 | ebp -76
| 37 | 0x2369 | ebp -72
| 38 | 0x2370 | ebp -68
| 39 | 0x2377 | ebp -64
| 40 | 0x237e | ebp -60
| 41 | 0x2385 | ebp -56
| 42 | 0x238c | ebp -52
| 43 | 0x2393 | ebp -48
| 44 | 0x239a | ebp -44
| 45 | 0x23a1 | ebp -40
| 46 | 0x23a8 | ebp -36
| 47 | 0x23af | ebp -32
| 48 | 0x23b6 | ebp -28
| 49 | 0x23bd | ebp -24
| 50 | 0x23c4 | ebp -20

### Snow Worries (B2)

Total frames: 24

>LEA Value Offset: 0x2407

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 51 | 0x2400 | ebp -112
| 52 | 0x240b | ebp -108
| 53 | 0x2413 | ebp -104
| 54 | 0x241a | ebp -100
| 55 | 0x2421 | ebp -96
| 56 | 0x2428 | ebp -92
| 57 | 0x242f | ebp -88
| 58 | 0x2436 | ebp -84
| 59 | 0x243d | ebp -80
| 60 | 0x2444 | ebp -76
| 61 | 0x244b | ebp -72
| 62 | 0x2452 | ebp -68
| 63 | 0x2459 | ebp -64
| 64 | 0x2460 | ebp -60
| 65 | 0x2467 | ebp -56
| 66 | 0x246e | ebp -52
| 67 | 0x2475 | ebp -48
| 68 | 0x247c | ebp -44
| 69 | 0x2483 | ebp -40
| 70 | 0x248a | ebp -36
| 71 | 0x2491 | ebp -32
| 72 | 0x2498 | ebp -28
| 73 | 0x249f | ebp -24
| 74 | 0x24a6 | ebp -20

### Lyre, Lyre Pants on Fire (C1)

Total frames: 5

>LEA Value Offset: 0x252D

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 75 | 0x2526 | ebp -36
| 76 | 0x2531 | ebp -32
| 77 | 0x2539 | ebp -28
| 78 | 0x2540 | ebp -24
| 79 | 0x2547 | ebp -20

### Beyond the Black Stump (C2)

Total frames: 29

First variable ebp -132 uses a int for the address as its too big for a signed byte

>LEA Value Offset: 0x258D

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 80 | 0x2586 | ebp -132
| 81 | 0x2594 | ebp -128
| 82 | 0x259c | ebp -124
| 83 | 0x25a3 | ebp -120
| 84 | 0x25aa | ebp -116
| 85 | 0x25b1 | ebp -112
| 86 | 0x25b8 | ebp -108
| 87 | 0x25bf | ebp -104
| 88 | 0x25c6 | ebp -100
| 89 | 0x25cd | ebp -96
| 90 | 0x25d4 | ebp -92
| 91 | 0x25db | ebp -88
| 92 | 0x25e2 | ebp -84
| 93 | 0x25e9 | ebp -80
| 94 | 0x25f0 | ebp -76
| 95 | 0x25f7 | ebp -72
| 96 | 0x25fe | ebp -68
| 97 | 0x2605 | ebp -64
| 98 | 0x260c | ebp -60
| 99 | 0x2613 | ebp -56
| 100 | 0x261a | ebp -52
| 101 | 0x2621 | ebp -48
| 102 | 0x2628 | ebp -44
| 103 | 0x262f | ebp -40
| 104 | 0x2636 | ebp -36
| 105 | 0x263d | ebp -32
| 106 | 0x2644 | ebp -28
| 107 | 0x264b | ebp -24
| 108 | 0x2652 | ebp -20

### Rex Marks the Spot (C3)

Total frames: 18

>LEA Value Offset: 0x26DD

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 109 | 0x2680 | ebp -88
| 110 | 0x2687 | ebp -84
| 111 | 0x268e | ebp -80
| 112 | 0x2695 | ebp -76
| 113 | 0x269c | ebp -72
| 114 | 0x26a3 | ebp -68
| 115 | 0x26aa | ebp -64
| 116 | 0x26b1 | ebp -60
| 117 | 0x26b8 | ebp -56
| 118 | 0x26bf | ebp -52
| 119 | 0x26c6 | ebp -48
| 120 | 0x26d6 | ebp -44
| 121 | 0x26e1 | ebp -40
| 122 | 0x26ee | ebp -36
| 123 | 0x26f5 | ebp -32
| 124 | 0x26fc | ebp -28
| 125 | 0x2703 | ebp -24
| 126 | 0x270a | ebp -20

### Bonus World [Day] (E2)

Total frames: 123

The bonus worlds work a bit different and end on a different offset and use ints for the memory addresses

>LEA Value Offset: 0x2C84

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 127 | 0x2807 | ebp -624
| 128 | 0x2811 | ebp -620
| 129 | 0x281b | ebp -616
| 130 | 0x2825 | ebp -612
| 131 | 0x282f | ebp -608
| 132 | 0x2839 | ebp -604
| 133 | 0x2843 | ebp -600
| 134 | 0x284d | ebp -596
| 135 | 0x2857 | ebp -592
| 136 | 0x2861 | ebp -588
| 137 | 0x286b | ebp -584
| 138 | 0x2875 | ebp -580
| 139 | 0x287f | ebp -576
| 140 | 0x2889 | ebp -572
| 141 | 0x2893 | ebp -568
| 142 | 0x289d | ebp -564
| 143 | 0x28a7 | ebp -560
| 144 | 0x28b1 | ebp -556
| 145 | 0x28bb | ebp -552
| 146 | 0x28c5 | ebp -548
| 147 | 0x28cf | ebp -544
| 148 | 0x28d9 | ebp -540
| 149 | 0x28e3 | ebp -536
| 150 | 0x28ed | ebp -532
| 151 | 0x28f7 | ebp -528
| 152 | 0x2901 | ebp -524
| 153 | 0x290b | ebp -520
| 154 | 0x2915 | ebp -516
| 155 | 0x291f | ebp -512
| 156 | 0x2929 | ebp -508
| 157 | 0x2933 | ebp -504
| 158 | 0x293d | ebp -500
| 159 | 0x2947 | ebp -496
| 160 | 0x2951 | ebp -492
| 161 | 0x295b | ebp -488
| 162 | 0x2965 | ebp -484
| 163 | 0x296f | ebp -480
| 164 | 0x2979 | ebp -476
| 165 | 0x2983 | ebp -472
| 166 | 0x298d | ebp -468
| 167 | 0x2997 | ebp -464
| 168 | 0x29a1 | ebp -460
| 169 | 0x29ab | ebp -456
| 170 | 0x29b5 | ebp -452
| 171 | 0x29bf | ebp -448
| 172 | 0x29c9 | ebp -444
| 173 | 0x29d3 | ebp -440
| 174 | 0x29dd | ebp -436
| 175 | 0x29e7 | ebp -432
| 176 | 0x29f1 | ebp -428
| 177 | 0x29fb | ebp -424
| 178 | 0x2a05 | ebp -420
| 179 | 0x2a0f | ebp -416
| 180 | 0x2a19 | ebp -412
| 181 | 0x2a23 | ebp -408
| 182 | 0x2a2d | ebp -404
| 183 | 0x2a37 | ebp -400
| 184 | 0x2a41 | ebp -396
| 185 | 0x2a4b | ebp -392
| 186 | 0x2a55 | ebp -388
| 187 | 0x2a5f | ebp -384
| 188 | 0x2a69 | ebp -380
| 189 | 0x2a73 | ebp -376
| 190 | 0x2a7d | ebp -372
| 191 | 0x2a87 | ebp -368
| 192 | 0x2a91 | ebp -364
| 193 | 0x2a9b | ebp -360
| 194 | 0x2aa5 | ebp -356
| 195 | 0x2aaf | ebp -352
| 196 | 0x2ab9 | ebp -348
| 197 | 0x2ac3 | ebp -344
| 198 | 0x2acd | ebp -340
| 199 | 0x2ad7 | ebp -336
| 200 | 0x2ae1 | ebp -332
| 201 | 0x2aeb | ebp -328
| 202 | 0x2af5 | ebp -324
| 203 | 0x2aff | ebp -320
| 204 | 0x2b09 | ebp -316
| 205 | 0x2b13 | ebp -312
| 206 | 0x2b1d | ebp -308
| 207 | 0x2b27 | ebp -304
| 208 | 0x2b31 | ebp -300
| 209 | 0x2b3b | ebp -296
| 210 | 0x2b45 | ebp -292
| 211 | 0x2b4f | ebp -288
| 212 | 0x2b59 | ebp -284
| 213 | 0x2b63 | ebp -280
| 214 | 0x2b6d | ebp -276
| 215 | 0x2b77 | ebp -272
| 216 | 0x2b81 | ebp -268
| 217 | 0x2b8b | ebp -264
| 218 | 0x2b95 | ebp -260
| 219 | 0x2b9f | ebp -256
| 220 | 0x2ba9 | ebp -252
| 221 | 0x2bb3 | ebp -248
| 222 | 0x2bbd | ebp -244
| 223 | 0x2bc7 | ebp -240
| 224 | 0x2bd1 | ebp -236
| 225 | 0x2bdb | ebp -232
| 226 | 0x2be5 | ebp -228
| 227 | 0x2bef | ebp -224
| 228 | 0x2bf9 | ebp -220
| 229 | 0x2c03 | ebp -216
| 230 | 0x2c0d | ebp -212
| 231 | 0x2c17 | ebp -208
| 232 | 0x2c21 | ebp -204
| 233 | 0x2c2b | ebp -200
| 234 | 0x2c35 | ebp -196
| 235 | 0x2c3f | ebp -192
| 236 | 0x2c49 | ebp -188
| 237 | 0x2c53 | ebp -184
| 238 | 0x2c5d | ebp -180
| 239 | 0x2c67 | ebp -176
| 240 | 0x2c7d | ebp -172
| 241 | 0x2c8e | ebp -168
| 242 | 0x2c9e | ebp -164
| 243 | 0x2ca8 | ebp -160
| 244 | 0x2cb2 | ebp -156
| 245 | 0x2cbc | ebp -152
| 246 | 0x2cc6 | ebp -148
| 247 | 0x2cd0 | ebp -144
| 248 | 0x2cda | ebp -140
| 249 | 0x2ce4 | ebp -136

### Bonus World [Night] (E3)

Total frames: 123

>LEA Value Offset: 0x2F76

| ID | Hex Offset | Variable Pointer Address
| :-: | :-: | :-:
| 250 | 0x2d15 | ebp -624
| 251 | 0x2d1f | ebp -620
| 252 | 0x2d29 | ebp -616
| 253 | 0x2d33 | ebp -612
| 254 | 0x2d3d | ebp -608
| 255 | 0x2d47 | ebp -604
| 256 | 0x2d51 | ebp -600
| 257 | 0x2d5b | ebp -596
| 258 | 0x2d65 | ebp -592
| 259 | 0x2d6f | ebp -588
| 260 | 0x2d79 | ebp -584
| 261 | 0x2d83 | ebp -580
| 262 | 0x2d8d | ebp -576
| 263 | 0x2d97 | ebp -572
| 264 | 0x2da1 | ebp -568
| 265 | 0x2dab | ebp -564
| 266 | 0x2db5 | ebp -560
| 267 | 0x2dbf | ebp -556
| 268 | 0x2dc9 | ebp -552
| 269 | 0x2dd3 | ebp -548
| 270 | 0x2ddd | ebp -544
| 271 | 0x2de7 | ebp -540
| 272 | 0x2df1 | ebp -536
| 273 | 0x2dfb | ebp -532
| 274 | 0x2e05 | ebp -528
| 275 | 0x2e0f | ebp -524
| 276 | 0x2e19 | ebp -520
| 277 | 0x2e23 | ebp -516
| 278 | 0x2e2d | ebp -512
| 279 | 0x2e37 | ebp -508
| 280 | 0x2e41 | ebp -504
| 281 | 0x2e4b | ebp -500
| 282 | 0x2e55 | ebp -496
| 283 | 0x2e5f | ebp -492
| 284 | 0x2e69 | ebp -488
| 285 | 0x2e73 | ebp -484
| 286 | 0x2e7d | ebp -480
| 287 | 0x2e87 | ebp -476
| 288 | 0x2e91 | ebp -472
| 289 | 0x2e9b | ebp -468
| 290 | 0x2ea5 | ebp -464
| 291 | 0x2eaf | ebp -460
| 292 | 0x2eb9 | ebp -456
| 293 | 0x2ec3 | ebp -452
| 294 | 0x2ecd | ebp -448
| 295 | 0x2ed7 | ebp -444
| 296 | 0x2ee1 | ebp -440
| 297 | 0x2eeb | ebp -436
| 298 | 0x2ef5 | ebp -432
| 299 | 0x2eff | ebp -428
| 300 | 0x2f09 | ebp -424
| 301 | 0x2f13 | ebp -420
| 302 | 0x2f1d | ebp -416
| 303 | 0x2f27 | ebp -412
| 304 | 0x2f31 | ebp -408
| 305 | 0x2f3b | ebp -404
| 306 | 0x2f45 | ebp -400
| 307 | 0x2f4f | ebp -396
| 308 | 0x2f59 | ebp -392
| 309 | 0x2f6f | ebp -388
| 310 | 0x2f80 | ebp -384
| 311 | 0x2f90 | ebp -380
| 312 | 0x2f9a | ebp -376
| 313 | 0x2fa4 | ebp -372
| 314 | 0x2fae | ebp -368
| 315 | 0x2fb8 | ebp -364
| 316 | 0x2fc2 | ebp -360
| 317 | 0x2fcc | ebp -356
| 318 | 0x2fd6 | ebp -352
| 319 | 0x2fe0 | ebp -348
| 320 | 0x2fea | ebp -344
| 321 | 0x2ff4 | ebp -340
| 322 | 0x2ffe | ebp -336
| 323 | 0x3008 | ebp -332
| 324 | 0x3012 | ebp -328
| 325 | 0x301c | ebp -324
| 326 | 0x3026 | ebp -320
| 327 | 0x3030 | ebp -316
| 328 | 0x303a | ebp -312
| 329 | 0x3044 | ebp -308
| 330 | 0x304e | ebp -304
| 331 | 0x3058 | ebp -300
| 332 | 0x3062 | ebp -296
| 333 | 0x306c | ebp -292
| 334 | 0x3076 | ebp -288
| 335 | 0x3080 | ebp -284
| 336 | 0x308a | ebp -280
| 337 | 0x3094 | ebp -276
| 338 | 0x309e | ebp -272
| 339 | 0x30a8 | ebp -268
| 340 | 0x30b2 | ebp -264
| 341 | 0x30bc | ebp -260
| 342 | 0x30c6 | ebp -256
| 343 | 0x30d0 | ebp -252
| 344 | 0x30da | ebp -248
| 345 | 0x30e4 | ebp -244
| 346 | 0x30ee | ebp -240
| 347 | 0x30f8 | ebp -236
| 348 | 0x3102 | ebp -232
| 349 | 0x310c | ebp -228
| 350 | 0x3116 | ebp -224
| 351 | 0x3120 | ebp -220
| 352 | 0x312a | ebp -216
| 353 | 0x3134 | ebp -212
| 354 | 0x313e | ebp -208
| 355 | 0x3148 | ebp -204
| 356 | 0x3152 | ebp -200
| 357 | 0x315c | ebp -196
| 358 | 0x3166 | ebp -192
| 359 | 0x3170 | ebp -188
| 360 | 0x317a | ebp -184
| 361 | 0x3184 | ebp -180
| 362 | 0x318e | ebp -176
| 363 | 0x3198 | ebp -172
| 364 | 0x31a2 | ebp -168
| 365 | 0x31ac | ebp -164
| 366 | 0x31b6 | ebp -160
| 367 | 0x31c0 | ebp -156
| 368 | 0x31ca | ebp -152
| 369 | 0x31d4 | ebp -148
| 370 | 0x31de | ebp -144
| 371 | 0x31e8 | ebp -140
| 372 | 0x31f2 | ebp -136
