# Poker
Grade 11 Assignment 
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Texas_Hold_em_Poker
{
    class Poker
    {
        //Global variable of the unshuffled deck array
        static string[] unshuffled = new string[52];
        
        //Constants to store the value of each type of hand
        const int STRAIGHT_FLUSH = 9;
        const int FOUR_OF_A_KIND = 8;
        const int FULL_HOUSE = 7;
        const int FLUSH = 6;
        const int STRAIGHT = 5;
        const int THREE_OF_A_KIND = 4;
        const int TWO_PAIRS = 3;
        const int PAIRS = 2;
        const int NOTHING = 1;

        //global variable of the computer and human's money amount and the pot value
        static int computerAmount = 1000;
        static int humanAmount = 1000;
        static int oldpot = 0;
        static int pot = 0;
         

        static void Main(string[] args)
        {
            

            //An array to store the shuffled cards 
            string[] shuffled = new string[52];

            //An 2 dimensional array to store the human cards and the computer hands
            string[,] cards = new string[2,7];
            unshuffled[0] = "♠A";
            unshuffled[1] = "♠2";
            unshuffled[2] = "♠3";
            unshuffled[3] = "♠4";
            unshuffled[4] = "♠5";
            unshuffled[5] = "♠6";
            unshuffled[6] = "♠7";
            unshuffled[7] = "♠8";
            unshuffled[8] = "♠9";
            unshuffled[9] = "♠10";
            unshuffled[10] = "♠J";
            unshuffled[11] = "♠Q";
            unshuffled[12] = "♠K";

            unshuffled[13] = "♥A";
            unshuffled[14] = "♥2";
            unshuffled[15] = "♥3";
            unshuffled[16] = "♥4";
            unshuffled[17] = "♥5";
            unshuffled[18] = "♥6";
            unshuffled[19] = "♥7";
            unshuffled[20] = "♥8";
            unshuffled[21] = "♥9";
            unshuffled[22] = "♥10";
            unshuffled[23] = "♥J";
            unshuffled[24] = "♥Q";
            unshuffled[25] = "♥K";

            unshuffled[26] = "♣A";
            unshuffled[27] = "♣2";
            unshuffled[28] = "♣3";
            unshuffled[29] = "♣4";
            unshuffled[30] = "♣5";
            unshuffled[31] = "♣6";
            unshuffled[32] = "♣7";
            unshuffled[33] = "♣8";
            unshuffled[34] = "♣9";
            unshuffled[35] = "♣10";
            unshuffled[36] = "♣J";
            unshuffled[37] = "♣Q";
            unshuffled[38] = "♣K";

            unshuffled[39] = "♦A";
            unshuffled[40] = "♦2";
            unshuffled[41] = "♦3";
            unshuffled[42] = "♦4";
            unshuffled[43] = "♦5";
            unshuffled[44] = "♦6";
            unshuffled[45] = "♦7";
            unshuffled[46] = "♦8";
            unshuffled[47] = "♦9";
            unshuffled[48] = "♦10";
            unshuffled[49] = "♦J";
            unshuffled[50] = "♦Q";
            unshuffled[51] = "♦K";

            cards[0,0] = "";
            cards[0,1] = "";
            cards[0,2] = "";
            cards[0,3] = "";
            cards[0,4] = "";
            cards[0,5] = "";
            cards[0,6] = "";

            cards[1,0] = "";
            cards[1,1] = "";
            cards[1,2] = "";
            cards[1,3] = "";
            cards[1,4] = "";
            cards[1,5] = "";
            cards[1,6] = "";
            
            //Call menu procedure

            //ComputerStraight(cards);

            Menu(cards,shuffled);
        }

        //Menu procedure that gives the user several options
        static void Menu(string[,] cards,string[] shuffled)
        {
            Console.WriteLine("WELCOME TO TEXAS HOLD'EM POKER");
            Console.WriteLine("1. Start Game");
            Console.WriteLine("2. Help");
            Console.WriteLine("3. Credits");
            Console.WriteLine("4. Exit");
            Console.Write("Command: ");
            //Store command value in string variable
            string command = Console.ReadLine();

            //If command = 1 call the play procedure
            if (command == "1")
            {
                //Play procedure
                Play(cards,shuffled, pot);
            }
            
            //If command = 2 call the help procedure 
            else if (command == "2")
            {
                Help(cards, shuffled);
            }

            //If command = 3 call credits procedure
            else if (command == "3")
            {
                Credits(cards, shuffled);
            }

            //If command = 4 exit this program
            else if (command == "4")
            {
                Console.WriteLine("Thank you for playing Texas Hold'em Poker");
                Environment.Exit(0);
            }

            //Otherwise, display "ERROR"
            else
            {
                Console.WriteLine("ERROR");
            }
        }

        //Procedure that randomizes the deck as if it is being shuffled
        static void ShuffleDeck(string[] shuffled)
        {
            //Random number generator
            Random random = new Random();
            for (int counter = 0; counter < 52; counter++)
            {
                //The number will be generated between 0-51
                int rnd = random.Next(0, 51);
                //The shuffled array will equal to the randomized unshuffled array
                shuffled[counter] = unshuffled[rnd];
                //The last card is put in the position of the randomized card
                unshuffled[rnd] = unshuffled[51 - counter];

            }
        }

        //Play procedure that allows the user to play the game
        static void Play(string[,] cards, string[] shuffled, int pot)
        {
            //call the shuffle deck procedure 
            ShuffleDeck(shuffled);

            Console.ForegroundColor = ConsoleColor.Cyan;
            //Call the procedure that deals the human card
            DealHumanCard(cards, shuffled);

            
            
            //Display human cards
            Console.WriteLine(cards[0,5] + " " + cards[0,6]);
            //Call the procedure that deals the computer cards
            DealComputerCard(cards, shuffled);

            Console.ResetColor(); 
            
            Console.WriteLine(cards[1, 5] + " " + cards[1, 6]);

            //Call the deal cards function
            DealCards(cards, shuffled);

            Console.ForegroundColor = ConsoleColor.Cyan;

            //Display the flop, the first three cards dealt 
            Console.WriteLine("Flop: " + cards[0,0] + " " + cards[0,1] + " " + cards[0,2]);

            Console.ResetColor(); 
            
            //Store the computer raise amount in int variable and make it equal to the computer command center function
            int computerRaiseAmount = ComputerCommandCenter(cards);

            //Call the command center that gives the user options after the cards are dealt
            CommandCenter(cards, shuffled, computerRaiseAmount);

            //Call the deal cards function
            DealCards(cards, shuffled);

            Console.ForegroundColor = ConsoleColor.Cyan;

            //Display the turn, the first 4 cards dealt
            Console.WriteLine("Turn: " + cards[0,0] + " " + cards[0,1] + " " + cards[0,2] + " " + cards[0,3]);

            Console.ResetColor(); 

            //Store the computer raise amount in int variable and make it equal to the computer command center function
            computerRaiseAmount = ComputerCommandCenter(cards);

            //Call the command center that gives the user options after the cards are dealt
            CommandCenter(cards, shuffled, computerRaiseAmount);

            //Call the deal cards function
            DealCards(cards, shuffled);

            Console.ForegroundColor = ConsoleColor.Cyan;

            //Display the river, all 5 cards that are dealt
            Console.WriteLine("River: " + cards[0,0] + " " + cards[0,1] + " " + cards[0,2] + " " + cards[0,3] + " " + cards[0,4]);

            Console.ResetColor(); 
            
            //Store the computer raise amount in int variable and make it equal to the computer command center function
            computerRaiseAmount = ComputerCommandCenter(cards);

            
            
            //Call the command center that gives the user options after the cards are dealt
            CommandCenter(cards, shuffled, computerRaiseAmount);

            //Call the procedure that displays the human hand
            DisplayHumanHand(cards);
            //Call the procedure that displays the computer hand
            DisplayComputerHand(cards);
            //Call the procedure that determines a winner
            DetermineAWinner(cards);

            if (computerAmount == 0)
            {
                Console.WriteLine("YOU ARE THE CHAMPION AT TEXAS HOLD'EM!");
                Reset(cards, shuffled);
            }
            else if (computerAmount == 0)
            {
                Console.WriteLine("AWE :( BETTER LUCK NEXT TIME!");
                Reset(cards, shuffled);
            }
            else
            {
                //Call the play procedure again 
                Play(cards, shuffled, pot);
            }

  
            
        }

        //Deal human card function
        static string[,] DealHumanCard(string[,] cards, string[] shuffled)
        {
            Console.WriteLine("Your hand: ");
            //Human cards equal to the shuffled cards
            cards[0,5] = shuffled[7];
            cards[0,6] = shuffled[8];
            //Return cards
            return cards;
           
        }
        
        //Deal computer cards function
        static string[,] DealComputerCard(string[,] cards, string[] shuffled)
        {
            //computer cards equal to the shuffled cards
            cards[1,5] = shuffled[5];
            cards[1,6] = shuffled[6];
            //Return cards
            return cards;
        }

        //Function to give the feild cards a value
        static string[,] DealCards(string[,] cards, string[] shuffled)
        {
            //Counting loop that counts the counter by one each time
            for (int counter = 0; counter < 5; counter++)
            {
                //Human and computer share the feild cards so they both use the same counter
                cards[0,counter] = shuffled[counter];
                cards[1, counter] = shuffled[counter];
            }
            //Return cards
            return cards;
        }


        //Function of the command center for the human player
        static void CommandCenter(string[,] cards, string[] shuffled, int computerRaiseAmount)
        {
            
            //Store the human raise amount in int variable
            int raiseAmount = 0;
            
            //Store the check value in bool variable
            bool check = false;

            //current value of computer's money is equal to the previous value subtract their raise amount
            computerAmount = computerAmount - computerRaiseAmount;
            pot = oldpot + computerRaiseAmount;
            oldpot = pot;

            //If the computer raise amount is equal to 0
            if (computerRaiseAmount == 0)
                Console.WriteLine("Computer checks");

            //otherwise 
            else
            {
                Console.WriteLine("Computer Raises: " + computerRaiseAmount.ToString("c"));
                Console.WriteLine("You must raise a minimum of: " + computerRaiseAmount.ToString("c"));
            }
            
            //While check is false, keep on repeating this program unless told otherwise
            while (check == false)
            {
                //Display human's money
                Console.WriteLine("Your money: " + humanAmount.ToString("c"));
                //Display's computer's money
                Console.WriteLine("Computer's money: " + computerAmount.ToString("c"));
                Console.WriteLine("1. Fold");
                Console.WriteLine("2. Call");
                Console.WriteLine("3. Raise");
                Console.WriteLine("4. Check");
                Console.WriteLine("5. Exit");
                Console.Write("Command: ");
                //Store command value in int variable
                int command = int.Parse(Console.ReadLine());

                
                //if command = 1 run this section
                if (command == 1)
                {
                    Console.WriteLine("Player Folds");
                    Console.WriteLine("Computer wins: " + oldpot.ToString("c"));
                    //The new computer amount equals to the old computer amount plus the old pot, reset the pot values
                    computerAmount = computerAmount + oldpot;
                    pot = 0;
                    oldpot = 0;
                    //Run play procedure
                    Play(cards, shuffled, pot);

                }
                
                //If command = 2, run this section
                else if (command == 2)
                {
                    //If the computer amount is greater than human raise amount, run this section
                    if (computerRaiseAmount > raiseAmount)
                    {
                        //human raise amount will equal to computer raise amount
                        raiseAmount = computerRaiseAmount;
                        //The new human amount will equal to the previous human amount - the new raised amount
                        humanAmount = humanAmount - raiseAmount;
                        //pot will equal to the old amount plus the the raise amount times 2 because the computer also put in that much 
                        pot = oldpot + raiseAmount;
                        //value of old pot = the newly adjusted pot value
                        oldpot = pot;
                        Console.WriteLine("Pot: " + oldpot.ToString("c"));
                        //exit the loop
                        break; 
                    }
                    //Otherwise, dont allow player to call
                    else
                    {
                        Console.WriteLine("Can't call, try again.");
                    }
                }
                //If command = 3, run this section
                else if (command == 3)
                {
                    //Determine how much the plauyer would like to raise
                    Console.Write("Raise how much? $: ");
                    raiseAmount = int.Parse(Console.ReadLine());

                    //if the raised amount is smaller than their total amount, and bigger than 0, run this section
                    if (raiseAmount <= humanAmount && raiseAmount > 0)
                    {
                        //subtract the raised amount from the human total amount
                        humanAmount = humanAmount - raiseAmount;
                        //the new pot is the old pot plus the raised amount and the old pot becomes the new pot
                        pot = oldpot + raiseAmount;
                        oldpot = pot;
                        Console.WriteLine("Pot: " + pot.ToString("c"));

                        //store the call value in a bool variable and it equals to the computercalls function
                        bool call = ComputerCalls(cards, raiseAmount);
                        //If computer decides to call the raised amount, run this section
                        if (call == true)
                        {
                            //if the computer dont have enough money to raise that much, run this section
                            if (computerAmount < raiseAmount)
                            {

                                Console.WriteLine("The computer does not have enough money.");
                                Console.WriteLine("Human Wins: " + oldpot.ToString("c"));
                                //Human wins round and the pot belongs to the human, reset the pot values
                                humanAmount = humanAmount + oldpot;
                                pot = 0;
                                oldpot = 0;
                                //Run the play procedure again to begin another round
                                Play(cards, shuffled, pot);
                            }
                            //Otherwise,
                            else
                            {
                                //Computer will call the raise amount
                                computerRaiseAmount = raiseAmount - computerRaiseAmount;
                                //Computer total amount will equal the the subrtracted value of the computer raise amount
                                computerAmount = computerAmount - computerRaiseAmount;
                                //The new pot will equal to the old pot plus computer amount and old pot will equal to the new pot
                                pot = oldpot + computerRaiseAmount;
                                oldpot = pot;
                                Console.WriteLine("Computer calls");
                                Console.WriteLine("Pot: " + pot.ToString("c"));
                                //Exit the loop
                                break;
                            }
                        }

                        //OtherWise,if computer doesn't have good enough cards
                        else
                        {
                            //Computer folds and human wins
                            Console.WriteLine("Computer Folds");
                            Console.WriteLine("Human Wins: " + oldpot.ToString("c"));
                            //Human will take the pot value and add it to their own total amount, reset pot value
                            humanAmount = humanAmount + oldpot;
                            pot = 0;
                            oldpot = 0;
                            //run the play procedure to play again 
                            Play(cards, shuffled, pot);
                        }
                    }

                    //Otherwise, don't allow human to raise and run the loop from the begining
                    else
                    {
                        Console.WriteLine("You can't do that");
                    }
                }
                //If command = 4, run this section
                else if (command == 4)
                {
                    //if the computer raises and human didn't call, dont allow them to check
                    if (computerRaiseAmount > raiseAmount)
                        Console.WriteLine("You must either fold, call or raise a greater amount");
                    
                    //Otherwise, check will equal to true
                    else
                        check = true;
                }

                //If command equals to 5, run the reset procedure
                else if (command == 5)
                {
                    Reset(cards, shuffled);
                }

                //Otherwise, display and error message
                else
                {
                    Console.WriteLine("Error");
                }
            }
        }

        //This function is for the computer to determine to raise based on their cards
        static int ComputerCommandCenter(string[,] cards)
        {
            //Computer raise amount is initally 0
            int computerRaiseAmount = 0;

            //Random number generator
            Random random = new Random();

            //store the computer hand value in int variable and make it equal to the determine computer hand value function
            //This will fine out the numerical value of the computer's hand
            int computerHandValue = DetermineComputerHandValue(cards);

            //if computer has a pair, they will raise between 5-100 dollars
            if (computerHandValue == PAIRS)
                computerRaiseAmount = random.Next(1, 100);
            //if computer has a two pair, they will raise between 60-200 dollars
            else if (computerHandValue == TWO_PAIRS)
                computerRaiseAmount = random.Next(60, 200);
            //if computer has a three of a kind, they will raise between 150-300 dollars
            else if (computerHandValue == THREE_OF_A_KIND)
                computerRaiseAmount = random.Next(150, 300);
            //if computer has a straight, they will raise between 250-600 dollars
            else if (computerHandValue == STRAIGHT)
                computerRaiseAmount = random.Next(250, 600);
            //if computer has a flush, they will raise between 400-700 dollars
            else if (computerHandValue == FLUSH)
                computerRaiseAmount = random.Next(400, 700);
            //if computer has a full house, they will raise between 600-850 dollars
            else if (computerHandValue == FULL_HOUSE)
                computerRaiseAmount = random.Next(600, 850);
            //if computer has a four of a kind, they will raise between 650-1000 dollars
            else if (computerHandValue == FOUR_OF_A_KIND)
                computerRaiseAmount = random.Next(650, 1500);
            //if computer has a straight flush, they will raise between 700-1000 dollars
            else if (computerHandValue == STRAIGHT_FLUSH)
                 computerRaiseAmount = random.Next(700, 1500);
            //if computer has a royal flush, they will raise between 900-1000 dollars
            

            //if the computer doesn't have enough for what they orginally plan to raise, go all in
            if (computerAmount < computerRaiseAmount)
                computerRaiseAmount = computerAmount;

            //Return the computer raise amount
            return computerRaiseAmount;
        }

        //Boolean function for computer to decide wether to call or fold
        static bool ComputerCalls(string[,] cards, int raiseAmount)
        {
            //store the computer hand value in int variable and make it equal to the determine computer hand value function
            int computerHandValue = DetermineComputerHandValue(cards);
            //store call value in bool variable and make it equal false
            bool call = false;

            //if the human raises an amount between 0 and 20, and the computer has something greater than nothing(1), then call
            if (raiseAmount > 0 && raiseAmount < 20 && computerHandValue >= NOTHING)
                call = true;
            //if the human raises an amount between 15 and 100, and the computer has something greater than a pair(2), then call
            else if (raiseAmount > 15 && raiseAmount < 100 && computerHandValue >= PAIRS)
                call = true;
            //if the human raises an amount between 60 and 200, and the computer has something greater than two pairs(3), then call
            else if (raiseAmount > 60 && raiseAmount < 200 && computerHandValue >= TWO_PAIRS)
                call = true;
            //if the human raises an amount between 150 and 400, and the computer has something greater than three of a kind(4), then call
            else if (raiseAmount > 150 && raiseAmount < 400 && computerHandValue >= THREE_OF_A_KIND)
                call = true;
            //if the human raises an amount between 330 and 700, and the computer has something greater than straight(5), then call
            else if (raiseAmount > 330 && raiseAmount < 700 && computerHandValue >= STRAIGHT)
                call = true;
            //if the human raises an amount between 400 and computer's money, and the computer has something greater than flush(6), then call
            else if (raiseAmount > 400 && raiseAmount < computerAmount && computerHandValue >= FLUSH)
                call = true;
            //if the human raises an amount between 600 and computer's money, and the computer has something greater than full house(7), then call
            else if (raiseAmount > 600 && raiseAmount < computerAmount && computerHandValue >= FULL_HOUSE)
                call = true;
            //if the human raises an amount between 650 and computer's money, and the computer has something greater than four of a kind(8), then call
            else if (raiseAmount > 650 && raiseAmount < computerAmount && computerHandValue >= FOUR_OF_A_KIND)
                call = true;
            //if the human raises an amount between 700 and computer's money, and the computer has something greater than straight flush(9), then call
            else if (raiseAmount > 700 && raiseAmount < computerAmount && computerHandValue >= STRAIGHT_FLUSH)
                call = true;
            
            //After examining each situation, the computer will decide if call is true or false, the return call
            return call;
        }

        //function to get the numerical card value
        static int GetCardValue(string card)
        {
            //if the card length is 3 then it must equal to 10
            if (card.Length == 3)
            {
                return 10;
            }

            //Depending on the type of card, each card is assigned to its own numberical group (A=14, K=13... 2=2)
            card = card.Substring(1, 1);
            
            if (card == "A")
            {
                return 14; 
            }
            else if (card == "K")
            {
                return 13;
            }
            else if (card == "Q")
            {
                return 12;
            }
            else if (card == "J")
            {
                return 11;
            }
            
            else if (card == "9")
            {
                return 9;
            }
            else if (card == "8")
            {
                return 8;
            }
            else if (card == "7")
            {
                return 7;
            }
            else if (card == "6")
            {
                return 6;
            }
            else if (card == "5")
            {
                return 5;
            }
            else if (card == "4")
            {
                return 4;
            }
            else if (card == "3")
            {
                return 3;
            }
            else if (card == "2")
            {
                return 2;
            }
            //Otherwise, return 0
            else
            {
                return 0;
            }
        }

        //function to get the human hand value
        static int[] GetHumanHandValue(string[,] cards)
        {
            //store the values in int array and its length equal to the cards length
            int[] values = new int[cards.GetLength(1)];

            //counting loop to count the card number
            for (int cardNumber = 0; cardNumber < cards.GetLength(1); cardNumber++)
            {
                //If the card doesn't equal nothing, find the numberical value of that card
                if (cards[0, cardNumber] != "")
                    values[cardNumber] = GetCardValue(cards[0, cardNumber]);
                
            }
            //After each card is listed as numbers, sort the values array
            Array.Sort(values);
            
            //Return the values array
            return values;
        }

        //function to get the computer hand value
        static int[] GetComputerHandValue(string[,] cards)
        {
            //store the count variable in int variable, make it equal 0 
            int count = 0;

            //counting loop that counts the card number up to the card length
            for (int cardNumber = 0; cardNumber < cards.GetLength(1); cardNumber++)
            {
                //if the number of cards doesn't equal nothing, count equals to the card number/ card length 
                if (cards[1, cardNumber] != "")
                    count = cardNumber;
                
            }

            //store values in int array and make it equal to count + 1, because the array size is always one greater since the card number starts from 0
            int[] values = new int[count + 1];

            //Counting loop that makes the card number count from 0 to the count value
            for (int cardNumber = 0; cardNumber <= count; cardNumber++)
            {
                //values of the card number equal tot he get card value function
                values[cardNumber] =  GetCardValue(cards[1, cardNumber]);
            }
            //Sort the values array
            Array.Sort(values);

            //return the sorted values array
            return values;
        }

        //function to get the suit value 
        static int GetSuitValue(string card)
        {
            //looks at the first letter using a substring to determine the suit
            card = card.Substring(0, 1);
            //Depending on the suit, label each of them with a numberical value
            //if spades, return 1
            if (card == "♠")
            {
                return 1;
            }
            //if hearts return 2
            else if (card == "♥")
            {
                return 2;
            }
            //if clubs, return 3
            else if (card == "♣")
            {
                return 3;
            }
            //Otherwise(diamonds), return 4
            else
            {
                return 4;
            }

        }
        
        //function to determine if human has a straight flush
        static int StraightFlush(string[,] cards)
        {
            //store flushhand and straight hand value in int variable and make them equal flush and straight function
            int flushHand = Flush(cards);
            int straighthand = Straight(cards);

            //if flushhand and straight hand both does not equal nothing, then return straight flush
            if (flushHand != NOTHING && straighthand != NOTHING)
            {
                return STRAIGHT_FLUSH;
            }
            //Otherwise, return nothing
            else
            {
                return NOTHING;
            }
        }

        //function that determines if human has four of a kind
        static int FourOfAKind(string[,] cards)
        {
            //store values in int array and make it equal to the human hand value
            int[] values = GetHumanHandValue(cards);

            //if the value length is less than 5, return nothing
            if (values.GetLength(0) < 5) 
                return NOTHING;

            //counting loop that counts from 0 to the value length - 3
            for (int counter = 0; counter < values.GetLength(0) - 3; counter++)
            {
                //if the values counter is equal to the value counter + 3, return four of a kind
                if (values[counter] == values[counter + 3])
                {
                    return FOUR_OF_A_KIND;
                }
            }
            //If not, return nothing
            return NOTHING;
        }

        //function that determines if human has a full house
        static int FullHouse(string[,] cards)
        {
            //store values in int array and make it equal to the human hand value
            int[] values = GetHumanHandValue(cards);
            //store three of a kind in bool 
            bool threeOfAKind = false;
            bool twoOfAKind = false;

            if (values.GetLength(0) < 5) return NOTHING;

            //find three of kind, counting loop to count from 0- values length -2 
            for (int counter = 0; counter < values.GetLength(0) - 2; counter++)
            {
                //if values equal to the value in the next 2 postions
                if (values[counter] == values[counter + 2])
                {
                    //All values set to -1
                    values[counter] = -1;
                    values[counter + 1] = -1;
                    values[counter + 2] = -1;
                    threeOfAKind = true;
                }
            }

            //find two of kind counting loop to count from 0- values -1
            for (int counter = 0; counter < values.GetLength(0) - 1; counter++)
            {
                //if values doesn't equal to -1, exclude the three of a kind
                if (values[counter] != -1)
                {
                    //if values counter is equal to the next value in the next postion, two of a kind is now true
                    if (values[counter] == values[counter + 1])
                    {
                        twoOfAKind = true;
                    }
                }
            }

            //if three of a kind and two of a kind is true then return full house
            if (threeOfAKind && twoOfAKind)
                return FULL_HOUSE;
            //Otherwise return nothing
            else
                return NOTHING;
        }

        //Function to determine if human has a flush 
        static int Flush(string[,] cards)
        {
            //store the 4 different suits in a string array and make them all equal to the cards length
            string[] hearts = new string[cards.GetLength(1)];
            string[] spades = new string[cards.GetLength(1)];
            string[] clubs = new string[cards.GetLength(1)];
            string[] diamonds = new string[cards.GetLength(1)];
            //the suits counter all initally start off as 0
            int heartsCounter = 0;
            int spadesCounter = 0;
            int clubsCounter = 0;
            int diamondsCounter = 0;

            //counting loop to count the cardsuit from 0 to the cardlength 
            for (int cardSuit = 0; cardSuit < cards.GetLength(1); cardSuit++)
            {
                //Depending on what suit the human has, add one to that suit counter each time there is a suit counter
                if (GetSuitValue(cards[0, cardSuit]) == 2)
                {
                    
                    hearts[heartsCounter] = cards[0, cardSuit];
                    heartsCounter = heartsCounter + 1;
                }
                if (GetSuitValue(cards[0, cardSuit]) == 1)
                {
                    spades[spadesCounter] = cards[0, cardSuit];
                    spadesCounter = spadesCounter + 1;
                }
                if (GetSuitValue(cards[0, cardSuit]) == 3)
                {
                    clubs[clubsCounter] = cards[0, cardSuit];
                    clubsCounter = clubsCounter + 1;
                }
                if (GetSuitValue(cards[0, cardSuit]) == 4)
                {
                    diamonds[diamondsCounter] = cards[0, cardSuit];
                    diamondsCounter = diamondsCounter + 1;
                }

            }

            //If any of the counter's are greater than 4, the return a flush
            if (heartsCounter > 4)
            {
                return FLUSH;
            }
            else if (spadesCounter > 4)
            {
                return FLUSH;
            }
            else if (clubsCounter > 4)
            {
                return FLUSH;
            }
            else if (diamondsCounter > 4)
            {
                return FLUSH;
            }
            //Otherwise, return nothing
            else
            {
                return NOTHING;
            }
        }

        //function to determine if the human has a straight
        static int Straight(string[,] cards)
        {
            //store values in int array and make it equal to the human hand value
            int[] values = GetHumanHandValue(cards);

            //if the value length is less than 5, return nothing
            if (values.GetLength(0) < 5) return NOTHING;

            int lengthOfStraight = 1;
            int[] newvalues = new int[7];

            // get rid of duplicated number from values array ...
            int newcounter = 0;
            //Counting loop that counts from 0 to values length
            for (int counter = 0; counter < values.GetLength(0); counter++)
            {
                //if counter plus one is equal to the values length, run this section
                if (counter + 1 < values.GetLength(0))
                {
                    //if values does not equal to the next postion, new values equals to old values and new counter plus 1
                    if (values[counter] != values[counter + 1])
                    {
                        newvalues[newcounter] = values[counter];
                        newcounter = newcounter + 1;
                    }
                }
                //Otherwise, newvalues = values
                else
                {
                    newvalues[newcounter] = values[counter];
                }
            }

            // count how many items with value in new values array...
            int count = 0;
            //counting loop  that counts from 0 to new values length
            for (int counter = 0; counter < newvalues.GetLength(0); counter++)
            {
                //if newvalues does not equal to 0, count + 1
                if (newvalues[counter] != 0)
                {
                    count = count + 1;
                }
            }

            // copy items with value to final value array...
            int[] finalvalues = new int[count];
            count = 0;
            //counting loop that counts from 0 to the new values length
            for (int counter = 0; counter < newvalues.GetLength(0); counter++)
            {
                //if new values doesnot = 0, final values = new values
                if (newvalues[counter] != 0)
                {
                    finalvalues[count] = newvalues[counter];
                    count = count + 1;
                }
            }

            //if the final values length is less than 5, return nothing
            if (finalvalues.GetLength(0) < 5) return NOTHING;

            // determine if straight
            int highCounter = finalvalues.GetLength(0);
            int lowCounter = finalvalues.GetLength(0) - 5;

            //while loop when low counter is greater or equal to 0
            while (lowCounter >= 0)
            {
                //Counting loop that counts from low counter to high counter
                for (int counter = lowCounter; counter < highCounter; counter++)
                {
                    //if counter plus 1 equals to the next number, run the next section
                    if (counter + 1 < finalvalues.GetLength(0))
                    {
                        //if final values plus 1 equals to the next value, add one to length of straight
                        if (finalvalues[counter] + 1 == finalvalues[counter + 1])
                        {
                            lengthOfStraight = lengthOfStraight + 1;
                        }
                        //Otherwise, exit loop
                        else
                            break;
                    }
                }

                //if length of straight is 5, return straight
                if (lengthOfStraight == 5)
                {
                    return STRAIGHT;
                }
                //Otherwise, subtract one from low and high counter and length of straight returns to one
                else
                {
                    highCounter = highCounter - 1;
                    lowCounter = lowCounter - 1;
                    lengthOfStraight = 1;
                }
            }

            //return nothing
            return NOTHING;
        }

        //function to determine if the human has a three of a kind
        static int ThreeOfAKind(string[,] cards)
        {
            //store values in int array and make it equal to the human hand value
            int[] values = GetHumanHandValue(cards);
            //Counting loop that counts from 0 to the value length - 2
            for (int counter = 0; counter < values.GetLength(0) - 2; counter++)
            {
                //if the current value equals to the value in the next 2 positions, return three of a kind
                if (values[counter] == values[counter + 2])
                {
                    return THREE_OF_A_KIND;
                }
            }
            //Otherwise, return nothing
            return NOTHING;
        }

        //function to determine if the human has a two pair or not 
        static int TwoPairs(string[,] cards)
        {
            //store values in int array and make it equal to the human hand value
            int[] values = GetHumanHandValue(cards);
            //store the first pair value in bool and make it equal false
            bool firstPair = false;
            //store the second pair value in bool and make it equal false
            bool secondPair = false;

            //Counting loop that counts from 0 to the value length - 1
            for (int counter = 0; counter < values.GetLength(0) - 1; counter++)
            {
                //if the current value equals to the value in the next position
                if (values[counter] == values[counter + 1])
                {
                    //if the first pair is false, then it will now equal true
                    if (firstPair == false)
                    {
                        firstPair = true;
                    }
                    //Otherwise, the second pair equals true and exit the loop
                    else
                    {
                        secondPair = true;
                        break;
                    }
                }
            }

            //if the first and second pair equals true, return two pairs
            if (firstPair == true && secondPair == true)
                return TWO_PAIRS;
            //otherwise, return nothing
            else
                return NOTHING;
        }

        //function to determine if the human has a pair or not 
        static int Pairs(string[,] cards)
        {
            //store values in int array and make it equal to the human hand value
            int[] values = GetHumanHandValue(cards);
            //Counting loop that counts from 0 to the value length - 1
            for (int counter = 0; counter < values.GetLength(0) - 1; counter++)
            {
                //if the current value equals to the value in the next position, return pairs
                if (values[counter] == values[counter + 1])
                {
                    return PAIRS;
                }
            }
            //otherwise, return nothing
            return NOTHING;
        }

        //function to determine if the human has a high card or not
        static int HighCard(string[,] cards)
        {
            //return nothing due because the human will definately have a high card
            return NOTHING;
        }
       
        

        

        //function to determine if computer has a straight flush
        static int ComputerStraightFlush(string[,] cards)
        {
            //store flushhand and straight hand value in int variable and make them equal computer flush and straight function
            int flushHand = ComputerFlush(cards);
            int straighthand = ComputerStraight(cards);

            //if flushhand and straight hand both does not equal nothing, then return straight flush
            if (flushHand != NOTHING && straighthand != NOTHING)
            {
                return STRAIGHT_FLUSH;
            }
            //Otherwise, return nothing
            else
            {
                return NOTHING;
            }
        }

        //function that determines if computer has four of a kind
        static int ComputerFourOfAKind(string[,] cards)
        {
            //store values in int array and make it equal to the computer hand value
            int[] values = GetComputerHandValue(cards);

            //if the value length is less than 5, return nothing
            if (values.GetLength(0) < 5) return NOTHING;

            //counting loop that counts from 0 to the value length - 3
            for (int counter = 0; counter < values.GetLength(0) - 3; counter++)
            {
                //if the values counter is equal to the value counter + 3, return four of a kind
                if (values[counter] == values[counter + 3])
                {
                    return FOUR_OF_A_KIND;
                }
            }
            //If not, return nothing
            return NOTHING;
        }
        static int ComputerFullHouse(string[,] cards)
        {
            //store values in int array and make it equal to the computer hand value
            int[] values = GetComputerHandValue(cards);
            //store three of a kind in bool 
            bool threeOfAKind = false;
            bool twoOfAKind = false;

            if (values.GetLength(0) < 5) return NOTHING;

            //find three of kind, counting loop to count from 0- values length -2 
            for (int counter = 0; counter < values.GetLength(0) - 2; counter++)
            {
                //if values equal to the value in the next 2 postions
                if (values[counter] == values[counter + 2])
                {
                    //All values set to -1
                    values[counter] = -1;
                    values[counter + 1] = -1;
                    values[counter + 2] = -1;
                    threeOfAKind = true;
                }
            }

            //find two of kind counting loop to count from 0- values -1
            for (int counter = 0; counter < values.GetLength(0) - 1; counter++)
            {
                //if values doesn't equal to -1, exclude the three of a kind
                if (values[counter] != -1)
                {
                    //if values counter is equal to the next value in the next postion, two of a kind is now true
                    if (values[counter] == values[counter + 1])
                    {
                        twoOfAKind = true;
                    }
                }
            }

            //if three of a kind and two of a kind is true then return full house
            if (threeOfAKind && twoOfAKind)
                return FULL_HOUSE;
            //Otherwise return nothing
            else
                return NOTHING;
        }

        //Function to determine if computer has a flush
        static int ComputerFlush(string[,] cards)
        {
            //store the 4 different suits in a string array and make them all equal to the cards length
            string[] hearts = new string[cards.GetLength(1)];
            string[] spades = new string[cards.GetLength(1)];
            string[] clubs = new string[cards.GetLength(1)];
            string[] diamonds = new string[cards.GetLength(1)];
            //the suits counter all initally start off as 0
            int heartsCounter = 0;
            int spadesCounter = 0;
            int clubsCounter = 0;
            int diamondsCounter = 0;


            //counting loop to count the cardsuit from 0 to the cardlength
            for (int cardSuit = 0; cardSuit < cards.GetLength(1); cardSuit++)
            {
                //Depending on what suit the human has, add one to that suit counter each time there is a suit counter
                if (GetSuitValue(cards[1, cardSuit]) == 2)
                {
                    hearts[heartsCounter] = cards[1, cardSuit];
                    heartsCounter = heartsCounter + 1;
                }
                if (GetSuitValue(cards[1, cardSuit]) == 1)
                {
                    spades[spadesCounter] = cards[1, cardSuit];
                    spadesCounter = spadesCounter + 1;
                }
                if (GetSuitValue(cards[1, cardSuit]) == 3)
                {
                    clubs[clubsCounter] = cards[1, cardSuit];
                    clubsCounter = clubsCounter + 1;
                }
                if (GetSuitValue(cards[1, cardSuit]) == 4)
                {
                    diamonds[diamondsCounter] = cards[1, cardSuit];
                    diamondsCounter = diamondsCounter + 1;
                }

            }

            //If any of the counter's are greater than 4, the return a flush
            if (heartsCounter > 4)
            {
                return FLUSH;
            }
            else if (spadesCounter > 4)
            {
                return FLUSH;
            }
            else if (clubsCounter > 4)
            {
                return FLUSH;
            }
            else if (diamondsCounter > 4)
            {
                return FLUSH;
            }
            //Otherwise, retrun nothng
            else
            {
                return NOTHING;
            }
        }

        //function to determine if the computer has a straight
        static int ComputerStraight(string[,] cards)
        {
            //store values in int array and make it equal to the computer hand value
            int[] values = GetComputerHandValue(cards);

            //if the value length is less than 5, return nothing
            if (values.GetLength(0) < 5) return NOTHING;

            int lengthOfStraight = 1;
            int[] newvalues = new int[7];
            
            // get rid of duplicated number from values array ...
            int newcounter = 0;
            //Counting loop that counts from 0 to values length
            for (int counter = 0; counter < values.GetLength(0); counter++)
            {
                //if counter plus one is equal to the values length, run this section
                if (counter + 1 < values.GetLength(0))
                {
                    //if values does not equal to the next postion, new values equals to old values and new counter plus 1
                    if (values[counter] != values[counter + 1])
                    {
                        newvalues[newcounter] = values[counter];
                        newcounter = newcounter + 1;
                    }
                }
                //Otherwise, newvalues = values
                else
                {
                    newvalues[newcounter] = values[counter];
                }
            }

            // count how many items with value in new values array...
            int count = 0;
            //counting loop  that counts from 0 to new values length
            for (int counter = 0; counter < newvalues.GetLength(0); counter++)
            {
                //if newvalues does not equal to 0, count + 1
                if (newvalues[counter] != 0)
                {
                    count = count + 1;
                }
            }

            // copy items with value to final value array...
            int[] finalvalues = new int[count];
            count = 0;
            //counting loop that counts from 0 to the new values length
            for (int counter = 0; counter < newvalues.GetLength(0); counter++)
            {
                //if new values doesnot = 0, final values = new values
                if (newvalues[counter] != 0)
                {
                    finalvalues[count] = newvalues[counter];
                    count = count + 1;
                }
            }

            //if the final values length is less than 5, return nothing
            if (finalvalues.GetLength(0) < 5) return NOTHING;

            // determine if straight
            int highCounter = finalvalues.GetLength(0);
            int lowCounter = finalvalues.GetLength(0) - 5;

            //while loop when low counter is greater or equal to 0
            while (lowCounter >= 0)
            {
                //Counting loop that counts from low counter to high counter
                for (int counter = lowCounter; counter < highCounter; counter++)
                {
                    //if counter plus 1 equals to the next number, run the next section
                    if (counter + 1 < finalvalues.GetLength(0))
                    {
                        //if final values plus 1 equals to the next value, add one to length of straight
                        if (finalvalues[counter] + 1 == finalvalues[counter + 1])
                        {                            
                            lengthOfStraight = lengthOfStraight + 1;
                        }
                        //Otherwise, exit loop
                        else
                            break;
                    }
                }

                //if length of straight is 5, return straight
                if (lengthOfStraight == 5)
                {
                    return STRAIGHT;
                }
                //Otherwise, subtract one from low and high counter and length of straight returns to one
                else
                {
                    highCounter = highCounter - 1;
                    lowCounter = lowCounter - 1;
                    lengthOfStraight = 1;
                }
            }

            //return nothing
            return NOTHING;
        }


        //function to determine if the computer has a three of a kind
        static int ComputerThreeOfAKind(string[,] cards)
        {
            //store values in int array and make it equal to the computer hand value
            int[] values = GetComputerHandValue(cards);
            //Counting loop that counts from 0 to the value length - 2
            for (int counter = 0; counter < values.GetLength(0) - 2; counter++)
            {
                //if the current value equals to the value in the next 2 positions, return three of a kind
                if (values[counter] == values[counter + 2])
                {
                    return THREE_OF_A_KIND;
                }
            }
            //Otherwise, return nothing
            return NOTHING;
        }

        //function to determine if the computer has a two pair or not 
        static int ComputerTwoPairs(string[,] cards)
        {
            //store values in int array and make it equal to the computer hand value
            int[] values = GetComputerHandValue(cards);
            //store the first pair value in bool and make it equal false
            bool firstPair = false;
            //store the second pair value in bool and make it equal false
            bool secondPair = false;

            //Counting loop that counts from 0 to the value length - 1
            for (int counter = 0; counter < values.GetLength(0) - 1; counter++)
            {
                //if the current value equals to the value in the next position
                if (values[counter] == values[counter + 1])
                {
                    //if the first pair is false, then it will now equal true
                    if (firstPair == false)
                    {
                        firstPair = true;
                    }
                    //Otherwise, the second pair equals true and exit the loop
                    else
                    {
                        secondPair = true;
                        break;
                    }
                }
            }

            //if the first and second pair equals true, return two pairs
            if (firstPair == true && secondPair == true)
                return TWO_PAIRS;
            //otherwise, return nothing
            else
                return NOTHING;
        }

        //function to determine if the computer has a pair or not 
        static int ComputerPairs(string[,] cards)
        {
            //store values in int array and make it equal to the computer hand value
            int[] values = GetComputerHandValue(cards);
            //Counting loop that counts from 0 to the value length - 1
            for (int counter = 0; counter < values.GetLength(0) - 1; counter++)
            {
                //if the current value equals to the value in the next position, return pairs
                if (values[counter] == values[counter + 1])
                {
                    return PAIRS;
                }
            }
            //otherwise, return nothing
            return NOTHING;
        }

        //function to determine if the computer has a high card or not
        static int ComputerHighCard(string[,] cards)
        {
            //return nothing due because the computer will definately have a high card
            return NOTHING;
        }

        
        //Function that determines the human's hand value
        static int DetermineHumanHandValue(string[,] cards)
        {
            //If the straight flush function equals to straight flush 
            if (StraightFlush(cards) == STRAIGHT_FLUSH)
            {
                //retrun the numerical value of a straight flush
                return STRAIGHT_FLUSH;
            }
            //If the four of a kind function equals to four of a kind
            else if (FourOfAKind(cards) == FOUR_OF_A_KIND)
            {
                //return the numerical value of four of a kind
                return FOUR_OF_A_KIND;
            }
            //If the full house function equals to full house
            else if (FullHouse(cards) == FULL_HOUSE)
            {
                //return the numerical value of full house
                return FULL_HOUSE;
            }
            //If the flush function equals to flush
            else if (Flush(cards) == FLUSH)
            {
                //return the numerical value of flush
                return FLUSH;
            }
            //If the straight function equals to straight
            else if (Straight(cards) == STRAIGHT)
            {
                //return the numerical value of straight
                return STRAIGHT;
            }
            //If the three of a kind function equals to three of a kind
            else if (ThreeOfAKind(cards) == THREE_OF_A_KIND)
            {
                //return the numerical value of three of a kind
                return THREE_OF_A_KIND;
            }
            //If the two pairs function equals to two pairs
            else if (TwoPairs(cards) == TWO_PAIRS)
            {
                //return the numerical value of two pairs
                return TWO_PAIRS;
            }
            //If the pairs function equals to pairs
            else if (Pairs(cards) == PAIRS)
            {
                //return the numerical value of pairs
                return PAIRS;
            }
            //Otherwise
            else 
            {
                //return the value of nothing
                return NOTHING;
            }
        }

        //Function to determine computer hand value
        static int DetermineComputerHandValue(string[,] cards)
        {
            //If the Computer straight flush function equals to straight flush 
            if (ComputerStraightFlush(cards) == STRAIGHT_FLUSH)
            {
                //retrun the numerical value of a straight flush
                return STRAIGHT_FLUSH;
            }
            //If the Computer four of a kind function equals to four of a kind
            else if (ComputerFourOfAKind(cards) == FOUR_OF_A_KIND)
            {
                //return the numerical value of four of a kind
                return FOUR_OF_A_KIND;
            }
            //If the Computer full house function equals to full house
            else if (ComputerFullHouse(cards) == FULL_HOUSE)
            {
                //return the numerical value of full house
                return FULL_HOUSE;
            }
            //If the Computer flush function equals to flush
            else if (ComputerFlush(cards) == FLUSH)
            {
                //return the numerical value of flush
                return FLUSH;
            }
            //If the Computer straight function equals to straight
            else if (ComputerStraight(cards) == STRAIGHT)
            {
                //return the numerical value of straight
                return STRAIGHT;
            }
            //If the computer three of a kind function equals to three of a kind
            else if (ComputerThreeOfAKind(cards) == THREE_OF_A_KIND)
            {
                //return the numerical value of three of a kind
                return THREE_OF_A_KIND;
            }
            //If the computer two pair function equals to two pairs
            else if (ComputerTwoPairs(cards) == TWO_PAIRS)
            {
                //return the numerical value of two pairs
                return TWO_PAIRS;
            }
            //If the Computer pair function equals to pairs
            else if (ComputerPairs(cards) == PAIRS)
            {
                //return the numerical value of pairs
                return PAIRS;
            }
            //Otherwise
            else
            {
                //return the value of nothing
                return NOTHING;
            }
        }

        //Display the human hand function
        static void DisplayHumanHand(string[,] cards)
        {
            //if the determine human hand value returns a straight flush
            if (DetermineHumanHandValue(cards) == STRAIGHT_FLUSH)
            {
                Console.WriteLine("Human: Straight flush");
            }
            //if the determine human hand value returns a four of a kind
            else if (DetermineHumanHandValue(cards) == FOUR_OF_A_KIND)
            {
                Console.WriteLine("Human: Four of a kind");
            }
            //if the determine human hand value returns a full house
            else if (DetermineHumanHandValue(cards) == FULL_HOUSE)
            {
                Console.WriteLine("Human: Full house");
            }
            //if the determine human hand value returns a  flush
            else if (DetermineHumanHandValue(cards) == FLUSH)
            {
                Console.WriteLine("Human: Flush");
            }
            //if the determine human hand value returns a straight 
            else if (DetermineHumanHandValue(cards) == STRAIGHT)
            {
                Console.WriteLine("Human: Straight");
            }
            //if the determine human hand value returns a three of a kind
            else if (DetermineHumanHandValue(cards) == THREE_OF_A_KIND)
            {
                Console.WriteLine("Human: Three of a Kind");
            }
            //if the determine human hand value returns a two pairs
            else if (DetermineHumanHandValue(cards) == TWO_PAIRS)
            {
                Console.WriteLine("Human: Two Pairs");
            }
            //if the determine human hand value returns a pair
            else if (DetermineHumanHandValue(cards) == PAIRS)
            {
                Console.WriteLine("Human: Pairs ");
            }
            //if the determine human hand value returns a nothing
            else
            {
                Console.WriteLine("Human: High Card ");
            }

        }

        static void DisplayComputerHand(string[,] cards)
        {
            //if the determine computer hand value returns a straight flush
            if (DetermineComputerHandValue(cards) == STRAIGHT_FLUSH)
            {
                Console.WriteLine("Computer: Straight flush");
            }
            //if the determine computer hand value returns a four of a kind
            else if (DetermineComputerHandValue(cards) == FOUR_OF_A_KIND)
            {
                Console.WriteLine("Computer: Four of a kind");
            }
            //if the determine computer hand value returns a full house 
            else if (DetermineComputerHandValue(cards) == FULL_HOUSE)
            {
                Console.WriteLine("Computer: Full house");
            }
            //if the determine computer hand value returns a flush
            else if (DetermineComputerHandValue(cards) == FLUSH)
            {
                Console.WriteLine("Computer: Flush");
            }
            //if the determine computer hand value returns a straight
            else if (DetermineComputerHandValue(cards) == STRAIGHT)
            {
                Console.WriteLine("Computer: Straight");
            }
            //if the determine computer hand value returns a three of a kind
            else if (DetermineComputerHandValue(cards) == THREE_OF_A_KIND)
            {
                Console.WriteLine("Computer: Three of a Kind");
            }
            //if the determine computer hand value returns a two pairs
            else if (DetermineComputerHandValue(cards) == TWO_PAIRS)
            {
                Console.WriteLine("Computer: Two Pairs");
            }
            //if the determine computer hand value returns a pair
            else if (DetermineComputerHandValue(cards) == PAIRS)
            {
                Console.WriteLine("Computer: Pairs ");
            }
            //if the determine computer hand value returns nothing
            else
            {
                Console.WriteLine("Computer: High Card ");
            }
        }

        //Procedure to determine a winner
        static void DetermineAWinner(string[,] cards)
        {
            //if the determine human value is greater than the determine computer value 
            if (DetermineHumanHandValue(cards) > DetermineComputerHandValue(cards))
            {
                //human wins and adds the pot value to their own 
                Console.WriteLine("Human Wins: " + oldpot.ToString("c"));
                humanAmount = humanAmount + oldpot;
                //Reset the pot value to 0
                oldpot = 0;
            }
            //if the determine computer value is greater than the determine human value 
            else if (DetermineComputerHandValue(cards) > DetermineHumanHandValue(cards))
            {
                //computer wins and adds the pot value to their own
                Console.WriteLine("Computer Wins: " + oldpot.ToString("c"));
                computerAmount = computerAmount + oldpot;
                //Reset the pot value to 0
                oldpot = 0;
            }
            //If the determine computer hand value is equal to determine human hand value
            else if (DetermineHumanHandValue(cards) == DetermineComputerHandValue(cards))
            {
                //Tie game and both player's split pot evenly
                Console.WriteLine("Tie Game, split pot");
                computerAmount = computerAmount + oldpot/2;
                humanAmount = humanAmount + oldpot/2;
                //reset pot back to 0
                oldpot = 0;
            }
        }

        //Display credits procedure
        static void Credits(string[,] cards, string[] shuffled)
        {
            Console.WriteLine("");
            Console.WriteLine("Created by Kevin Sun");
            //Reset back to main menu
            Reset(cards, shuffled);
        }

        //Help Menu that explains the rules
        static void Help(string[,] cards, string[] shuffled)
        {
            Console.WriteLine("List of Poker Hands");
            Console.WriteLine("===================");
            
            Console.WriteLine("1. Striaght flush (♦4,♦5,♦6,♦7,♦8)");
            Console.WriteLine("2. Four of a kind (♥6,♦6,♣6,♠6)");
            Console.WriteLine("3. Full house (♥7,♦7,♣7,♣9,♠9)");
            Console.WriteLine("4. Flush (♥A,♥5,♥Q,♥J,♥7)");
            Console.WriteLine("5. Straight (♦7,♣8,♦9,♥10,♠J)");
            Console.WriteLine("6. Three of a kind (♣5,♠5,♥5)");
            Console.WriteLine("7. Two pairs (♣9,♦9,♦K,♠K)");
            Console.WriteLine("8. one pair (♠J,♥J)");


            //Calls the reset procedure
            Reset(cards, shuffled);
        }

        //Reset procedure
        static void Reset(string[,] cards, string[] shuffled)
        {
            Console.WriteLine("");
            Console.Write("Press 1 to reset: ");
            
            //Store command variable in int variable
            int command = int.Parse(Console.ReadLine());
            Console.WriteLine("");
            //if command is equal to 1, call menu procedure
            if (command == 1)
            {
                //call menu
                Menu(cards, shuffled);
            }
            //Otherwise, display Error
            else
            {
                Console.WriteLine("Error");
            }
        }

    }

}
