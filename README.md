# Scrabble Solver

Given a board state in Scrabble, and a set of tiles, generate a list of valid solutions, ranked by score.

## Usage Examples

The simplest usage is to create the board state, give a set of tiles, and request a list of solutions.

```python
print('Creating board...')
_board = np.array([
    # 0    1    2    3    4    5    6    7    8    9   10   11   12   13  13
    [' ', ' ', ' ', ' ', ' ', ' ', 'S', 'T', 'Y', 'L', 'e', ' ', ' ', ' ', ' '], # 0
    [' ', ' ', ' ', ' ', ' ', ' ', ' ', 'H', ' ', ' ', ' ', 'K', 'E', 'A', ' '], # 1
    [' ', ' ', ' ', ' ', ' ', ' ', ' ', 'A', ' ', 'V', 'E', 'E', ' ', ' ', ' '], # 2
    [' ', ' ', ' ', ' ', ' ', ' ', ' ', 'W', 'R', 'A', 'N', 'G', 'S', ' ', ' '], # 3
    [' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', 'U', 'G', ' ', 'I', ' ', ' '], # 4
    [' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', 'L', ' ', ' ', ' ', 'G', ' '], # 5
    [' ', 'L', ' ', ' ', ' ', 'U', 'P', 'J', 'E', 'T', ' ', ' ', ' ', 'R', ' '], # 6
    ['M', 'E', 'C', 'C', 'a', ' ', 'O', 'A', 'T', ' ', 'B', 'R', 'O', 'O', 'M'], # 7
    [' ', 'A', ' ', ' ', ' ', ' ', 'Y', ' ', ' ', ' ', 'R', ' ', ' ', 'I', ' '], # 8
    [' ', 'D', 'O', 'H', ' ', ' ', 'N', ' ', ' ', 'Q', 'I', ' ', ' ', 'N', ' '], # 9
    [' ', ' ', 'P', 'O', 'X', ' ', 'T', 'O', 'Z', 'I', 'E', ' ', 'V', ' ', ' '], # 10
    ['F', ' ', 'T', 'W', 'I', 'N', 'E', ' ', ' ', ' ', 'F', 'R', 'E', 'E', 'D'], # 11
    ['A', ' ', ' ', ' ', ' ', ' ', 'D', 'A', ' ', ' ', 'S', 'E', 'A', 'T', ' '], # 12
    ['I', ' ', ' ', ' ', ' ', ' ', ' ', 'I', ' ', ' ', ' ', ' ', 'L', ' ', ' '], # 13
    ['R', 'E', 'A', 'S', 'O', 'N', 'E', 'D', ' ', ' ', ' ', ' ', ' ', ' ', ' ']]) # 14

# Let's get the hand
_hand = list('TEST')

# Calculate the next move
_success, _board, _hand, tmp_score = place_word(_board, _hand, False, 5)
print_board_state(_board)
print('Hand after move:', _hand)
```

The resulting output would be:

```
Creating board...
There are 81 possible words:
21 pts by placing ZEST vertically from [10, 8] 
	Meaning: enthusiasm; relish [n -S] / to give zest to [v -ED, -ING, -S]
	+ ext.  DAS meaning: DA, (Burmese) a heavy Burmese knife, also DAH [n]
	+ ext.  IT meaning: the neuter of he, she, him or her [pron]
19 pts by placing STYLES horizontally from [0, 6] 
	Meaning: STYLE, to name [v]
	+ ext.  SKEG meaning: a length of keel projecting aft to protect the rudder, also SKEGG [n -S]
19 pts by placing SKEG vertically from [0, 11] 
	Meaning: a length of keel projecting aft to protect the rudder, also SKEGG [n -S]
	+ ext.  STYLES meaning: STYLE, to name [v]
18 pts by placing ATS horizontally from [12, 0] 
	Meaning: AT, a monetary unit of Laos [n]
	+ ext.  OPTS meaning: OPT, to decide or choose [v]
18 pts by placing TRES vertically from [6, 11] 
	Meaning: (French) very [adv]
	+ ext.  RE meaning: in tonic sol-fa, the second note of the scale [n -S]
	+ ext.  QIS meaning: QI, (Chinese) a life force, also KI [n]
[[' ' ' ' ' ' ' ' ' ' ' ' 'S' 'T' 'Y' 'L' 'e' ' ' ' ' ' ' ' ']
 [' ' ' ' ' ' ' ' ' ' ' ' ' ' 'H' ' ' ' ' ' ' 'K' 'E' 'A' ' ']
 [' ' ' ' ' ' ' ' ' ' ' ' ' ' 'A' ' ' 'V' 'E' 'E' ' ' ' ' ' ']
 [' ' ' ' ' ' ' ' ' ' ' ' ' ' 'W' 'R' 'A' 'N' 'G' 'S' ' ' ' ']
 [' ' ' ' ' ' ' ' ' ' ' ' ' ' ' ' ' ' 'U' 'G' ' ' 'I' ' ' ' ']
 [' ' ' ' ' ' ' ' ' ' ' ' ' ' ' ' ' ' 'L' ' ' ' ' ' ' 'G' ' ']
 [' ' 'L' ' ' ' ' ' ' 'U' 'P' 'J' 'E' 'T' ' ' ' ' ' ' 'R' ' ']
 ['M' 'E' 'C' 'C' 'a' ' ' 'O' 'A' 'T' ' ' 'B' 'R' 'O' 'O' 'M']
 [' ' 'A' ' ' ' ' ' ' ' ' 'Y' ' ' ' ' ' ' 'R' ' ' ' ' 'I' ' ']
 [' ' 'D' 'O' 'H' ' ' ' ' 'N' ' ' ' ' 'Q' 'I' ' ' ' ' 'N' ' ']
 [' ' ' ' 'P' 'O' 'X' ' ' 'T' 'O' 'Z' 'I' 'E' ' ' 'V' ' ' ' ']
 ['F' ' ' 'T' 'W' 'I' 'N' 'E' ' ' 'E' ' ' 'F' 'R' 'E' 'E' 'D']
 ['A' ' ' ' ' ' ' ' ' ' ' 'D' 'A' 'S' ' ' 'S' 'E' 'A' 'T' ' ']
 ['I' ' ' ' ' ' ' ' ' ' ' ' ' 'I' 'T' ' ' ' ' ' ' 'L' ' ' ' ']
 ['R' 'E' 'A' 'S' 'O' 'N' 'E' 'D' ' ' ' ' ' ' ' ' ' ' ' ' ' ']]
Hand after move: ['T']
```
