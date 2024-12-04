import random

def print_board(board):
    for row in board:
        print(" | ".join(row))
        print("-" * 9)

def check_winner(board):
    # Vérifie les lignes, colonnes et diagonales
    for row in board:
        if row.count(row[0]) == 3 and row[0] != " ":
            return row[0]

    for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] and board[0][col] != " ":
            return board[0][col]

    if board[0][0] == board[1][1] == board[2][2] and board[0][0] != " ":
        return board[0][0]

    if board[0][2] == board[1][1] == board[2][0] and board[0][2] != " ":
        return board[0][2]

    return None

def is_board_full(board):
    return all(cell != " " for row in board for cell in row)

def player_move(board):
    while True:
        try:
            move = int(input("Entrez votre mouvement (1-9): ")) - 1
            if board[move // 3][move % 3] == " ":
                board[move // 3][move % 3] = "X"
                break
            else:
                print("Cette case est déjà prise. Essayez à nouveau.")
        except (ValueError, IndexError):
            print("Entrée invalide. Veuillez entrer un nombre entre 1 et 9.")

def ai_move(board):
    empty_cells = [(i, j) for i in range(3) for j in range(3) if board[i][j] == " "]
    if empty_cells:
        i, j = random.choice(empty_cells)
        board[i][j] = "O"

def main():
    board = [[" " for _ in range(3)] for _ in range(3)]
    print("Jeu du Morpion ! Vous jouez avec 'X' et l'IA joue avec 'O'.")
    
    while True:
        print_board(board)
        
        # Mouvement du joueur
        player_move(board)
        if check_winner(board):
            print_board(board)
            print("Vous avez gagné !")
            break
        if is_board_full(board):
            print_board(board)
            print("Match nul !")
            break
        
        # Mouvement de l'IA
        ai_move(board)
        if check_winner(board):
            print_board(board)
            print("L'IA a gagné !")
            break
        if is_board_full(board):
            print_board(board)
            print("Match nul !")
            break

if __name__ == "__main__":
    main()
