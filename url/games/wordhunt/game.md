# Word Hunt 

### Game-Specific Parameters

| Parameter    | Type    | Description                              |
|-------------|---------|------------------------------------------|
| score1      | String  | Player 1's score for the round           |
| words1      | String  | Total number of words found by player 1  |
| words_list1 | String  | Pipe-delimited list of found words       |

### Word List Format
Words are stored in a pipe-delimited format:
```
WORD1|WORD2|WORD3|WORD4
```

### Parameter Specifics

#### Score Parameter (score1)
- Represents the numerical score for player 1
- Format: String containing numeric value
- Example: "9999999"

#### Words Count Parameter (words1)
- Represents the total count of words found by player 1
- Format: String containing numeric value
- Example: "9999999"

#### Words List Parameter (words_list1)
- Contains all words found by player 1
- Format: Pipe-delimited string of uppercase words
- Example: "GET|REKT|NOOB|IM|PRO|ANDROID|BEST|LOL|BRIIQN"

### Parameter Handling
1. All game-specific parameters are stored in the extraData map
2. Parameters follow a numerical suffix pattern for multiple players
3. Missing parameters should be handled gracefully
4. Word lists should be preserved in their original case (typically uppercase)

### Message Construction
When constructing a Word Hunt message:
1. Base message parameters must be included (sender, ios, ver, etc.)
2. Game-specific parameters (score1, words1, words_list1) are added to extraData
3. All values should be properly encoded according to the protocol's encoding rules

### Validation Rules
1. Scores should be numeric strings
2. Word lists should:
   - Be uppercase
   - Contain only valid dictionary words
   - Be pipe-delimited
   - Not contain duplicate words

### Implementation Notes
1. Word lists should be validated before transmission
2. Score calculations are done by the client (meaning what ever score you send will be seen by who you send it too)
3. No dictionary is provided, you will need to create your own thats compatible with the original game client.
   




### Example Message
```
sender=[GUID]&ios=15.0&ver=1[...]&score1=9999999&words1=9999999&words_list1=GET|REKT|NOOB|IM|PRO|ANDROID|BEST|LOL|BRIIQN

```
![image](https://github.com/user-attachments/assets/c46c0dba-0c89-42b0-8f2b-2979baa59954)

