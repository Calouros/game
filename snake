import pygame
from pygame.locals import *
from sys import exit
from random import randint
from pygame.math import Vector2

pygame.init()

tamanho = 40
numero = 20

tela = pygame.display.set_mode((tamanho * numero, tamanho * numero))
relogio = pygame.time.Clock()

imagem_maca = pygame.image.load('maca.png').convert_alpha()


class Cobra:
    def __init__(self):
        self.corpo = [Vector2(5, 10), Vector2(4, 10), Vector2(3, 10)]
        self.direcao = Vector2(1, 0)
        self.novo_bloco = False

    def desenhar_cobra(self):
        for bloco in self.corpo:
            x_cobra = int(bloco.x * tamanho)
            y_cobra = int(bloco.y * tamanho)
            cobra = pygame.Rect(x_cobra, y_cobra, tamanho, tamanho)
            pygame.draw.rect(tela, (0, 30, 200), cobra)


    def mover_cobra(self):
        if self.novo_bloco == True:
            copia_corpo = self.corpo[:]
            copia_corpo.insert(0, copia_corpo[0] + self.direcao)
            self.corpo = copia_corpo[:]
            self.novo_bloco = False
        else:
            copia_corpo = self.corpo[:-1]
            copia_corpo.insert(0, copia_corpo[0] + self.direcao)
            self.corpo = copia_corpo[:]


    def adicionar_bloco(self):
        self.novo_bloco = True


class Maca:
    def __init__(self):
        self.aleatorio()

    def desenhar_maca(self):
        maca = pygame.Rect(int(self.posicao.x * tamanho), int(self.posicao.y * tamanho), tamanho, tamanho)
        tela.blit(imagem_maca, maca)
        #pygame.draw.rect(tela, (200, 20, 0), maca)


    def aleatorio(self):
        self.x = randint(0, numero - 1)
        self.y = randint(0, numero - 1)
        self.posicao = Vector2(self.x, self.y)


class Jogo:
    def __init__(self):
        self.cobra = Cobra()
        self.maca = Maca()

    def carregar(self):
        self.cobra.mover_cobra()
        self.colisao()
        self.perdeu()

    def desenhar_elementos(self):
        self.maca.desenhar_maca()
        self.cobra.desenhar_cobra()


    def colisao(self):
        if self.maca.posicao == self.cobra.corpo[0]:
            self.maca.aleatorio()
            self.cobra.adicionar_bloco()

    def perdeu(self):
        if not 0 <= self.cobra.corpo[0].x < numero or not 0 <= self.cobra.corpo[0].y < numero:
            self.fim_de_jogo()

        for bloco in self.cobra.corpo[1:]:
            if bloco == self.cobra.corpo[0]:
                self.fim_de_jogo()

    def fim_de_jogo(self):
        pygame.quit()
        exit()

    def pontos(pontos):
        pontuacao = fonte.render('PONTUACAO: ' + str(pontos), True, (255, 255, 255))
        tela.blit(pontuacao, (0, 0))


    def recorde(recorde):
        pontuacao = fonte.render('RECORDE: ' + str(recorde), True, (255, 255, 255))
        tela.blit(pontuacao, (600, 0))


recorde = 0
carregar_tela = pygame.USEREVENT
pygame.time.set_timer(carregar_tela, 150)

jogo = Jogo()

fonte = pygame.font.SysFont('Boink Let', 30)

while True:
    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            exit()

        if event.type == carregar_tela:
            jogo.carregar()

        if event.type == KEYDOWN:
            if event.key == K_w:
                if jogo.cobra.direcao.y != 1:
                    jogo.cobra.direcao = Vector2(0, -1)

            if event.key == K_s:
                if jogo.cobra.direcao.y != -1:
                    jogo.cobra.direcao = Vector2(0, 1)

            if event.key == K_a:
                if jogo.cobra.direcao.x != 1:
                    jogo.cobra.direcao = Vector2(-1, 0)

            if event.key == K_d:
                if jogo.cobra.direcao.x != -1:
                    jogo.cobra.direcao = Vector2(1, 0)

    tela.fill((0, 100, 20))
    jogo.desenhar_elementos()
    relogio.tick(60)
    pygame.display.flip()
