# My-mini-project-
A python code game
def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 9)

def check_winner(board, player):
    # Check rows
    for row in board:
        if all(s == player for s in row):
            return True
    # Check columns
    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True
    # Check diagonals
    if all(board[i][i] == player for i in range(3)) or \
       all(board[i][2 - i] == player for i in range(3)):
        return True
    return False

# Initialize the board
board = [[" " for _ in range(3)] for _ in range(3)]
player = "X"

# Game loop
for _ in range(9):
    print_board(board)
    try:
        row, col = map(int, input(f"Player {player}, enter row and column (0-2): ").split())
        if 0 <= row <= 2 and 0 <= col <= 2:
            if board[row][col] == " ":
                board[row][col] = player
                if check_winner(board, player):
                    print_board(board)
                    print(f"Player {player} wins!")
                    break
                player = "O" if player == "X" else "X"
            else:
                print("Invalid move! Cell already taken.")
        else:
            print("Invalid input! Enter row and column between 0 and 2.")
    except ValueError:
        print("Invalid input! Please enter two numbers separated by space.")
else:
    print_board(board)
    print("It's a tie!")
