import pygame

# Initialize pygame
pygame.init()

# Set the window size
screen_width = 600
screen_height = 400

# Create the screen
screen = pygame.display.set_mode((screen_width, screen_height))

# Load the images
background_image = pygame.image.load("background.png")
bird_image = pygame.image.load("bird.png")
pipe_image = pygame.image.load("pipe.png")

# Create the objects
background = pygame.Rect(0, 0, screen_width, screen_height)
bird = pygame.Rect(100, 100, 50, 50)
pipe1 = pygame.Rect(300, 200, 100, 100)
pipe2 = pygame.Rect(500, 100, 100, 100)

# Set the game state
game_over = False

# Create a clock to control the frame rate
clock = pygame.time.Clock()

# Start the main loop
while not game_over:

    # Get the events
    for event in pygame.event.get():
        # If the user clicks the X button, quit the game
        if event.type == pygame.QUIT:
            game_over = True

        # If the user presses the spacebar, make the bird flap
        if event.type == pygame.KEYDOWN and event.key == pygame.K_SPACE:
            bird.y -= 50

    # Update the game state
    bird.y += 1
    pipe1.x -= 5
    pipe2.x -= 5

    # Check for collisions
    if bird.colliderect(pipe1) or bird.colliderect(pipe2):
        game_over = True

    # Draw the game objects
    screen.blit(background_image, (0, 0))
    screen.blit(bird_image, bird)
    screen.blit(pipe_image, pipe1)
    screen.blit(pipe_image, pipe2)

    # Update the display
    pygame.display.update()

    # Wait for the next frame
    clock.tick(60)

# Quit pygame
pygame.quit()
