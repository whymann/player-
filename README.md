# player-
import pygame
from player import player
pygame.init()
pygame.display.set_caption("top down grid game") # set the window title
screen = pygame.display.set_mode((1000,800)) # creats a game screen
clock = pygame.time.Clock() #set up clock
gameover = False # variable to run our game loop


#instantiate player
p1 = player()

#constants 
LEFT = 0
RIGHT = 1
UP = 2
DOWN = 3
keys = [False, False, False, False,False]# this is a list holds water each key pressed 

map = [[2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2],
       [2,3,3,3,3,2,2,3,3,2,2,2,2,2,2,2,2,2,2,2],
       [2,3,0,3,3,2,2,3,3,2,2,2,2,2,2,2,2,2,2,2],
       [2,0,0,2,2,2,2,3,3,2,3,3,3,3,3,3,3,3,3,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1,0,0,0,2],
       [2,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,0,2,3,3,3,0,0,3,0,2,2,0,0,0,0,0,0,2,2],
       [2,3,0,0,3,3,0,3,0,0,0,0,0,0,0,0,0,0,0,2],
       [2,2,2,2,2,2,2,2,0,0,0,0,0,0,0,0,0,0,2,2],
       [2,0,2,3,3,3,0,0,3,0,0,0,2,2,0,0,0,2,2,2],
       [2,3,2,0,3,3,0,3,0,0,0,2,0,0,2,0,2,0,2,2],
       [2,2,2,2,0,0,0,2,2,2,2,2,0,0,0,0,0,0,2,2],
       [2,0,2,3,3,3,0,0,3,2,2,0,2,2,0,0,0,0,2,2],
       [2,3,0,0,3,3,0,3,0,2,0,2,0,0,2,0,2,2,2,2],
       [2,2,2,2,2,2,2,2,2,2,2,2,0,2,0,0,0,0,2,2],
       [2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2,2]]


brick = pygame.image.load('brick.jpg')
dirt = pygame.image.load('wa wa.jpg')
rat  = pygame.image.load('rat.png')


while not gameover:# GAME LOOP==================================================
    clock.tick(60) #FPS
    #input section---------------------------------------------------------------
    for event in pygame.event.get(): # quit game if x is pressed in the top corner
        if event.type == pygame.QUIT:
            gameover = True
            
        if event.type == pygame.KEYDOWN:#keyborad input
            if event.key == pygame.K_LEFT:
                keys[LEFT]= True
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT] = True
            elif event.key == pygame.K_UP:
                keys[UP ]= True
            elif event.key == pygame.K_DOWN:
                keys[DOWN] = True
                
        elif event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT:
                keys[LEFT] = False
            elif event.key == pygame.K_RIGHT:
                keys[RIGHT] = False
                
            elif event.key == pygame.K_UP:
                keys[UP] = False
            elif event.key == pygame.K_DOWN:
                keys[DOWN] = False 
    # physics section--------------------------------------------------------------
    p1.move(keys,map)
    
    #Render section--------------------------------------------------------------------
   
    screen.fill((0,0,0)) # wipe screen so it doesn't smear
    #draw map
    for i in range(len(map)):
        for j in range(len(map[i])):
           if map[i][j] == 1:
              screen.blit(dirt, (j * 50, i * 50), (0, 0, 50, 50))
           if map[i][j] ==2:
              screen.blit(brick, (j * 50, i * 50), (0, 0, 50, 50))
           if map[i][j] ==3:
              screen.blit(rat, (j * 50, i * 50), (0, 0, 50, 50))
    p1.draw(screen)            
    pygame.display.flip() # this actually puts the pixles on the screen
    
# end game loop=====================================================================
pygame.quit() 
