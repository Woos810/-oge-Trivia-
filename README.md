import pygame
import random

# Initialize Pygame
pygame.init()

# Screen settings
WIDTH = 800
HEIGHT = 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Bounce Craze")

# Colors
WHITE = (255, 255, 255)
RED = (255, 0, 0)
BLUE = (0, 0, 255)

# Paddle settings
PADDLE_WIDTH = 100
PADDLE_HEIGHT = 10
paddle_x = WIDTH // 2 - PADDLE_WIDTH // 2
paddle_y = HEIGHT - 40
paddle_speed = 10

# Ball settings
BALL_RADIUS = 10
ball_x = WIDTH // 2
ball_y = HEIGHT // 2
ball_dx = 5  # Horizontal speed
ball_dy = -5  # Vertical speed (negative to move upward initially)

# Game loop
running = True
clock = pygame.time.Clock()

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Move paddle with keys
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and paddle_x > 0:
        paddle_x -= paddle_speed
    if keys[pygame.K_RIGHT] and paddle_x < WIDTH - PADDLE_WIDTH:
        paddle_x += paddle_speed

    # Move ball
    ball_x += ball_dx
    ball_y += ball_dy

    # Ball collision with walls
    if ball_x - BALL_RADIUS < 0 or ball_x + BALL_RADIUS > WIDTH:
        ball_dx = -ball_dx
    if ball_y - BALL_RADIUS < 0:
        ball_dy = -ball_dy

    # Ball collision with paddle
    if (ball_y + BALL_RADIUS > paddle_y and 
        paddle_x < ball_x < paddle_x + PADDLE_WIDTH and 
        ball_dy > 0):
        ball_dy = -ball_dy

    # Game over if ball falls below paddle
    if ball_y > HEIGHT:
        print("Game Over!")
        running = False

    # Draw everything
    screen.fill((0, 0, 0))  # Black background
    pygame.draw.rect(screen, BLUE, (paddle_x, paddle_y, PADDLE_WIDTH, PADDLE_HEIGHT))
    pygame.draw.circle(screen, RED, (int(ball_x), int(ball_y)), BALL_RADIUS)

    # Update display
    pygame.display.flip()
    clock.tick(60)  # 60 FPS

# Quit Pygame
pygame.quit()
