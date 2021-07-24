# Hangman-game
# Please check the website below to get hangman word_list and stages logo.
#https://replit.com/@SophiaLai1/Day-7-Hangman-game-finished#hangman_words.py
#from hangman_words import word_list
#from replit import clear
#TODO-1: - Update the word list to use the 'word_list' from hangman_words.py


import random
word_list = ["ardvark", "baboon", "camel"] # You can add more words into word_list.
running = True
while running:
  chosen_word = random.choice(word_list)
  word_length = len(chosen_word)

  end_of_game = False
  lives = 6

  #TODO-3: - Import the logo from hangman_art.py and print it at the start of the game.
  from hangman_art import stages,logo
  print(logo)

  #Testing code
  #print(f'Pssst, the solution is {chosen_word}.')
  #Create blanks
  display = []
  for _ in range(word_length):
      display += "_"

  while not end_of_game:
      print(f"{' '.join(display)}") 
      guess = input("Guess a letter: ").lower()
      if guess in display:
        print(f"You have already guessed this {guess} letter.")
      #TODO-4: - If the user has entered a letter they've already guessed, print the letter and let them know.
      
      #Check guessed letter
      for position in range(word_length):
          letter = chosen_word[position]
          
          #print(f"Current position: {position}\n Current letter: {letter}\n Guessed letter: {guess}")
          if letter == guess:
              display[position] = letter
      #Check if user is wrong.
              
          #TODO-5: - If the letter is not in the chosen_word, print out the letter and let them know it's not in the word.
      if guess not in chosen_word:
        print(f"You guessed {guess}, it is not in the word. You lose a life!")

        lives -= 1
        if lives == 0:
          end_of_game = True
          print("You have no more lives, Game over!")
          print(f'Pssst, the solution is {chosen_word}.')

      #Join all the elements in the list and turn it into a String.
      print(f"{' '.join(display)}")

      #Check if user has got all letters.
      if "_" not in display:
          end_of_game = True
          print(f"Congratulations! The correct word is '{chosen_word}', you win!")
      #TODO-2: - Import the stages from hangman_art.py and make this error go away.
      print(stages[lives])
      
    # ask users if they want to play again.
  result = input("Type 'yes' if you want to go again. Otherwise type 'no'.\n").lower()
  if result == "yes":
      running = True
      clear()
  else:
      running = False
      print("Good bye!")
