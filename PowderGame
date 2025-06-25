import pygame
import sys
import random as rd
import keyboard

WIDTH,HEIGHT = 1000,700
PIXEL_SIZE = 3 
THICKNESS = 3 
FPS = 60

#Elements ID's 1 = Sand, 2 = Stone, 3 = Water, 4 = Oil, 5 = Fire, 6 = Lava
ELEMENT_ID = 1 
ELEMENT_NAME = "Sand"

cols = WIDTH // PIXEL_SIZE
rows = HEIGHT // PIXEL_SIZE

grid = [[0 for _ in range(rows)] for _ in range(cols)] 

pygame.init()
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Powder Game")
clock = pygame.time.Clock()

def reset_grid():
    
    global grid
    grid = [[0 for _ in range(rows)] for _ in range(cols)] 
    

def toggle_element_id(keyPressed):
    global ELEMENT_ID
    global ELEMENT_NAME
    ELEMENT_ID = int(keyPressed)
    print(f"ID: {ELEMENT_ID}")
    match ELEMENT_ID:
        case 1:
            ELEMENT_NAME = "Sand"
        case 2:
            ELEMENT_NAME = "Stone"
        case 3:
            ELEMENT_NAME = "Water"
        case 4:
            ELEMENT_NAME = "Oil"
        case 5:
            ELEMENT_NAME = "Fire"
        case 6:
            ELEMENT_NAME = "Lava"

def handle_erase(pos):
    x,y=pos
    grid_x = x // PIXEL_SIZE
    grid_y = y // PIXEL_SIZE
    half = THICKNESS // 2

    if 0 <= grid_x < cols and 0 <= grid_y < rows:
            for i in range(-half, half + 1):  
                for j in range(-half, half + 1):
                    if 0 <= grid_x+i < cols and 0 <= grid_y+j < rows:
                        grid[grid_x+i][grid_y+j] = 0

def handle_click_concrete(pos):
    x, y = pos
    grid_x = x // PIXEL_SIZE
    grid_y = y // PIXEL_SIZE
    half = THICKNESS // 2

    for dx in range(-half, half + 1):
        for dy in range(-half, half + 1):

            noise_x = rd.randint(0, 1)
            noise_y = rd.randint(0, 1)

            ix = grid_x + dx
            iy = grid_y + dy
            nx = ix + noise_x
            ny = iy + noise_y

            if (
                0 <= ix < cols and
                0 <= iy < rows and
                0 <= nx < cols and
                0 <= ny < rows and
                grid[ix][iy] not in (1, 2)
            ):
                grid[ix][iy] = 2
                grid[nx][ny] = 2
                print(f"Concrete added at grid[{ix}][{iy}] (noised at [{nx}][{ny}])")


def handle_click_sand(pos):
    #TO DO: MAKE NOISE NOT BEING ABLE TO REMOVE OTHER ELEMENTS!!! DONE
    x,y = pos
    grid_x = x // PIXEL_SIZE  
    grid_y = y // PIXEL_SIZE
    half = THICKNESS // 2
    if 0 <= grid_x < cols and 0 <= grid_y < rows:
        for i in range(-half, half + 1):  
            for j in range(-half, half + 1):
                noise_x = rd.randint(-1,1)
                noise_y = rd.randint(0,2)
                ix1 = grid_x + noise_x + i
                iy1 = grid_y + noise_y + j
                ix2 = grid_x - noise_x + i
                iy2 = grid_y - noise_y + j

                if 0 <= ix1 < cols and 0 <= iy1 < rows and 0 <= ix2 < cols and 0 <= iy2 < rows:
                    if grid[ix1][iy1] not in (1,2) and grid[ix2][iy2] not in(1,2): #Here was the fucking shit problem
                        grid[ix1][iy1] = 1
                        grid[ix2][iy2] = 1 
                    print(f"Sand added at grid[{grid_x+noise_x+i}][{grid_y+noise_y+j}]")

