import pygame

SCREEN_TITLE = 'Crossy RPG'
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 800
WHITE_COLOUR = (255, 255, 255)
BLACK_COLOUR = (0, 0, 0)
PURPLE_COLOUR = (156, 143, 240)
clock = pygame.time.Clock()
pygame.font.init()
font = pygame.font.SysFont('comicsans', 75)

class Game:

    TICK_RATE = 60

    def __init__(self, image_path, title, width, height):
        self.title = title
        self.width = width
        self.height = height

        self.game_display = pygame.display.set_mode((width, height))
        self.game_display.fill(WHITE_COLOUR)
        pygame.display.set_caption(title)

        background_image = pygame.image.load(image_path)
        self.image = pygame.transform.scale(background_image, (width,height))

    def run_game_loop(self, level_speed):
        is_game_over = False
        did_win = False
        direction = 0

        player_character = PlayerCharacter('player.png', 375, 700, 50, 50)
        enemy_0 = NonPlayerCharacter('enemy.png', self.width - 40, 400, 50, 50)
        enemy_0.SPEED *= level_speed
        
        enemy_1 = NonPlayerCharacter('enemy.png', 20, 200, 50, 50)
        enemy_1.SPEED *= level_speed
        
        enemy_2 = NonPlayerCharacter('enemy.png', 20, 600, 50, 50)
        enemy_2.SPEED *= level_speed
        
        treasure = GameObject('treasure.png', 375, 50, 50, 50)
            
        while not is_game_over:

            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    is_game_over = True
                elif event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_UP:
                        direction = 1
                    elif event.key == pygame.K_DOWN:
                        direction = -1
                elif event.type == pygame.KEYUP:
                    if event.key == pygame.K_UP or event.key == pygame.K_DOWN:
                        direction = 0
                print(event)

            self.game_display.fill(WHITE_COLOUR)
            self.game_display.blit(self.image, (0, 0))

            treasure.draw(self.game_display)
            
            player_character.move(direction, self.height)
            player_character.draw(self.game_display)

            enemy_0.move(self.width)
            enemy_0.draw(self.game_display)

            if level_speed > 2:
                enemy_1.move(self.width)
                enemy_1.draw(self.game_display)
            if level_speed > 4:
                enemy_2.move(self.width)
                enemy_2.draw(self.game_display)

            enemies = [enemy_0, enemy_1, enemy_2]
            if player_character.detect_collision(treasure):
                is_game_over = True
                did_win = True
                text = font.render('You Win!', True, BLACK_COLOUR)
                self.game_display.blit(text, (300, 350))
                pygame.display.update()
                clock.tick(1)
                break
            else:
                for enemy in enemies:
                    if player_character.detect_collision(enemy):
                        is_game_over = True
                        did_win = False
                        text = font.render('You Lose :(', True, BLACK_COLOUR)
                        self.game_display.blit(text, (300, 350))
                        pygame.display.update()
                        clock.tick(1)
                        break

            pygame.display.update()
            clock.tick(self.TICK_RATE)

        if did_win:
            self.run_game_loop(level_speed + 0.5)
        else:
            return

class GameObject:
    def __init__(self, image_path, x, y, width, height):
        object_image = pygame.image.load(image_path)
        self.image = pygame.transform.scale(object_image, (width, height))

        self.x_pos = x
        self.y_pos = y

        self.width = width
        self.height = height

    def draw(self, background):
        background.blit(self.image, (self.x_pos, self.y_pos))
        
class PlayerCharacter(GameObject):

    SPEED = 10

    def __init__(self, image_path, x, y, width, height):
        super().__init__(image_path, x, y, width, height)

    def move(self, direction, max_height):
        if direction > 0:
            self.y_pos -= self.SPEED
        elif direction < 0:
            self.y_pos += self.SPEED
        if self.y_pos >= max_height - self.height:
            self.y_pos = max_height - self.height

    def detect_collision(self, other_body):
        if self.y_pos > other_body.y_pos + other_body.height:
            return False
        elif self.y_pos + self.height < other_body.y_pos:
            return False
        
        if self.x_pos > other_body.x_pos + other_body.width:
            return False
        elif self.x_pos + self.width < other_body.x_pos:
            return False

        return True

class NonPlayerCharacter(GameObject):

    SPEED = 10

    def __init__(self, image_path, x, y, width, height):
        super().__init__(image_path, x, y, width, height)

    def move(self, max_width):
        if self.x_pos <= 40:
            self.SPEED = abs(self.SPEED)
        elif self.x_pos >= max_width - 40:
            self.SPEED = -abs(self.SPEED)
        self.x_pos += self.SPEED

pygame.init()

new_game = Game('background.png',SCREEN_TITLE, SCREEN_WIDTH, SCREEN_HEIGHT)
new_game.run_game_loop(1)



pygame.quit()
quit()



# pygame.draw.rect(game_display, BLACK_COLOUR, [350, 350, 100, 100])
            # pygame.draw.circle(game_display, PURPLE_COLOUR, (400, 300), 50)

            # game_display.blit(player_image, (375, 375))


