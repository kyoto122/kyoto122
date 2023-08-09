import pygame
import random

# Initialisation
pygame.init()

# Paramètres de la fenêtre
largeur_fenetre = 800
hauteur_fenetre = 600
fenetre = pygame.display.set_mode((largeur_fenetre, hauteur_fenetre))
pygame.display.set_caption("Jeu de Blocs")

# Couleurs
blanc = (255, 255, 255)
noir = (0, 0, 0)
couleurs_blocs = [(255, 0, 0), (0, 255, 0), (0, 0, 255), (255, 255, 0), (0, 255, 255)]

# Joueur
joueur_largeur = 100
joueur_hauteur = 20
joueur_x = (largeur_fenetre - joueur_largeur) // 2
joueur_y = hauteur_fenetre - joueur_hauteur - 10
joueur_vitesse = 5

# Blocs
nombre_blocs = 50
bloc_largeur = 60
bloc_hauteur = 20
blocs = []

for i in range(nombre_blocs):
    couleur = random.choice(couleurs_blocs)
    blocs.append(pygame.Rect(random.randint(0, largeur_fenetre - bloc_largeur), random.randint(50, 300), bloc_largeur, bloc_hauteur))

# Boucle de jeu
continuer = True
horloge = pygame.time.Clock()

while continuer:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            continuer = False
    
    touches = pygame.key.get_pressed()
    if touches[pygame.K_LEFT] and joueur_x > 0:
        joueur_x -= joueur_vitesse
    if touches[pygame.K_RIGHT] and joueur_x < largeur_fenetre - joueur_largeur:
        joueur_x += joueur_vitesse
    
    fenetre.fill(blanc)
    
    # Dessin des blocs
    for bloc in blocs:
        pygame.draw.rect(fenetre, bloc[1], bloc[0])
    
    # Dessin du joueur
    pygame.draw.rect(fenetre, noir, (joueur_x, joueur_y, joueur_largeur, joueur_hauteur))
    
    pygame.display.flip()
    horloge.tick(60)

pygame.quit()
