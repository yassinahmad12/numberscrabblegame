# numberscrabblegame
#FILE:CS112_A1_T2_2_20230464
#PURPOSE:This is number scrabble game you must choose 3 numbers from 1 to 9 that their sum is equal to 15 to win
#AUTHOR:Yassin Ahmad Hassan Ahmad
#ID:20230464

print("***Welcome to Number Scrabble***\n")        #welcome message
numbers_list = [1, 2, 3, 4, 5, 6, 7, 8, 9]
player1score = []
player2score = []       #empty list so we can store the score here

def player1input():
    global player1score #"global' here is used because player1score is initialized globaly so we can access it
    while True:
        try:                                                                         #validate the input so the user must enter an integer
            player1num = int(input("Player 1, please enter a number from 1 to 9: "))
            break
        except ValueError:
            print ("Error,Please enter a valid integer number")
    if 1 <= player1num <= 9 and player1num in numbers_list: #input validation,
        numbers_list.remove(player1num) #remove the chosen number from the list
        player1score.append(player1num) # add it to player 1 list
        return player1score
    else:
        print("Invalid input or number chosen before. Please try again.")  #error msg
        player1input()

def player2input():
    global player2score #"global' here is used because player2 score is initialized globaly so we can access it
    while True:
        try:
            player2num = int(input("Player 2, please enter a number from 1 to 9: ")) #validate the input so the user must enter an integer
            break
        except ValueError:
            print ("Error,Please enter a valid integer number")
    if 1 <= player2num <= 9 and player2num in numbers_list:
        numbers_list.remove(player2num)    #remove the chosen number from the list
        player2score.append(player2num)    # add it to player 2 list
        return player2score
    else:
        print("Invalid input or number already chosen. Please try again.")
        player2input()

def main_game():    #the main game function
    count = 0

    while count < 9:  # Change the loop condition to run until both players have taken four turns in total
        print("Numbers remaining:", numbers_list)
        player1input()  # Call the function for player 1's turn
        count += 1

        # iterates over all possible combinations of three numbers for player1
        if len(player1score) >= 3:
            for x in range(len(player1score)):
                for y in range(x + 1, len(player1score)):
                    for z in range(y + 1, len(player1score)):
                        if player1score[x] + player1score[y] + player1score[z] == 15:
                            print("***PLAYER 1 IS THE WINNER***")
                            return

        # Check if the game has ended after player 1's turn to avoid unnecessary input from player 2
        if count < 9:
            print("Numbers remaining:", numbers_list)
            player2input() # Call the function for player 2's turn
            count += 1

            # iterates over all possible combinations of three numbers for player2
            if len(player2score) >= 3:
                for x in range(len(player2score)):
                    for y in range(x + 1, len(player2score)):
                        for z in range(y + 1, len(player2score)):
                            if player2score[x] + player2score[y] + player2score[z] == 15:
                                print("***PLAYER 2 IS THE WINNER***")
                                return

    # If no winner is found after all turns, print the draw message
    print("No player wins, it's a draw.")

main_game()