def handle_click_water(pos):
    x,y = pos
    grid_x = x // PIXEL_SIZE  
    grid_y = y // PIXEL_SIZE
    half = THICKNESS // 2
    if 0 <= grid_x < cols and 0 <= grid_y < rows:
        for i in range(-half, half + 1):  
            for j in range(-half, half + 1):
                noise_x = rd.randint(-1,1)
                noise_y = rd.randint(0,2)

                ix1 = grid_x + noise_x + i
                iy1 = grid_y + noise_y + j
                ix2 = grid_x - noise_x + i
                iy2 = grid_y - noise_y + j

                if 0 <= ix1 < cols and 0 <= iy1 < rows and 0 <= ix2 < cols and 0 <= iy2 < rows:
                    if grid[ix1][iy1] not in (1,2) and grid[ix2][iy2] not in(1,2):
                        grid[ix1][iy1] = 3
                        grid[ix2][iy2] = 3 
                    print(f"Water added at grid[{grid_x+noise_x+i}][{grid_y+noise_y+j}]")

def handle_click_oil(pos):
    x,y = pos
    grid_x = x // PIXEL_SIZE  
    grid_y = y // PIXEL_SIZE
    half = THICKNESS // 2
    if 0 <= grid_x < cols and 0 <= grid_y < rows:
        for i in range(-half, half + 1):  
            for j in range(-half, half + 1):
                noise_x = rd.randint(-1,1)
                noise_y = rd.randint(0,2)
                ix1 = grid_x + noise_x + i
                iy1 = grid_y + noise_y + j
                ix2 = grid_x - noise_x + i
                iy2 = grid_y - noise_y + j

                if 0 <= ix1 < cols and 0 <= iy1 < rows and 0 <= ix2 < cols and 0 <= iy2 < rows:
                    if grid[ix1][iy1] not in (1,2) and grid[ix2][iy2] not in(1,2):
                        grid[ix1][iy1] = 4
                        grid[ix2][iy2] = 4 
                    print(f"Oil added at grid[{grid_x+noise_x+i}][{grid_y+noise_y+j}]")

def handle_click_fire(pos):
    x,y = pos
    grid_x = x // PIXEL_SIZE  
    grid_y = y // PIXEL_SIZE
    half = THICKNESS//2
    if 0 <= grid_x < cols and 0 <= grid_y < rows:
        for i in range(-half, half + 1):  
            for j in range(-half, half + 1):
                noise_x = rd.randint(-2,2)
                noise_y = rd.randint(-2,0)
                ix1 = grid_x + noise_x + i
                iy1 = grid_y + noise_y + j
                ix2 = grid_x - noise_x + i
                iy2 = grid_y - noise_y + j

                if 0 <= ix1 < cols and 0 <= iy1 < rows and 0 <= ix2 < cols and 0 <= iy2 < rows:
                    if grid[ix1][iy1] not in (1,2,3) and grid[ix2][iy2] not in(1,2,3):
                        grid[ix1][iy1] = (5,5)
                        grid[ix2][iy2] = (5,5)
                    print(f"Fire added at grid[{grid_x+noise_x+i}][{grid_y+noise_y+j}]")
 
def handle_click_lava(pos): #TO DO LAVA
    pass

