# mundo-caotico
'''
Decripcion:  Reeborg debe atravesar 
un campo de 5x5 en zig-zag.
Pre: Reeborg está en la posición (1,1), mira al Este.
Pos: Reeborg está en la posición (5,5) y mira al Este.'''
global medicina
def walk():
    global energia # variable global 
    energia= 7 # declaracion de variables
    energia_guardada=0
    goloso=0
    tulipan=0
    manzana=0
    medicina=0
    #reeborg se mueve y hace descuento en la energia
    
    while (energia > 0 and front_is_clear()):
        energia= energia - 1 # con cada mivimiento se descuenta energia
        move()
        
        if object_here(): #verifica paso a paso si hay un objeto y de que tipo
            if object_here("apple"):
                if manzana==3: # si la energia ya recolectada es de tres manzanas, se almacena en otra variable
                    energia_guardada= energia_guardada+1
                else: #de lo contrario hace el proceso normal
                    take()
                    energia= energia +7
                    manzana= manzana +1

            if object_here("token"):
                if energia_guardada > 0 :#si la energia se agota reeborg utiliza la de las manzanas recolectadas
                    energia= enrgia+ (energia_guardada* 7)
                else:
                    while(manzana >=0): #deja las manzanas que ha recolectado 
                        put("apple")
                        manzana=manzana -1
                    
            if object_here("tulip"):
                if medicina==1: # verifica que ya tenga la vacuna
                    tulipan= 0
                else:
                    tulipan = tulipan +1 
                    energia= energia-(tulipan *2)# hace el descuento de enrgia
            if object_here("triangle"):
                medicina= 1
    if energia ==0:
        print("ya no tengo energia, intentalo nuevamente")
'''
Descripcion: Esta función hace que reeborg gire 
a la derecha
pre: reeborg mira al oeste 
pos: reeborg mira al este
'''
def girarDerecha():
    global energia
    repeat 3:
        turn_left()
    move()
    energia= energia - 1
    repeat 3:
        turn_left()
'''
Descripcion: Esta funcion hace que Reeborg gire a la izquierda
pre: reeborg mira al este
pos: reeborg mira al oeste
'''
def girarIzquierda():
    global energia
    turn_left()
    move()
    energia= energia - 1
    turn_left()
'''
Descripcion: Esta funcion hace que todo el programa
se ejecute de manera ordenada
pre: reeborg mira al este
pos: reeborg esta en casa e informa con cuanta energia 
llego.
'''
def zigzag():
    global energia
    repeat 2:
        walk()
        girarIzquierda()
        walk()
        girarDerecha()
    walk()
    print("ha terminado el juego, su energia es de:", energia)
        
        
zigzag()
