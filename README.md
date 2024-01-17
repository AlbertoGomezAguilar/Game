# Game
Juego de MSMK AB-PROGRAMACION

import time
import numpy as np
import sys
import random


    # retraso en las salidas
def delay_print(s):
    # pintamos los caracteres 1 a 1
    for c in s:
        sys.stdout.write(c)
        sys.stdout.flush()
        time.sleep(0.05)

    # creación de clase ANILLO
class Anillo:
    def __init__(self, name, types, moves, EVs, health='++++++++++++++++++++'):
        # pasar las variables a atributos
        self.name = name
        self.types = types
        self.moves = moves
        self.attack = EVs['ATAQUE']
        self.defense = EVs['DEFENSA']
        self.health = health
        self.bars = 20 # Cantidad de salud

 # hace que los guerreros luchen entre si
    def fight(self, Anillo2):
        # mostrar la información de los participantes
        print("#__LA BATALLA EMPIEZA__#")
        print(f"\n{self.name}")
        print("TYPO/", self.types)
        print("ATAQUE/", self.attack)
        print("DEFENSA/", self.defense)
        print("LVL/", 3*(1+np.mean([self.attack,self.defense])))
        print("\nVS")
        print(f"\n{Anillo2.name}")
        print("TYPO/", Anillo2.types)
        print("ATAQUE/", Anillo2.attack)
        print("DEFENSA/", Anillo2.defense)
        print("LVL/", 3*(1+np.mean([Anillo2.attack,Anillo2.defense])))

        time.sleep(2)

  # clases de personaje y devilidades
        version = ['Guerrero', 'Mago', 'Arquero']
        for i,k in enumerate(version):
            if self.types == k:
                if Anillo2.types == k:
                    # son del mismo tipo
                    string_1_attack = '\nNo es muy efectivo...!'
                    string_2_attack = '\nNo es muy efectivo...!'

   # es mas fuerte
                if Anillo2.types == version[(i+1)%3]:
                    Anillo2.attack *= 2
                    Anillo2.defense *= 2
                    self.attack /= 2
                    self.defense /= 2
                    string_1_attack = '\nNo es muy efectivo...!'
                    string_2_attack = '\nEs muy efectivo!\n'

   # es mas debil
                if Anillo2.types == version[(i+2)%3]:
                    self.attack *= 2
                    self.defense *= 2
                    Anillo2.attack /= 2
                    Anillo2.defense /= 2
                    string_1_attack = '\nEs muy efectivo!\n'
                    string_2_attack = '\nNo es muy efectivo...!'

   # pelea
            # comprobar la salud de los personajes
        while (self.bars > 0) and (Anillo2.bars > 0):
   # mostrar vida
            print(f"\n{self.name}\t\tHP\t{self.health}")
            print(f"{Anillo2.name}\t\tHP\t{Anillo2.health}\n")

            print(f"Vamos {self.name}!")
  # mostrar movimientos
            for i, x in enumerate(self.moves):
                print(f"{i+1}.", x)
  # comprobar que es un movimiento valido
            index = int(input('Selecciona tu movimiento: '))
            while index < 1 or index > len(self.moves):
                print(f"\n Ese ataque no existe!")
                index = int(input('Selecciona tu movimiento: '))
            delay_print(f"\n{self.name} a usado {self.moves[index-1]}!")
            time.sleep(1)
            delay_print(string_1_attack)

   # determinar daño
            Anillo2.bars -= self.attack
            Anillo2.health = ""

            for j in range(int(Anillo2.bars+.1*Anillo2.defense)):
                Anillo2.health += "+"

  # mostrar vida 
            time.sleep(1)
            print(f"\n{self.name}\t\tHP\t{self.health}")
            print(f"{Anillo2.name}\t\tHP\t{Anillo2.health}\n")
            time.sleep(.5)

   # turno del segundo personaje
            if Anillo2.bars <= 0:
                delay_print("\n..." + Anillo2.name + ' a fallecido.')
                break
            print(f"Vamos {Anillo2.name}!")
            for i, x in enumerate(Anillo2.moves):
                print(f"{i+1}.", x)
            index = int(input('Selecciona tu movimiento: '))
            while index < 1 or index > len(self.moves):
                print(f"\n Ese ataque no existe!")
                index = int(input('Selecciona tu movimiento: '))
            delay_print(f"\n{Anillo2.name} a usado {Anillo2.moves[index-1]}!")
            time.sleep(1)
            delay_print(string_2_attack)

   # determinar daño
            self.bars -= Anillo2.attack
            self.health = ""

            for j in range(int(self.bars+.1*self.defense)):
                self.health += "+"

   # mostrar vida
            time.sleep(1)
            print(f"{self.name}\t\tHP\t{self.health}\n")
            print(f"{Anillo2.name}\t\tHP\t{Anillo2.health}\n")
            time.sleep(.5)

   # comprobar la salud de los personajes
            if self.bars <= 0:
                delay_print("\n..." + self.name + ' a fallecido.')
                break

        money = np.random.choice(5000)
        delay_print(f"\nHas saqueado a tu oponente, tenia ${money}.\n")

 # crear personajes
    if __name__ == '__main__':
      # crear personajes
      Aragorn = Anillo('Aragorn', 'Guerrero', ['Vertical', 'Horizontal', 'Golpe vorpal', 'Daga arrojadiza'], {'ATAQUE':12, 'DEFENSA': 11})
      Gandalf = Anillo('Gandalf', 'Mago', ['Bola de Fuego', 'Destello', 'Lanzas de hielo', 'Hola Mundo'],{'ATAQUE': 10, 'DEFENSA':10})
      Legolas = Anillo('Legolas', 'Arquero', ['Tiro', 'LLuvia de Flechas', 'Flecha de fuego', 'Bomba'],{'ATAQUE':10, 'DEFENSA':12})
      SolaireDeAstora = Anillo('SolaireDeAstora', 'Guerrero', ['Medalla de la luz', 'Horacion al sol', 'Pose T', 'Espada del sol'], {'ATAQUE':10, 'DEFENSA': 8})
      Merlin = Anillo('Merlin', 'Mago', ['Baile', 'Ataque buho', 'Espada voladora', 'Abracadabra'],{'ATAQUE': 8, 'DEFENSA':10})
      RobinHood = Anillo('RobinHood', 'Arquero', ['Tiro a la manzana', 'Drop de oro', 'Robo', 'Emboscada'],{'ATAQUE':11, 'DEFENSA':12})

      personajes = [Aragorn, Gandalf, Legolas, SolaireDeAstora, Merlin, RobinHood]

 # seleccionar personajes que luchen 
    pelean = np.random.choice(personajes)
    pelean2 = np.random.choice(personajes)

    pelean.fight(pelean2)