def draw_grid():
    SAND_COLOR = (195, 180, 130)
    STONE_COLOR = (90, 80, 80)
    WATER_COLOR = (40, 150, 220)
    OIL_COLOR = (100, 60, 40)
    FIRE_COLOR = (230, 70, 80)
    LAVA_COLOR = (215, 25, 20)
    BLACK = (0, 0, 0)
    screen.fill(BLACK)

    for col in range(cols):
        for row in range(rows):
            cell = grid[col][row]

            element = cell[0] if isinstance(cell, tuple) else cell

            if element == 1:
                pygame.draw.rect(screen, SAND_COLOR, (col * PIXEL_SIZE, row * PIXEL_SIZE, PIXEL_SIZE, PIXEL_SIZE))
            elif element == 2:
                pygame.draw.rect(screen, STONE_COLOR, (col * PIXEL_SIZE, row * PIXEL_SIZE, PIXEL_SIZE, PIXEL_SIZE))
            elif element == 3:
                pygame.draw.rect(screen, WATER_COLOR, (col * PIXEL_SIZE, row * PIXEL_SIZE, PIXEL_SIZE, PIXEL_SIZE))
            elif element == 4:
                pygame.draw.rect(screen, OIL_COLOR, (col * PIXEL_SIZE, row * PIXEL_SIZE, PIXEL_SIZE, PIXEL_SIZE))
            elif element == 5:
                pygame.draw.rect(screen, FIRE_COLOR, (col * PIXEL_SIZE, row * PIXEL_SIZE, PIXEL_SIZE, PIXEL_SIZE))
            elif element == 6:
                pygame.draw.rect(screen, LAVA_COLOR, (col * PIXEL_SIZE, row * PIXEL_SIZE, PIXEL_SIZE, PIXEL_SIZE))
            

    text_draw()
    pygame.display.flip()


def text_draw():
    font = pygame.font.SysFont("Courier New", 16)
    screen_width = screen.get_width()
    y_offset = 10
    middle = " " * 43

    esc_mid = f"{middle}Esc to reset"
    info_lines = [f"Chosen Element: {ELEMENT_NAME}", f"Scroll for Brush Size: {THICKNESS}", f"Left Click: Draw", f"Right Click: Erase"]
    element_lines = ["1: Sand ", "2: Stone", "3: Water", "4: Oil  ", "5: Fire ", "6: Lava "]
    
    text_surface = font.render(esc_mid, True, (255, 255, 255))
    screen.blit(text_surface, (10, y_offset))

    for line in element_lines: ##Right part of screen.
        text_surface = font.render(line, True, (255, 255, 255))
        text_width = text_surface.get_width()
        screen.blit(text_surface, (screen_width - text_width - 10, y_offset))
        y_offset += font.get_linesize()
    
    y_offset = 10
    for line in info_lines: ##Left part of screen.
        text_surface = font.render(line, True, (255, 255, 255))
        screen.blit(text_surface, (10, y_offset))
        y_offset += font.get_linesize()


def update_grid():
     for y in reversed(range(rows - 1)):
        for x in range(cols):
                    update_sand(x,y) 
                    update_stone(x,y)
                    update_water(x,y)
                    update_oil(x,y)
                    update_fire(x,y)
                    
def update_water(x, y):
    if grid[x][y] != 3:
        return 

    # Move Down
    if y + 1 < len(grid[0]) and grid[x][y + 1] == 0:
        if grid[x][y + 1] == 0:
            grid[x][y] = 0 
            grid[x][y + 1] = 3
    elif y + 1 < len(grid[0]) and grid[x][y + 1] == 4:
        if grid[x][y + 1] == 4:
            grid[x][y] = 4
            grid[x][y + 1] = 3

    # Move left or right
    elif y + 1 < len(grid[0]) and grid[x][y + 1] == 3:
        noise = rd.randint(-2,2)
        new_x = x + noise
        new_y = y # + 1 for more "movement" in water.

        if (0 <= new_x < len(grid)) and (0 <= new_y < len(grid[0])):
            if grid[new_x][new_y] == 0:
                grid[x][y] = 0
                grid[new_x][new_y] = 3
            elif grid[new_x][new_y] == 4:
                grid[x][y] = 4
                grid[new_x][new_y] = 3
 
