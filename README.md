def print_board(board):
    """Функция для печати текущего состояния игрового поля."""
    for row in board:
        print(" | ".join(row))
        print("-" * 9)  # Разделительная линия


def check_winner(board):
    """Функция для проверки, есть ли победитель."""
    # Проверка строк
    for row in board:
        if row[0] == row[1] == row[2] != ' ':
            return row[0]

    # Проверка столбцов
    for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] != ' ':
            return board[0][col]

    # Проверка диагоналей
    if board[0][0] == board[1][1] == board[2][2] != ' ':
        return board[0][0]
    if board[0][2] == board[1][1] == board[2][0] != ' ':
        return board[0][2]

    return None  # Нет победителя

def check_draw(board):
    """Функция для проверки ничьи."""
    for row in board:
        if ' ' in row:
            return False
    return True

def is_valid_input(user_input, board):
    """Функция для проверки корректности ввода пользователем."""
    try:
        x, y = map(int, user_input.split())
        if 0 <= x < 3 and 0 <= y < 3 and board[x][y] == ' ':
            return True
        else:
            print("Некорректный ввод. Попробуйте снова.")
            return False
    except ValueError:
        print("Некорректный ввод. Введите координаты в формате 'x y'.")
        return False


def main():
    """Основная функция игры."""
    board = [[' ' for _ in range(3)] for _ in range(3)]
    current_player = 'X'

    while True:
        print_board(board)

        user_input = input(f"Игрок {current_player}, введите координаты (x y): ")

        if is_valid_input(user_input, board):
            x, y = map(int, user_input.split())
            board[x][y] = current_player

            winner = check_winner(board)
            if winner:
                print_board(board)
                print(f"Поздравляем! Игрок {winner} выиграл!")
                break

            if check_draw(board):
                print_board(board)
                print("Игра закончилась вничью!")
                break
            # Смена игрока
            current_player = 'O' if current_player == 'X' else 'X'

if __name__ == "__main__":
    main()
