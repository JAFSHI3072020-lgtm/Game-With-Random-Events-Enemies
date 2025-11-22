import random
def random_enemy():
    enemies = ["Goblin", "Bandit", "Giant Spider", "Skeleton Warrior", "Wild Boar"]
    return random.choice(enemies)
def random_event():
    events = [
        "You find a hidden stash of gold!",
        "You step into a trap and lose!",
        "You discover a healing spring!",
        "You find an old map that reveals shortcuts!",
        "A thief steals some of your supplies!"
    ]
    return random.choice(events)
def battle(enemy):
    print(f"\n⚔️ A {enemy} appears!")
    action = input("Do you fight or run? (fight/run): ").lower()
    if action == "fight":
        # 50/50 win or lose
        if random.random() < 0.5:
            print(f"You defeated the {enemy}! You continue your journey.\n")
            return True
        else:
            print(f"The {enemy} defeated you. You lose!\n")
            return False
    elif action == "run":
        # 70% chance to escape
        if random.random() < 0.7:
            print("You managed to escape safely!\n")
            return True
        else:
            print("You failed to run away and were defeated. You lose!\n")
            return False
    else:
        print("Invalid action. The enemy takes advantage and defeats you!\n")
        return False

def play_game():
    name = input("Type your name: ")
    print(f"\nGreetings, {name}! Welcome to the Random Encounter Adventure!\n")

    choice = input(
        "You stand at a fork in the road. Do you go left or right? (left/right): "
    ).lower()

    # -------------------------
    # LEFT PATH
    # -------------------------
    if choice == "left":
        print("\nYou walk along a dark forest trail...")
        
        # Random event occurs
        event = random_event()
        print("🎲 Random Event:", event)

        if "trap" in event:
            print("The trap was deadly. You lose.\n")
            print("Thanks for playing,", name + "!\n")
            return

        # Random enemy encounter
        enemy = random_enemy()
        survived = battle(enemy)

        if not survived:
            print("Thanks for playing,", name + "!\n")
            return

        print("You reach a clearing with a treasure chest...")
        if random.random() < 0.5:
            print("🎉 The chest contains rare gems! YOU WIN!\n")
        else:
            print("💥 The chest was a mimic! It eats you. You lose.\n")

    # -------------------------
    # RIGHT PATH
    # -------------------------
    elif choice == "right":
        print("\nYou follow a rocky mountain path...")

        # Random enemy first
        enemy = random_enemy()
        survived = battle(enemy)

        if not survived:
            print("Thanks for playing,", name + "!\n")
            return

        # Random event after surviving
        event = random_event()
        print("🎲 Random Event:", event)

        if "trap" in event:
            print("The trap was fatal. You lose.\n")
            print("Thanks for playing,", name + "!\n")
            return
        elif "gold" in event:
            print("You feel rich and powerful. YOU WIN!\n")
        else:
            print("You safely reach the end of the mountain trail. YOU WIN!\n")

    else:
        print("\nInvalid path. You trip and fall off a cliff. You lose.\n")

    print("Thanks for playing,", name + "!\n")


# ==============================
#       MAIN GAME LOOP
# ==============================

while True:
    play_game()
    replay = input("Would you like to play again? (yes/no): ").lower()
    if replay != "yes":
        print("\nThanks for adventuring! Goodbye!")
        break
    print("\nRestarting game...\n")