def update_sand(x,y):
  if grid[x][y] == 1:
    if grid[x][y + 1] == 0:
        grid[x][y] = 0
        grid[x][y + 1] = 1
    elif grid[x][y+1] == 3 or grid[x][y] == 3:
        grid[x][y]=3
        grid[x][y+1]=1
    elif grid[x][y+1] == 4 or grid[x][y] == 4:
        grid[x][y]=4
        grid[x][y+1]=1
    else:
        noise = rd.randint(-1, 1)
        if noise != 0:
            nx = x + noise
            ny = y + 1
            if 0 <= nx < cols and grid[nx][ny] == 0:
                grid[x][y] = 0
                grid[nx][ny] = 1 

def update_stone(x,y):
  if grid[x][y] == 2:
    grid[x][y] = 2

def update_oil(x,y):
    if grid[x][y] != 4:
       return 
    
    # Move Down
    if y + 1 < len(grid[0]) and grid[x][y + 1] == 0:
        grid[x][y] = 0 
        grid[x][y + 1] = 4

    # Move left or right
    elif y + 1 < len(grid[0]) and grid[x][y + 1] in (3,4):
        noise = rd.randint(-2,2)
        new_x = x + noise
        new_y = y

        if (0 <= new_x < len(grid)) and (0 <= new_y < len(grid[0])):
            if grid[new_x][new_y] == 0:
                grid[x][y] = 0
                grid[new_x][new_y] = 4

def update_fire(x, y):
    if isinstance(grid[x][y], tuple) and grid[x][y][0] == 5:
        fire_life = grid[x][y][1]

        # Burn
        for dx, dy in [(-1, 0), (1, 0), (0, -1)]:
            nx, ny = x + dx, y + dy
            if 0 <= nx < cols and 0 <= ny < rows:
                if grid[nx][ny] == 4:  # 4 is oil
                    grid[nx][ny] = (5, 5)  # ignite oil
                    grid[nx][ny+1] = (5, 5)  
                    
        fire_life -= 1
        if fire_life <= 0:
            grid[x][y] = 0  # fire burns out
        else:
            #fire upward
            ny = y - 1
            if 0 <= ny < rows and grid[x][ny] == 0:
                grid[x][y] = 0
                grid[x][ny] = (5, fire_life)
            else:
                grid[x][y] = (5, fire_life)

while True:
    clock.tick(FPS)
    mouse_pos = pygame.mouse.get_pos()

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        elif event.type == pygame.KEYDOWN:
            if event.unicode.isdigit():
               toggle_element_id(event.unicode)
            elif event.key == pygame.K_LEFT and PIXEL_SIZE < 5:
                PIXEL_SIZE+=1
                cols = WIDTH // PIXEL_SIZE
                rows = HEIGHT // PIXEL_SIZE
                reset_grid()
            elif event.key == pygame.K_RIGHT and PIXEL_SIZE > 3:
                PIXEL_SIZE-=1
                cols = WIDTH // PIXEL_SIZE
                rows = HEIGHT // PIXEL_SIZE
                reset_grid()
            elif event.key == pygame.K_ESCAPE:
                reset_grid()
            elif event.key == pygame.K_k:
                if THICKNESS <15:
                   THICKNESS +=1
            elif event.key == pygame.K_l:
                if THICKNESS > 1:
                   THICKNESS-=1
        elif event.type == pygame.MOUSEWHEEL: #Brush size
            if event.y > 0:
                if THICKNESS <15:
                   THICKNESS +=1
            elif event.y < 0:
                if THICKNESS > 1:
                   THICKNESS -=1

    if pygame.mouse.get_pressed()[0]: # Left Click
        match ELEMENT_ID:
            case 1:
                handle_click_sand(mouse_pos)
            case 2:
                handle_click_concrete(mouse_pos)
            case 3:
                handle_click_water(mouse_pos)
            case 4:
                handle_click_oil(mouse_pos)
            case 5:
                handle_click_fire(mouse_pos)

    elif pygame.mouse.get_pressed()[2]: # Right Click
        handle_erase(mouse_pos)

    update_grid()
    draw_grid()



