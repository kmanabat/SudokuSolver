# Kyle Manabat
# Find Empty (e1)
# Test possible number (taking into account row, column and square)
# Once a number is found, recursively check next box
# If next box fails, work backwards in the recursion loop until another possibility is found

# required methods:
# getEmpty
# solve (recursive)
#   - isLegal
# printBoard
# error trapping?

board = [
    [0, 6, 0, 3, 0, 0, 8, 0, 4],
    [5, 3, 7, 0, 9, 0, 0, 0, 0],
    [0, 4, 0, 0, 0, 6, 3, 0, 7],
    [0, 9, 0, 0, 5, 1, 2, 3, 8],
    [0, 0, 0, 0, 0, 0, 0, 0, 0],
    [7, 1, 3, 6, 2, 0, 0, 4, 0],
    [3, 0, 6, 4, 0, 0, 0, 1, 0],
    [0, 0, 0, 0, 6, 0, 5, 2, 3],
    [1, 0, 2, 0, 0, 9, 0, 8, 0]
]



def printBoard(b):
    for i in range(len(b)):
        if i % 3 == 0:
            print("- - - - - - - - - - - - - ")

        for j in range(len(b[0])):
            if j % 3 == 0:
                print("| ", end="")

            if j == 8:
                print(str(b[i][j]) + " |")
            else:
                print(str(b[i][j]) + " ", end="")
    print("- - - - - - - - - - - - - ")


def getEmpty(b):
    for i in range(len(b)):
        for j in range (len(b)):
            if b[i][j] == 0:
                return i, j
    return False


def isLegal(b, num, row, col):
    # check row
    for i in range(len(b)):
        if b[row][i] == num and col != i:
            return False
    # check col
    for i in range(len(b)):
        if b[i][col] == num and row != i:
            return False
    # check square
    rowSQ = int(row/3)
    colSQ = int(col/3)
    # reset to beginning of square
    rowO = rowSQ * 3
    colO = colSQ * 3
    for i in range(rowO, rowO+3):
        for j in range(colO, colO+3):
            if b[i][j] == num and i != row and j != col:
                return False
    return True


def solve(b):
    empty_pos = getEmpty(b)
    if not empty_pos:
        return True
    else:
        r, c = empty_pos

    for i in range(1, 10):
        if isLegal(b, i, r, c):
            b[r][c] = i
            if solve(b):
                return True
            b[r][c] = 0
    return False


printBoard(board)
solve(board)
print("SOLVED BOARD: ")
printBoard(board)


