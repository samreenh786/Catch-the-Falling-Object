import pygame
import random

# Game shuru karne ke liye setup
pygame.init()

# Window size 500x600 jaisa assignment mein bola hai
window_width = 500
window_height = 600
window = pygame.display.set_mode((window_width, window_height))
pygame.display.set_caption("Catch the Falling Objects - Assignment")

# Colors setup
black = (0, 0, 0)
white = (255, 255, 255)
blue = (0, 0, 255)
red = (255, 0, 0)

# Text ke liye font setup
game_font = pygame.font.Font(None, 35)

# Basket ke variables (y = 560 pe fixed)
bx = 210
by = 560
b_width = 80
b_height = 20
b_speed = 10 # 10px speed per press

# Falling object ke variables
ox = random.randint(0, 480)
oy = 0
o_width = 20
o_height = 20
o_speed = 5 # 5px speed per frame

# Score aur lives counters
score = 0
lives = 3

# Game chalane ke variables
game_running = True
is_game_over = False

# Frames set karne ke liye clock
game_clock = pygame.time.Clock()

# --- MAIN LOOP SHURU ---
while game_running:
    
    # User ke inputs check karne ke liye loop
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_running = False
            
        # Agar game over ho gaya aur 'r' dabaya toh restart hoga
        if event.type == pygame.KEYDOWN:
            if is_game_over == True and event.key == pygame.K_r:
                score = 0
                lives = 3
                bx = 210
                ox = random.randint(0, 480)
                oy = 0
                is_game_over = False

    # Agar game chal raha hai (game over nahi hua hai)
    if is_game_over == False:
        
        # Keys input checking for movement
        keys = pygame.key.get_pressed()
        
        # Left aur Right movement logic (Test case 3: up arrow wagera automatically ignore hoga)
        if keys[pygame.K_LEFT]:
            bx = bx - b_speed
        if keys[pygame.K_RIGHT]:
            bx = bx + b_speed
            
        # Test case 2: Boundary conditions taaki basket window se bahar na jaye
        if bx < 0:
            bx = 0
        if bx > 420: # 500 - 80 (basket width) = 420 max
            bx = 420
            
        # Object ko har frame 5px niche girao
        oy = oy + o_speed
        
        # Collision check karne ke liye Rectangles banana
        basket_rect = pygame.Rect(bx, by, b_width, b_height)
        object_rect = pygame.Rect(ox, oy, o_width, o_height)
        
        # Test case 1: Agar object catch ho gaya
        if basket_rect.colliderect(object_rect):
            score = score + 1
            ox = random.randint(0, 480) # Naya object top pe bhej do random x pe
            oy = 0
            
        # Test case 4: Agar object miss ho gaya aur niche chala gaya
        if oy > 600:
            lives = lives - 1
            if lives <= 0:
                is_game_over = True
            else:
                ox = random.randint(0, 480) # Reset to top
                oy = 0

    # --- DRAWING SECTION ---
    window.fill(white) # Screen saaf karne ke liye white fill

    if is_game_over == False:
        # Game chalte waqt shapes draw karna
        pygame.draw.rect(window, blue, (bx, by, b_width, b_height)) # Blue Basket
        pygame.draw.rect(window, red, (ox, oy, o_width, o_height))   # Red Object
        
        # Score aur Lives board pe dikhane ke liye render aur blit
        txt_score = game_font.render("Score: " + str(score), True, black)
        txt_lives = game_font.render("Lives: " + str(lives), True, black)
        window.blit(txt_score, (15, 15))
        window.blit(txt_lives, (15, 50))
    else:
        # Game Over hone ke baad text screen pe dikhana
        txt_gameover = game_font.render("Game Over", True, red)
        txt_final = game_font.render("Final Score: " + str(score), True, red)
        txt_restart = game_font.render("Press R to Restart", True, red)
        
        window.blit(txt_gameover, (180, 240))
        window.blit(txt_final, (180, 290))
        window.blit(txt_restart, (150, 340))

    # Screen refresh karna
    pygame.display.flip()
    
    # 60 FPS ki speed cap taaki game bohot zyada fast na chale
    game_clock.tick(60)

# Window close karne par quit karna
pygame.quit()