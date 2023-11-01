import pygame
import random

# Initialize Pygame
pygame.init()

# Constants
WIDTH, HEIGHT = 800, 600
BALL_SIZE = 20
BALL_SPEED = 5
WHITE = (255, 255, 255)
BLUE = (0, 0, 255)

# Create the screen
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Catch the Ball")

# Initialize player position
player_x = WIDTH // 2
player_y = HEIGHT - 50

# Initialize ball position and speed
ball_x = random.randint(0, WIDTH - BALL_SIZE)
ball_y = 0
ball_speed_y = BALL_SPEED

# Game loop
running = True
score = 0

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT]:
        player_x -= 5
    if keys[pygame.K_RIGHT]:
        player_x += 5

    # Update ball position
    ball_y += ball_speed_y

    # Check if the ball is caught
    if ball_y > HEIGHT - BALL_SIZE:
        if player_x < ball_x < player_x + BALL_SIZE:
            score += 1
            ball_x = random.randint(0, WIDTH - BALL_SIZE)
            ball_y = 0

    # Draw everything
    screen.fill(WHITE)
    pygame.draw.rect(screen, BLUE, (player_x, player_y, BALL_SIZE, BALL_SIZE))
    pygame.draw.ellipse(screen, BLUE, (ball_x, ball_y, BALL_SIZE, BALL_SIZE))

    # Update the display
    pygame.display.update()

# Clean up
pygame.quit()

