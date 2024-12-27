# GamePigeon Protocol Documentation

## Overview
This document outlines the protocol specifications for GamePigeon message handling and communication.

## Message Format

### General URL Structure
Messages are transmitted using URL-encoded parameters with specific modifications for GamePigeon's requirements.

### Encryption, Decryption & Encoding
- Encryption and Decryption methods are proprietary and not publicly documented
- URL encoding follows standard conventions with notable exceptions:
  - The pipe character ("|") is preserved unencoded for value separation in specific games (e.g., Word Hunt)
  - Custom encoding rules may apply for game-specific data

### Required Parameters
All GamePigeon messages must include these base parameters:

| Parameter | Type   | Description                    |
|-----------|--------|--------------------------------|
| sender    | String | UUID of the message sender     |
| ios       | String | iOS version of the sender      |
| ver       | Int    | GamePigeon version of sender   |
| tver      | Int    | Game-specific version number   |
| id        | String | Unique message identifier      |
| mode      | Int    | Game mode identifier           |
| num       | Int    | Message sequence number        |
| build     | String | Game build version            |

### Player Data

#### Player Identifiers
- Players are identified using sequential keys starting with "player" (e.g., player1, player2)
- Player order is maintained through numerical suffixes
- The base "player" key without a suffix is reserved

#### Avatar System
Avatars are complex objects containing multiple customization parameters:

| Parameter     | Type           | Description                    |
|--------------|----------------|--------------------------------|
| body         | Int            | Body style identifier          |
| eyes         | Int            | Eyes style identifier          |
| mouth        | Int            | Mouth style identifier         |
| accessories  | Int            | Accessories identifier         |
| wins         | Int            | Player's win count             |
| glasses      | Int            | Glasses style identifier       |
| mustache     | Int            | Mustache style identifier      |
| backdrop     | Int            | Background style identifier    |
| hair         | Int            | Hair style identifier          |
| clothes      | Int            | Clothing style identifier      |

#### Color Parameters
Colors are stored as RGB float triplets (0.0-1.0):

| Parameter      | Format        | Description                    |
|---------------|---------------|--------------------------------|
| backgroundColor| r,g,b         | Avatar background color        |
| bodyColor      | r,g,b         | Avatar body color             |
| hairColor      | r,g,b         | Hair color                    |
| clothesColor   | r,g,b         | Clothing color                |

### Message Parsing

#### Avatar String Format
Avatars are encoded as pipe-delimited key-value pairs:
```
key1,value1|key2,value2|key3,value3
```

Example:
```
body,1|eyes,2|mouth,1|acc,0|wins,10|bg_color,0.5,0.5,0.5|body_color,1.0,0.8,0.6
```



### Implementation Notes

1. All numeric parameters should be validated before parsing
2. Empty avatar strings should return a default avatar object
3. Color values should be clamped to the valid range (0.0-1.0)
4. Missing avatar parameters should fall back to default values (typically 0)
5. Message parsing should be resilient to missing optional parameters


## Game-Specific Extensions
Individual games may extend the base message format with additional parameters and parsing rules. Please read each of their individual documentation for further details.
