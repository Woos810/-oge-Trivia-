# -oge-Trivia-
import random
import time
import threading

def countdown_timer(seconds, stop_event):
    for i in range(seconds, 0, -1):
        if stop_event.is_set():
            break
        time.sleep(1)
    if not stop_event.is_set():
        print("\n⏰ WOOF WOOF! Time’s up, pup! Onward we go! 🐾🌈")

def doge_barkCelebration():
    print("🐶 WOOF WOOF! You’re a barking genius! 🏆✨")

def doge_trivia_game():
    print("🎉🐶 Welcome to the ULTIMATE Doge Trivia Bash! 🚀✨")
    print("⏰ Answer in 15 seconds or hear the Doge bark! WOOF! 🐕")
    print("Pick a, b, c, or d—type fast and let’s have a blast! 🌟🐾\n")

    # Enhanced questions: [question, options, correct_answer, fun_response]
    questions = [
        [
            "What goofy pup is the Dogecoin star? 🐶💫",
            ["a) Sneaky Kitty 😺", "b) Shiba Inu 🐕", "c) Wacky Dino 🦖", "d) Hoppy Bunny 🐰"],
            "b",
            "🎈 WOOF! The Shiba Inu rules Doge-land! 🌟🐾"
        ],
        [
            "Who’s the silly boss who loves Dogecoin? 😂🚀",
            ["a) Mickey Mouse 🐭", "b) Elon Musk 🌍", "c) SpongeBob 🧽", "d) Grumpy Cat 😾"],
            "b",
            "🌙 Yay-yay! Elon’s the Doge rocket man! 🦸‍♂️✨"
        ],
        [
            "What’s the coolest Doge word ever? 🗣️🌈",
            ["a) Snooze Time 😴", "b) Much Wow 🎉", "c) Blah Blah 😐", "d) Quiet Paws 🤫"],
            "b",
            "🎡 Woohoo! Much wow is Doge magic! 🐶💖"
        ],
        [
            "What’s Dogecoin for, little HODLer? 💰🎲",
            ["a) Candy Cash 🍭", "b) Fun Internet Coins 🎮", "c) Rocket Fuel ⛽", "d) Toy Trucks 🚚"],
            "b",
            "💰 Sweet bark! It’s fun money for games! 🌟🎠"
        ],
        [
            "Where’s Doge flying with its cape? 🦸‍♀️🌌",
            ["a) Puppy Park 🌳", "b) The Moon 🌕", "c) Candy Store 🍬", "d) Cloud Castle ☁️"],
            "b",
            "🚀 Zoom-zoom! Doge blasts to the moon! 🌠🐾"
        ],
        [
            "What color is the Doge coin logo? 🎨💿",
            ["a) Blue like the sky 🌊", "b) Gold like treasure 🪙", "c) Red like a rocket 🔥", "d) Green like slime 🐸"],
            "b",
            "🌟 Shiny win! It’s gold and super cool! 💎🐶"
        ]
    ]

    score = 0
    total_questions = len(questions)

    # Shuffle for extra fun
    random.shuffle(questions)

    # Game loop with bark-tastic timer
    for i, (question, options, correct_answer, response) in enumerate(questions, 1):
        print(f"\n🎲✨ Question {i}: {question}")
        for option in options:
            print(option)

        # Timer magic
        stop_event = threading.Event()
        timer_thread = threading.Thread(target=countdown_timer, args=(15, stop_event))
        timer_thread.start()

        # Kiddo answers
        user_answer = input("Your answer (a/b/c/d): ").lower().strip()
        stop_event.set()  # Stop the bark timer
        timer_thread.join()  # Sync up

        if user_answer == correct_answer:
            print(f"🐶 {response}")
            if i == total_questions and score == i - 1:  # Perfect so far, last question
                doge_barkCelebration()
            score += 1
        elif user_answer in ['a', 'b', 'c', 'd']:
            print(f"🌈 Oops-a-doodle! It was '{correct_answer}'. You’re still a Doge rockstar! 🎸🐾")
        else:
            print(f"⏰ WOOF WOOF! Time’s gone or silly paws! It was '{correct_answer}'. Next adventure! 🌟")

    # Epic score reveal
    print(f"\n🎉🎶 Game Over, Doge Buddy! Your score: {score}/{total_questions} 🌟")
    if score == total_questions:
        print("🌕 WOOF WOOF! Perfect score! You’re the Doge Emperor—bow wow wow! 👑🐶✨")
        doge_barkCelebration()
    elif score >= total_questions // 2:
        print("🚀 Bark-tastic! You’re a Doge rocket pup—zooming high! 🌈🐾")
    else:
        print("🐶 Aww, cute pup! You’re a bouncy Doge—more fun to come! 🎈💖")

    # Replay with extra bark
    replay = input("\n🎡 Play again, little barker? (yes/no): ").lower()
    if replay == "yes":
        print("\n🐕 WOOF WOOF! New game time—let’s bounce! 🌟🎉")
        doge_trivia_game()
    else:
        print("🐾 Thanks for barking along, Doge pal! Catch ya later—much wow! 🚀🌈")

# Launch the party
if __name__ == "__main__":
    doge_trivia_game()
​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​​
