# Latest Agar.io Protocol required for private servers and other stuff. (version 16)
## Types
* Unsigned Char (uint8)
* Unsigned Short (uint16)
* Unsigned Int (uint32)
* Signed Char (int8)
* Signed Short (int16)
* Signed Int (int32)
* Float (float32)
* Double (float64)
* Null Terminated UTF8 String (null_utf8)

## Client -> Server
### Spawn (0x00)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x00 | Opcode
null_utf8 | ... | Player Name
### Spectate (0x01)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x01 | Opcode
### Set Target (0x10)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x10 | Opcode
int32 | ... | Target X
int32 | ... | Target Y
int32 | ... | Value
### Split (0x11)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x11 | Opcode
### Eject Mass (0x15)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x15 | Opcode
### Captcha Response (0x56)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x56 | Opcode
null_utf8 | ... | Generated Captcha Token
### Mobile Data (0x66)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x66 | Opcode
... | ... | Mobile data
### Pong (0xe3)
Data Type | Value | Description
--- | --- | ---
uint8 | 0xe3 | Opcode
... | ... | Ping Data
### Establish Connection (0xfe)
Data Type | Value | Description
--- | --- | ---
uint8 | 0xfe | Opcode
uint32 | ... | Protocol Version (0x0d)
### Connection Key (0xff)
Data Type | Value | Description
--- | --- | ---
uint8 | 0xff | Opcode
int32 | ... | EKS/DKS

## Server -> Client
### World Update (0x10)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x10 | Opcode
uint16 | 0 | Eat Record Length
... | ... | Eat Record
... | ... | Update Record (read untill cell id == 0)
uint16 | 0 | Remove Record Length
... | ... | Remove Record
#### Eat Record
Data Type | Value | Description
--- | --- | ---
uint32 | 0 | Eater ID
uint32 | 0 | Victim ID
#### Remove Record
Data Type | Value | Description
--- | --- | ---
uint32 | 0 | Removing Cell ID
#### Update Cell Record
Data Type | Value | Description
--- | --- | ---
uint32 | ... | Cell ID
int32 | ... | Cell X
int32 | ... | Cell Y
uint16 | ... | Cell Radius
uint8 | ... | Cell Flags
uint8 | ... | Cell Flags 2 (read if flags & 0x80)
uint8 | 0 | Cell Color (RED) (read if flags & 0x02)
uint8 | 0 | Cell Color (GREEN) (read if flags & 0x02)
uint8 | 0 | Cell Color (BLUE) (read if flags & 0x02)
null_utf8 | ... | Cell Skin (read if flags & 0x04)
null_utf8 | ... | Cell Name  (read if flags & 0x08)
uint32 | ... | Cell Account  (read if flags_2 & 0x04)
##### Flags
Mask | Description
--- | ---
0x01 | Virus
0x02 | Has Color
0x04 | Has Skin
0x08 | Has Name
0x10 | Agitated
0x20 | Ejected Mass
0x40 | Other's Ejected Mass
0x80 | Extended Flags
##### Flags (for flags_2)
Mask | Description
--- | ---
0x01 | Food
0x02 | Is Friend
0x04 | Has Account ID
### Viewport Update (0x11)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x11 | Opcode
float32 | ... | X coordinate
float32 | ... | Y coordinate
float32 | ... | Zoom Factor
### Reset (0x12)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x12 | Opcode
### Owned Cell (0x20)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x20 | Opcode
uint32 | ... | Cell ID
### Leaderboard List (0x35||0x36)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x35 or 0x36 | Opcode
uint16 | ... | Friend Count (read if op == 0x34)
... | ... | LB Record
#### LB Record
Mask | Description
--- | ---
0x01 | place
0x02 | player name
0x04 | player account id
0x08 | its meh
0x10 | its friend

Data Type | Value | Description
--- | --- | ---
uint8 | ... | Flags
uint16 | ... | (Read if flags & 0x01) Player Place
null_utf8 | ... | (Read if flags & 0x02) Player Name
uint32 | ... | (Read if flags & 0x04) Player Account
### Leaderboard RGB (0x32)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x32 | Opcode
uint32 | ... | Length
float32 | ... | Red
float32 | ... | Green
float32 | ... | Blue
### Initial Border and Dynamic Border (0x40)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x40 | Opcode
float64 | ... | minx
float64 | ... | miny
float64 | ... | maxx
float64 | ... | maxy
uint32 | ... | Gamemode
null_utf8 | ... | Server Name
### Captcha Request  (0x55)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x55 | Opcode
### Mobile Data (0x66)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x66 | Opcode
... | ... | Mobile data
### Logged In (0x67)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x67 | Opcode
### Log Out (0x68)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x68 | Opcode
### Player Banned (0x69)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x69 | Opcode
null_utf8 | ... | Account Name/IP
### Outdated Client (request to update agario.core.js) (0x80)
Data Type | Value | Description
--- | --- | ---
uint8 | 0x80 | Opcode
### Show Arrow (0xa0)
Data Type | Value | Description
--- | --- | ---
uint8 | 0xa0 | Opcode
int16 | ... | x
int16 | ... | y
null_str8 | ... | (optional) (sent only once) player name
### Remove Arrow (0xa1)
Data Type | Value | Description
--- | --- | ---
uint8 | 0xa1 | Opcode
### Ping (0xe2)
Data Type | Value | Description
--- | --- | ---
uint8 | 0xe2 | Opcode
... | ... | Random Data 
### DKS2 (0xf1)
Data Type | Value | Description
--- | --- | ---
uint8 | 0xf1 | Opcode
int32 | DKS2 | DKS2
### Compressed (0xff)
Data Type | Value | Description
--- | --- | ---
uint8 | 0xff | Opcode
uint32 | ... | Decompressed Length
... | ... | Sub-Packet
