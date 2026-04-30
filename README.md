import pygame
import random
pygame.init()

largura,altura = 400,600
tela = pygame.display.set_mode((largura,altura))
pygame.display.set_caption("jogo de desvio")
jogador = pygame.Rect(200,500,40,40)
obstaculos = []
relogio = pygame.time.Clock()
rodando = True
velocidade = 5
while rodando:
    pygame.draw.rect(tela,(0,255,0),jogador)
    tecla = pygame.key.get_pressed()
    if tecla[pygame.K_LEFT] and jogador.left > 0:
        jogador.x -= velocidade
    if tecla[pygame.K_RIGHT] and jogador.right < largura:
        jogador.x += velocidade

    def criar_obstaculo():
        x = random.randint(0,largura -40)
        return pygame.Rect(x,-40,40,40)
    
    for obstaculo in obstaculos:
        obstaculo.y += velocidade
        pygame.draw.rect(tela,(255,0,0),obstaculo)
        if obstaculo.colliderect(jogador):
            rodando = False
    
    if random.randint(1,30) == 1:
        obstaculos.append(criar_obstaculo())

    obstaculos = [obstaculo for obstaculo in obstaculos if obstaculo.y < altura]
    pygame.display.flip()
    tela.fill((0,0,0))
    relogio.tick(60)
    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            rodando = False

pygame.quit()
