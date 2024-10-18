import pygame
import random
import math

# Initialize pygame
pygame.init()

# Set the window size and title
screen_width, screen_height = 800, 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Firework")

# Define color
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)


# Define Firework Class
class Firework:
    def __init__(self, x, y, intensity):
        self.x = x
        self.y = y
        self.intensity = intensity
        self.particles = []
        self.create_particles()

    def create_particles(self):
        num_particles = 50 + self.intensity * 10
        for _ in range(num_particles):
            angle = random.uniform(0, 2 * math.pi)
            speed = random.uniform(1, 3) + self.intensity * 0.5
            color = (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
            radius = random.randint(2, 5)
            self.particles.append([self.x, self.y, angle, speed, color, 255, radius])

    def update(self):
        for particle in self.particles:
            particle[0] += math.cos(particle[2]) * particle[3]
            particle[1] += math.sin(particle[2]) * particle[3]
            particle[3] *= 0.95  # Deceleration effect
            particle[5] -= 5  # Gradually reduce transparency
            particle[6] *= 0.95  # Gradually reduce the radius

    def draw(self, surface):
        for particle in self.particles:
            if particle[5] > 0 and particle[6] > 0:  # Only draw particles with transparency and radius greater than 0
                color = (particle[4][0], particle[4][1], particle[4][2], particle[5])
                pygame.draw.circle(surface, color, (int(particle[0]), int(particle[1])), int(particle[6]))


# Main Game Loop
def main():
    clock = pygame.time.Clock()
    fireworks = []
    click_count = 0
    running = True

    while running:
        # Drawing a semi-transparent background
        screen.fill((0, 0, 0, 20))

        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False
            elif event.type == pygame.MOUSEBUTTONDOWN:
                x, y = pygame.mouse.get_pos()
                click_count += 1
                intensity = min(click_count // 10, 20)  # Control the intensity of fireworks
                fireworks.append(Firework(x, y, intensity))

        # Update and draw fireworks
        for firework in fireworks:
            firework.update()
            firework.draw(screen)

        # Removed disappearing fireworks
        fireworks = [fw for fw in fireworks if any(p[5] > 0 and p[6] > 0 for p in fw.particles)]

        # Drawing prompts
        font = pygame.font.SysFont(None, 36)
        text = font.render("Please click to set off firework", True, WHITE)
        screen.blit(text, (20, 20))

        pygame.display.flip()
        clock.tick(60)

    pygame.quit()


if __name__ == "__main__":
    main()
