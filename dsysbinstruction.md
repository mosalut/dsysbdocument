# DSYSB Task Instruction Set

| Instruction Name | Instruction Number | Instruction Number Hexadecimal Representation | Operation |
| --- | --- | --- | --- |
| [movsb](#ins_movsb) | 0 | 0x0 | Copy byte array |
| [mov8](#ins_mov) | 1 | 0x1 | Copy 8 bits |
| [mov16](#ins_mov) | 2 | 0x2 | Copy 16 bits |
| [mov32](#ins_mov) | 3 | 0x3 | Copy 32 bits |
| [mov64](#ins_mov) | 4 | 0x4 | Copy 64 bits |
| [add8](#ins_add) | 5 | 0x5 | 8-bit signed addition |
| [add16](#ins_add) | 6 | 0x6 | 16-bit signed addition |
| [add32](#ins_add) | 7 | 0x7 | 32-bit signed addition |
| [add64](#ins_add) | 8 | 0x8 | 64-bit signed addition |
| [add8u](#ins_add) | 9 | 0x9 | 8-bit unsigned addition |
| [add16u](#ins_add) | 10 | 0xa | 16-bit unsigned addition |
| [add32u](#ins_add) | 11 | 0xb | 32-bit unsigned addition |
| [add64u](#ins_add) | 12 | 0xc | 64-bit unsigned addition |
| [sub8](#ins_sub) | 13 | 0xd | 8-bit signed subtraction |
| [sub16](#ins_sub) | 14 | 0xe | 16-bit signed subtraction |
| [sub32](#ins_sub) | 15 | 0xf | 32-bit signed subtraction |
| [sub64](#ins_sub) | 16 | 0x10 | 64-bit signed subtraction |
| [sub8u](#ins_sub) | 17 | 0x11 | 8-bit unsigned subtraction |
| [sub16u](#ins_sub) | 18 | 0x12 | 16-bit unsigned subtraction |
| [sub32u](#ins_sub) | 19 | 0x13 | 32-bit unsigned subtraction |
| [sub64u](#ins_sub) | 20 | 0x14 | 64-bit unsigned subtraction |
| [mul8](#ins_mul) | 21 | 0x15 | 8-bit signed multiplication |
| [mul16](#ins_mul) | 22 | 0x16 | 16-bit signed multiplication |
| [mul32](#ins_mul) | 23 | 0x17 | 32-bit signed multiplication |
| [mul64](#ins_mul) | 24 | 0x18 | 64-bit signed multiplication |
| [mul8u](#ins_mul) | 25 | 0x19 | 8-bit unsigned multiplication |
| [mul16u](#ins_mul) | 26 | 0x1a | 16-bit unsigned multiplication |
| [mul32u](#ins_mul) | 27 | 0x1b | 32-bit unsigned multiplication |
| [mul64u](#ins_mul) | 28 | 0x1c | 64-bit unsigned multiplication |
| [quo8](#ins_quo) | 29 | 0x1d | 8-bit signed division |
| [quo16](#ins_quo) | 30 | 0x1e | 16-bit signed division |
| [quo32](#ins_quo) | 31 | 0x1f | 32-bit signed division |
| [quo64](#ins_quo) | 32 | 0x20 | 64-bit signed division |
| [quo8u](#ins_quo) | 33 | 0x21 | 8-bit unsigned division |
| [quo16u](#ins_quo) | 34 | 0x22 | 16-bit unsigned division |
| [quo32u](#ins_quo) | 35 | 0x23 | 32-bit unsigned division |
| [quo64u](#ins_quo) | 36 | 0x24 | 64-bit unsigned division |
| [inc8](#ins_inc) | 37 | 0x25 | 8-bit signed auto-increment |
| [inc16](#ins_inc) | 38 | 0x26 | 16-bit signed auto-increment |
| [inc32](#ins_inc) | 39 | 0x27 | 32-bit signed auto-increment |
| [inc64](#ins_inc) | 40 | 0x28 | 64-bit signed auto-increment |
| [inc8u](#ins_inc) | 41 | 0x29 | 8-bit unsigned increment |
| [inc16u](#ins_inc) | 42 | 0x2a | 16-bit unsigned increment |
| [inc32u](#ins_inc) | 43 | 0x2b | 32-bit unsigned increment |
| [inc64u](#ins_inc) | 44 | 0x2c | 64-bit unsigned increment |
| [dec8](#ins_dec) | 45 | 0x2d | 8-bit signed decrement |
| [dec16](#ins_dec) | 46 | 0x2e | 16-bit signed decrement |
| [dec32](#ins_dec) | 47 | 0x2f | 32-bit signed decrement |
| [dec64](#ins_dec) | 48 | 0x30 | 64-bit signed decrement |
| [dec8u](#ins_dec) | 49 | 0x31 | 8-bit unsigned decrement |
| [dec16u](#ins_dec) | 50 | 0x32 | 16-bit unsigned decrement |
| [dec32u](#ins_dec) | 51 | 0x33 | 32-bit unsigned decrement |
| [dec64u](#ins_dec) | 52 | 0x34 | 64-bit unsigned decrement |
| [write_uint8](#ins_write_uint) | 53 | 0x35 | Write uint8 from register to vData |
| [write_uint16](#ins_write_uint) | 54 | 0x36 | Write uint16 from register to vData |
| [write_uint32](#ins_write_uint) | 55 | 0x37 | Write uint32 from register to vData |
| [write_uint64](#ins_write_uint) | 56 | 0x38 | Write uint64 from register to vData |
| [read_uint8](#ins_read_uint) | 57 | 0x39 | Read uint8 from vData to register |
| [read_uint16](#ins_read_uint) | 58 | 0x3a | Read uint16 from vData to register |
| [read_uint32](#ins_read_uint) | 59 | 0x3b | Read uint32 from vData to register |
| [read_uint64](#ins_read_uint) | 60 | 0x3c | Read uint64 from vData into register |
| [eq](#ins_eq) | 61 | 0x3d | Compare for equality |
| [gt](#ins_gt) | 62 | 0x3e | Compare for greater than |
| [lt](#ins_lt) | 63 | 0x3f | Compare for less than |
| [gteq](#ins_gteq) | 64 | 0x40 | Compare for greater than or equal to |
| [lteq](#ins_lteq) | 65 | 0x41 | Compare for less than or equal to |
| [eq_bytes](#ins_eq_bytes) | 66 | 0x42 | Compare byte order |
| [height](#ins_height) | 67 | 0x43 | Get current block height |
| [transfer_dsb_from_caller](#ins_transfer_dsb_from_caller) | 68 | 0x44 | Task caller transfers DSB to task initiator |
| [transfer_dsb_to_caller](#ins_transfer_dsb_to_caller) | 69 | 0x45 | Task initiator transfers DSB to task caller |
| [transfer_from_caller](#ins_transfer_from_caller) | 70 | 0x46 | Task caller transfers asset token to task initiator |
| [transfer_to_caller](#ins_transfer_to_caller) | 71 | 0x47 | Task initiator transfers asset token to task caller |
| [pushsb](#ins_pushsb) | 72 | 0x48 | Read byte order from call parameter into vData |
| [push8](#ins_push) | 73 | 0x49 | Read 8-bit byte from call parameter into vData |
| [push16](#ins_push) | 74 | 0x4a | Read 16-bit byte from call parameter into vData |
| [push32](#ins_push) | 75 | 0x4b | Read 32-bit byte from call parameter into vData |
| [push64](#ins_push) | 76 | 0x4c | Read 64-bit byte from call parameter into vData |
| [exit](#ins_exit) | 77 | 0x4d | exit |
- In the following pn descriptions, unless otherwise specified, they represent the starting position index of specific data. Some length data is a value.

<h3 id="ins_movsb">movsb</h3>

```
p0: Source
p1: Destination
p2: Length
```

p0, p1 are the indices of the vData where the data is located

<h3 id="ins_mov">mov8&nbsp;mov16&nbsp;mov32&nbsp;mov64</h3>

```
p0: Source
p1: Destination
```

p0, p1 are the indices of the vData where the data is located

<h3 id="ins_add">add8&nbsp;add16&nbsp;add32&nbsp;add64&nbsp;add8u&nbsp;add16u&nbsp;add32u&nbsp;add64u</h3>

```
p0: Addend
p1: Addend
p2: Sum
```

p0, p1, and p2 are the indices of the vData containing the data.

<h3 id="ins_sub">sub8&nbsp;sub16&nbsp;sub32&nbsp;sub64&nbsp;sub8u&nbsp;sub16u&nbsp;sub32u&nbsp;sub64u</h3>

```
p0: Minuend
p1: Subtrahend
p2: Subtraction
```

p0, p1, and p2 are the indices of the vData containing the data.

<h3 id="ins_mul">mul8&nbsp;mul16&nbsp;mul32&nbsp;mul64&nbsp;mul8u&nbsp;mul16u&nbsp;mul32u&nbsp;mul64u</h3>

```
p0: Multiplier
p1: Multiplier
p2: Product
```

p0, p1, and p2 are the indices of the vData containing the data.

<h3 id="ins_quo">quo8&nbsp;quo16&nbsp;quo32&nbsp;quo64&nbsp;quo8u&nbsp;quo16u&nbsp;quo32u&nbsp;quo64u</h3>

```
p0: dividend
p1: divisor
p2: quotient
p3: remainder
```

p0, p1, p2, p3 are the indices of the vData where the data is located.

<h3 id="ins_inc8">inc8&nbsp;inc16&nbsp;inc32&nbsp;inc64&nbsp;inc8u&nbsp;inc16u&nbsp;inc32u&nbsp;inc64u</h3>

```
p0: self-incrementing number
```

p0 is the index of vData where the data is located


<h3 id="ins_dec8">dec8&nbsp;dec16&nbsp;dec32&nbsp;dec64&nbsp;dec8u&nbsp;dec16u&nbsp;dec32u&nbsp;dec64u</h3>

```
p0: Decrement
```

p0 is the index of the data in vData

<h3 id="ins_write_uint">write_uint8&nbsp;write_uint16&nbsp;write_uint32&nbsp;write_uint64</h3>

```
p0: Destination
```

Write from virtual register to p0

<h3 id="ins_read_uint">read_uint8&nbsp;read_uint16&nbsp;read_uint32&nbsp;read_uint64</h3>

```
p0: Source
```

Read from p0 to virtual register

<h3 id="ins_eq">eq</h3>

```
p0: Number to compare with
p1: Number to compare with
p2: Destination of the jump
p3: A flag value used to determine the bit length of a number (0: 8, 1: 16, 2: 32, 3: 64)
```

If p0 == p1, the instruction jumps to p2. To avoid loops, instructions can only jump into the future, not into the past.

<h3 id="ins_gt">gt</h3>

```
p0: The number to be compared
p1: The number to be compared
p2: Destination of the jump
p3: A flag value used to determine the bit length of a number (0: 8, 1: 16, 2: 32, 3: 64)
```

If p0 > p1, the instruction jumps to p2. To avoid loops, instructions can only jump into the future, not into the past.

<h3 id="ins_lt">lt</h3>

```
p0: The number to be compared
p1: The number to be compared
p2: Destination of the jump
p3: A flag value used to determine the bit length of a number (0: 8, 1: 16, 2: 32, 3: 64)
```

If p0 < p1, the instruction jumps to p2. To avoid loops, instructions can only jump into the future, not into the past.

<h3 id="ins_gteq">gteq</h3>

```
p0: The number to be compared
p1: The number to be compared
p2: Destination of the jump
p3: A flag value used to determine the bit length of a number (0: 8, 1: 16, 2: 32, 3: 64)
```

If p0 >= p1, the instruction jumps to p2. To avoid loops, instructions can only jump into the future, not into the past.

<h3 id="ins_lteq">lteq</h3>

```
p0: The number to be compared
p1: Number to compare
p2: Destination to jump to
p3: A flag value used to determine the bit length of the number (0: 8, 1: 16, 2: 32, 3: 64)
```

If p0 <= p1, the instruction jumps to p2. To avoid loops, instructions can only jump into the future, not into the past.

<h3 id="ins_eq_bytes">eq_bytes</h3>

```
p0: Byte order to compare
p1: Byte order to compare
p2: Destination to jump to
p3: Byte order length
```

If p0 == p1, the instruction jumps to p2. To avoid loops, instructions can only jump into the future, not into the past.

<h3 id="ins_height">height</h3>
Get the current block height and temporarily save the result to the vUint32 virtual register.

<h3 id="ins_transfer_dsb_from_caller">transfer_dsb_from_caller</h3>

```
p0: Transfer amount
```

Transfer p0 satoshi DSB from the task caller address to the task initiator address

<h3 id="ins_transfer_dsb_to_caller">transfer_dsb_to_caller</h3>

```
p0: Transfer amount
```

Transfer p0 satoshi DSB from the task initiator address to the task caller address

<h3 id="ins_transfer_from_caller">transfer_from_caller</h3>

```
p0: Specified asset ID
p1: Transfer amount
```

Transfer p0 satoshi of the specified asset from the task caller address to the task initiator address

<h3 id="ins_transfer_to_caller">transfer_to_caller</h3>

```
p0: Specified asset ID
p1: Transfer amount
```

Transfer p0 satoshis of the specified asset from the task initiator's address to the task caller's address

<h3 id="ins_pushsb">pushsb</h3>

```
p0: Task call parameters
p1: Receive parameter vData
p2: Length
```

Passing byte order parameters when calling a task

<h3 id="ins_push">push8&nbsp;push16&nbsp;push32&nbsp;push64</h3>

```
p0: Task call parameters
p1: vData receiving parameters
```

When calling a task, pass a numeric parameter

<h3 id="ins_exit">exit</h3>

Exit
