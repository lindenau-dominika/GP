def ekwipunek():
    player.execute("/clear")
    mobs.give(mobs.target(NEAREST_PLAYER), DIAMOND_PICKAXE, 1)
    mobs.give(mobs.target(NEAREST_PLAYER), DIAMOND_AXE, 1)
    mobs.give(mobs.target(NEAREST_PLAYER), DIAMOND_CHESTPLATE, 1)
    mobs.give(mobs.target(NEAREST_PLAYER), DIAMOND_LEGGINGS, 1)
    mobs.give(mobs.target(NEAREST_PLAYER), DIAMOND_HELMET, 1)
    mobs.give(mobs.target(NEAREST_PLAYER), DIAMOND_BOOTS, 1)
    mobs.give(mobs.target(NEAREST_PLAYER), ARROW, 64)
    mobs.give(mobs.target(NEAREST_PLAYER), BOW, 1)

#funkcja odpowiedzialna za przygotowanie areny
def arenaKonstruktor():
    #ustawiamy noc
    gameplay.time_set(DayTime.NIGHT)
    #pobieramy aktualne kordy gracza z małym przesuniecięm na osi x tak żeby arena nie budowała się na graczu
    pozycja=positions.add(player.position(), pos(10, 0, 0))
    x=pozycja.get_value(Axis.X)
    y=pozycja.get_value(Axis.Y)
    z=pozycja.get_value(Axis.Z)
    #tworzymy arenę
    blocks.fill(STONE_BRICKS, world(x,y,z),world(x+40,y+4,z+40))
    #tworzymy w narożnikach areny diamentowe pola potrzebne dla bloku beacon aby ten mógł wypuścić wiązkę światła
    blocks.fill(DIAMOND_BLOCK, world(x,y+4,z), world(x+2,y+4,z+2))
    blocks.fill(DIAMOND_BLOCK, world(x+38,y+4,z), world(x+40,y+4,z+2))
    blocks.fill(DIAMOND_BLOCK, world(x,y+4,z+38), world(x+2,y+4,z+40))
    blocks.fill(DIAMOND_BLOCK, world(x+38,y+4,z+38), world(x+40,y+4,z+40))

    #dodajemy bloki beacon
    blocks.place(BEACON, world(x+1,y+5,z+1))
    blocks.place(BEACON, world(x+39,y+5,z+1))
    blocks.place(BEACON, world(x+1,y+5,z+39))
    blocks.place(BEACON, world(x+39,y+5,z+39))

    #tworzymy schody
    for i in range(15,21):
        shapes.line(STONE_BRICK_STAIRS, world(x-4,y,z+i), world(x,y+4,z+i))
 

player.on_chat("arena", arenaKonstruktor)
player.on_chat("ekwipunek", ekwipunek)
