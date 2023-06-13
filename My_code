import pygame
import numpy as np

# Размер окна и клетки
cell_size = 10
width, height = 800, 600
cols, rows = width // cell_size, height // cell_size

# Инициализация Pygame
pygame.init()
clock = pygame.time.Clock()
screen = pygame.display.set_mode((width, height))

# Инициализация игрового поля
grid = np.zeros((cols, rows))

# Функция для заполнения случайными значениями
def randomize_grid():
    grid[:, :] = np.random.choice([0, 1], size=(cols, rows), p=[0.8, 0.2])

# Функция для рисования клеток
def draw_cells():
    screen.fill((255, 255, 255))
    for x in range(cols):
        for y in range(rows):
            if grid[x][y] == 1:
                center_x = x * cell_size + cell_size // 2
                center_y = y * cell_size + cell_size // 2
                radius = cell_size // 2
                pygame.draw.circle(screen, (0, 0, 0), (center_x, center_y), radius)

# Функция для обновления состояния клеток
def update_cells():
    new_grid = np.copy(grid)
    for x in range(cols):
        for y in range(rows):
            neighbors = count_neighbors(x, y)
            if grid[x][y] == 1:
                if neighbors < 2 or neighbors > 3:
                    new_grid[x][y] = 0
            else:
                if neighbors == 3:
                    new_grid[x][y] = 1
    grid[:, :] = new_grid[:, :]

# Функция для подсчета соседей клетки
def count_neighbors(x, y):
    count = 0
    for i in range(-1, 2):
        for j in range(-1, 2):
            neighbor_x = (x + i + cols) % cols
            neighbor_y = (y + j + rows) % rows
            count += grid[neighbor_x][neighbor_y]
    count -= grid[x][y]
    return count

# Случайное заполнение игрового поля
randomize_grid()

# Основной игровой цикл
running = True
while running:
    # Обработка событий
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                randomize_grid()

    # Обновление состояния клеток
    update_cells()

    # Рисование клеток
    draw_cells()

    # Обновление экрана
    pygame.display.flip()
    clock.tick(10)  # Частота обновления (10 кадров в секунду)

# Завершение работы Pygame
pygame.quit()
