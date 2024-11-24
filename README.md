- 👋 Hi, I’m @suryamanikumar111
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
suryamanikumar111/suryamanikumar111 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import random
import time

# Game Constants
MAX_HEALTH = 100
WEAPONS = {
    "Pistol": {"damage": 15, "accuracy": 80},
    "Shotgun": {"damage": 40, "accuracy": 60},
    "Rifle": {"damage": 30, "accuracy": 75},
    "Sniper": {"damage": 50, "accuracy": 50}
}

# Player and Enemy Classes
class Character:
    def __init__(self, name, health=MAX_HEALTH):
        self.name = name
        self.health = health
    
    def take_damage(self, damage):
        self.health -= damage
        if self.health < 0:
            self.health = 0

    def is_alive(self):
        return self.health > 0

# Attack function to simulate shooting
def attack(player, weapon, enemy):
    print(f"{player.name} attacks with {weapon}.")
    hit_chance = random.randint(1, 100)
    
    if hit_chance <= WEAPONS[weapon]["accuracy"]:
        damage = WEAPONS[weapon]["damage"]
        print(f"Hit! {enemy.name} takes {damage} damage.")
        enemy.take_damage(damage)
    else:
        print("Missed! No damage dealt.")

# Game loop function
def game_loop():
    # Player setup
    player_name = input("Enter your character name: ")
    player = Character(player_name)
    
    # Enemy setup
    enemy = Character("Enemy")
    
    print("\nYour enemy is ready for battle!\n")
    
    # Weapon selection
    print("Choose your weapon:")
    for i, weapon in enumerate(WEAPONS.keys(), 1):
        print(f"{i}. {weapon} (Damage: {WEAPONS[weapon]['damage']}, Accuracy: {WEAPONS[weapon]['accuracy']}%)")
    
    weapon_choice = int(input("Select a weapon (1-4): "))
    chosen_weapon = list(WEAPONS.keys())[weapon_choice - 1]
    
    # Game battle loop
    while player.is_alive() and enemy.is_alive():
        print(f"\n{player.name}'s Health: {player.health}/{MAX_HEALTH}")
        print(f"Enemy's Health: {enemy.health}/{MAX_HEALTH}")
        
        # Player's turn to attack
        attack(player, chosen_weapon, enemy)
        time.sleep(1)

        # Check if enemy is defeated
        if not enemy.is_alive():
            print("\nYou defeated the enemy!")
            break
        
        # Enemy's turn to attack
        enemy_weapon = random.choice(list(WEAPONS.keys()))
        print(f"\n{enemy.name} attacks with {enemy_weapon}.")
        attack(enemy, enemy_weapon, player)
        time.sleep(1)

        # Check if player is defeated
        if not player.is_alive():
            print("\nYou were defeated by the enemy!")
            break
    
    # End of the game
    print("\nGame Over!")
    if player.is_alive():
        print(f"{player.name} wins!")
    else:
        print(f"{player.name} loses...")

# Start the game
if __name__ == "__main__":
    game_loop()
