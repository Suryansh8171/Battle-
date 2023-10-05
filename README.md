# Battle-
mind your health but defeat is inevitable 
keep in mind the amount of health left whenever you fight a demon, regenerate on time or else you will lose the game 
remember what you got in inventory 





import random

class Player:
    def __init__(self, name, health=100, attack=10, coins=0):
        self.name = name
        self.health = health
        self.max_health = health
        self.attack = attack
        self.coins = coins
        self.inventory = []

    def take_damage(self, damage):
        self.health -= damage

    def is_alive(self):
        return self.health > 0

    def add_item_to_inventory(self, item):
        self.inventory.append(item)

    def use_item(self, item):
        if item in self.inventory:
            if item == "Health Potion" and self.health < self.max_health:
                self.health = min(self.max_health, self.health + 20)
                print("You used a Health Potion and restored 20 health points.")
                self.inventory.remove(item)
            else:
                print("You can't use this item now.")
        else:
            print("Item not found in your inventory.")

class Monster:
    def __init__(self, name, health, attack, coins):
        self.name = name
        self.health = health
        self.attack = attack
        self.coins = coins

    def take_damage(self, damage):
        self.health -= damage

    def is_alive(self):
        return self.health > 0

def battle(player, monster):
    print(f"You are battling {monster.name}!")
    while player.is_alive() and monster.is_alive():
        player_damage = random.randint(1, player.attack)
        monster_damage = random.randint(1, monster.attack)

        player.take_damage(monster_damage)
        monster.take_damage(player_damage)

        print(f"You attacked {monster.name} for {player_damage} damage.")
        print(f"{monster.name} attacked you for {monster_damage} damage.")
        print(f"Your health: {player.health} | {monster.name}'s health: {monster.health}\n")

    if player.is_alive():
        print(f"You defeated {monster.name} and earned {monster.coins} coins!")
        player.coins += monster.coins
        return True
    else:
        print("Game Over. You were defeated.")
        return False
    # ... (unchanged code for battle function)

def main():
    player_name = input("Enter your name: ")
    player = Player(player_name)
    monsters = [Monster("Goblin", 20, 5, 10), Monster("Dragon", 50, 15, 50), Monster("Skeleton", 15, 3, 5)]

    while True:
        print("\n1. Explore\n2. View Inventory\n3. Use Item\n4. Quit")
        choice = input("Enter your choice: ")

        if choice == "1":
            monster = random.choice(monsters)
            if battle(player, monster):
                item = monster.name + " Tooth"
                player.add_item_to_inventory(item)
                print(f"You obtained {item}!")
        elif choice == "2":
            print("Inventory: ", player.inventory)
            print("Coins: ", player.coins)
        elif choice == "3":
            item_to_use = input("Enter the item you want to use: ")
            player.use_item(item_to_use)
        elif choice == "4":
            print("Thanks for playing!")
            break
        else:
            print("Invalid choice. Try again.")

if __name__ == "__main__":
    main()
