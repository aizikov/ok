import pygame
import sys


class Obj(pygame.sprite.Sprite):
    def __init__(self, obj_type, x_pos, y_pos):
        super().__init__(grp, sprt)
        self.image = imgs[obj_type]
        self.rect = self.image.get_rect().move(wdth * x_pos, hght * y_pos)


class Player(pygame.sprite.Sprite):
    def __init__(self, x_pos, y_pos):
        super().__init__(grp_plr, sprt)
        self.image = img_plr
        self.rect = self.image.get_rect().move(wdth * x_pos + 15, hght * y_pos + 5)

    def update(self, *args):
        if args and type(args[0]) == tuple:
            if args[0][pygame.K_w]:
                self.rect = self.rect.move(0, -10)
                print('up')
            if args[0][pygame.K_s]:
                self.rect = self.rect.move(0, 10)
            if args[0][pygame.K_a]:
                self.rect = self.rect.move(-10, 0)
            if args[0][pygame.K_d]:
                self.rect = self.rect.move(10, 0)


def ld_lvl(file):
    file = "data/" + file
    with open(file, 'r') as mp:
        mp_lines = [line.strip() for line in mp]

    max_wdth = max(map(len, mp_lines))
    return list(map(lambda x: x.ljust(max_wdth, '.'), mp_lines))


def gn_lvl(level):
    new_player, x, y = None, None, None
    for y_pos in range(len(level)):
        for x_pos in range(len(level[y_pos])):
            if level[y_pos][x_pos] == '.':
                Obj('empty', x_pos, y_pos)
            elif level[y_pos][x_pos] == '#':
                Obj('wall', x_pos, y_pos)
            elif level[y_pos][x_pos] == '@':
                Obj('empty', x_pos, y_pos)
                new_player = Player(x_pos, y_pos)
    return new_player, x, y


def ld_img(file):
    file = 'data/' + file
    return pygame.image.load(file).convert_alpha()


def terminate():
    pygame.quit()
    sys.exit()


def err_scr():
    txt_lines = ['Произошла ошибка', 'Нажмите любую клавишу', 'для выхода из игры']

    screen.fill((0, 0, 0))
    font = pygame.font.Font(None, 30)
    txt_coord = 50
    for line in txt_lines:
        string_rendered = font.render(line, 1, pygame.Color('white'))
        intro_rect = string_rendered.get_rect()
        txt_coord += 10
        intro_rect.top = txt_coord
        intro_rect.x = 10
        txt_coord += intro_rect.height
        screen.blit(string_rendered, intro_rect)

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                terminate()
            elif event.type == pygame.KEYDOWN or event.type == pygame.MOUSEBUTTONDOWN:
                terminate()
        pygame.display.flip()
        clock.tick(FPS)


def start_scr():
    intro_text = ["ЗАСТАВКА", "",
                  "Правила игры",
                  "Если в правилах несколько строк,",
                  "приходится выводить их построчно"]

    background = pygame.transform.scale(ld_img('background.jpg'), (screen_width, screen_height))
    screen.blit(background, (0, 0))
    font = pygame.font.Font(None, 30)
    txt_coord = 50
    for line in intro_text:
        string_rendered = font.render(line, 1, pygame.Color('black'))
        intro_rect = string_rendered.get_rect()
        txt_coord += 10
        intro_rect.top = txt_coord
        intro_rect.x = 10
        txt_coord += intro_rect.height
        screen.blit(string_rendered, intro_rect)

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                terminate()
            elif event.type == pygame.KEYDOWN or event.type == pygame.MOUSEBUTTONDOWN:
                return
        pygame.display.flip()
        clock.tick(FPS)


file = input('Введите название файла: ')
pygame.init()
screen_width, screen_height = 800, 800
screen = pygame.display.set_mode((screen_width, screen_height))
FPS = 30
clock = pygame.time.Clock()

start_scr()
try:
    level = ld_lvl(file)
except (FileNotFoundError, IOError):
    err_scr()

imgs = {'wall': ld_img('wall.png'), 'empty': ld_img('empty.png')}
img_plr = ld_img('player.png')

wdth = hght = 50

player = None

sprt = pygame.sprite.Group()
grp = pygame.sprite.Group()
grp_plr = pygame.sprite.Group()
player, level_width, level_height = gn_lvl(level)

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            terminate()
        if event.type == pygame.KEYDOWN:
            print(event.key)
    sprt.update(pygame.key.get_pressed())

    screen.fill((0, 0, 0))
    grp.draw(screen)
    grp_plr.draw(screen)
    clock.tick(FPS)
    pygame.display.flip()
