class Pokemon:
    def __init__(self, name, level, type):
        self.name = name
        self.level = level
        self.type = type.title()
        self.max_health = level
        self.health = level
        self.is_knocked_out = True
        self.max_experience = 50
        self.experience = 0

    def lose_health(self, value):
        self.health = max(0, self.health - value)
        print("Your Pokemon's health has decreased! {name} has now {health} health.".format(name = self.name, health = self.health))
        if self.health == 0:
            self.knock_out()

    def regain_health(self):
        self.health = self.max_health
        print("{name} has now {health} health.".format(name = self.name, health = self.health))

    def knock_out(self):
        self.is_knocked_out = True
        print("Ouch! {name} is knocked out!".format(name = self.name))

    def attack(self, other):
        try:
            print("{attacker_name} attacked {attacked_name}!".format(attacker_name = self.name, attacked_name = other.name))
            if (self.type == "Grass" and other.type == "Water") or (self.type == "Water" and other.type == "Fire") or (self.type == "Fire" and other.type == "Grass"):
                other.lose_health(2*self.level)
                self.experience += 2*self.level
            else:
                other.lose_health(int(self.level/2))
                self.experience += int(self.level/2)
            if self.experience >= self.max_experience:
                self.experience = 0
                self.max_experience += 50
                self.level += 1
                self.max_health += 1
                print("Hooray! Your Pokemon has leveled up!")
        except NameError:
            print("Please choose a currently available trainer.")

class Trainer:
    def __init__(self, name, pokemons, potions, active_pokemon):
        self.name = name
        self.pokemons = pokemons
        self.potions = potions
        self.active_pokemon = active_pokemon

    def use_potion(self):
        print("Your are using a potion on {pokemon}.".format(pokemon = self.pokemons[self.active_pokemon].name))
        self.pokemons[self.active_pokemon].regain_health()
        if self.potions > 0:
            self.potions -= 1
        print("You currently have {number} potions.".format(number = self.potions))

    def attack_trainer(self, other):
        if self.pokemons[self.active_pokemon].is_knocked_out == False:
            print("You have begun attacking {trainer_name}'s Pokemon {pokemon_name}.".format(trainer_name = other.name, pokemon_name = other.pokemons[other.active_pokemon].name))
            self.pokemons[self.active_pokemon].attack(other.pokemons[other.active_pokemon])
        else:
            print("*Oof* You cannot use {name} because it is knocked out. Poor guy!".format(name = self.pokemons[self.active_pokemon].name))

    def switch_active_pokemon(self, value):
        try:
            if value == self.active_pokemon:
                print("You are already using this Pokemon.")
            else:
                if self.pokemons[value].is_knocked_out == True:
                    print("Please choose a Pokemon that is not knocked out.")
                else:
                    self.active_pokemon = value
                    print("You successfully switched to {name}".format(name = self.pokemons[self.active_pokemon].name))
        except IndexError:
            print("You do not have sufficient Pokemons. Please choose a Pokemon index which is in range.")

muff = Pokemon("Muff", 69, "Grass")
puff = Pokemon("Puff", 45, "Water")
huff = Pokemon("Huff", 78, "Fire")

iulia = Trainer("Iulia", [muff, huff], 18, 1)
diana = Trainer("Diana", [puff], 4, 0)

iulia.use_potion()
iulia.switch_active_pokemon(0)
iulia.attack_trainer(diana)
diana.attack_trainer(iulia)
