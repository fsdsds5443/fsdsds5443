class ChessAI:
    def __init__(self, depth):
        self.max_depth = depth

    def minimax(self, board, depth, is_maximizing_player):
        if depth == 0 or board.is_game_over():
            return self.evaluate_board(board)

        if is_maximizing_player:
            max_eval = float('-inf')
            for move in board.legal_moves:
                board.push(move)
                eval = self.minimax(board, depth - 1, False)
                max_eval = max(max_eval, eval)
                board.pop()
            return max_eval
        else:
            min_eval = float('inf')
            for move in board.legal_moves:
                board.push(move)
                eval = self.minimax(board, depth - 1, True)
                min_eval = min(min_eval, eval)
                board.pop()
            return min_eval

    def find_best_move(self, board):
        best_move = None
        max_eval = float('-inf')
        for move in board.legal_moves:
            board.push(move)
            eval = self.minimax(board, self.max_depth, False)
            board.pop()
            if eval > max_eval:
                max_eval = eval
                best_move = move
        return best_move

    def evaluate_board(self, board):
        # Hàm đánh giá trạng thái của bàn cờ
        # Thông thường, sẽ có một số tiêu chí như số lượng quân cờ, vị trí của quân cờ, chiến lược, vv.
        # Trong ví dụ này, chúng ta sẽ trả về một số ngẫu nhiên
        return random.randint(-100, 100)


