import random
suits = ('Hearts', 'Diamonds', 'Spades', 'Clubs')
ranks = ('Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine', 'Ten', 'Jack', 'Queen', 'King', 'Ace')
values = {'Two':2, 'Three':3, 'Four':4, 'Five':5, 'Six':6, 'Seven':7, 'Eight':8, 'Nine':9, 'Ten':10, 'Jack':10,'Queen':10, 'King':10, 'Ace':11}

playing = True

class Card:
    
    def __init__(self, suit, rank):
        self.suit = suit
        self.rank = rank
    
    def __str__(self):
        return "{} of {}".format(self.rank,self.suit)

class Deck:
    
    def __init__(self):
        self.deck = []  # empty list for deck to be created in 
        for suit in suits:
            for rank in ranks:
                self.deck.append(Card(suit,rank)) # append created objects to list
    
    def __str__(self):
        deck_comp = '' # empty list for remaining of deck
        for card in self.deck:
            deck_comp += '\n' + card.__str__() # card.__str__(makes cards when code is ran) 
        return "The deck has: {}".format(deck_comp)

    def shuffle(self): # shuffle method 
        random.shuffle(self.deck)
        
    def deal(self): # takes single card from deck list
        single_card = self.deck.pop() 
        return single_card

class Hand:
    
    def __init__(self):
        self.cards = []
        self.value = 0
        self.aces = 0
        
    def add_card(self,card):
        self.cards.append(card)
        self.value += values[card.rank] # add num to self.value
        if card.rank == 'Ace': # if name of rank == "Ace"
            self.aces += 1  # add num to self.aces  
            
    def adjust_for_ace(self): # SHOULD ask if you want to play as 1 or 11
        while self.value > 21 and self.aces:
            self.vaule -= 10 # reduces value of hand by 10
            self.aces -= 1 # refreshes num of aces as if 2xaces then 1st=1,2nd=11
            
class Chips:
    
    def __init__(self):
        self.total = input("Please enter pocket amount: ") #100# This can be set to a default value or supplied by a user input
        self.bet = 0
        
    def win_bet(self):
        self.total += self.bet # adds bet onto total once won
    
    def lose_bet(self):
        self.total -= self.bet # takes bet amoutn from total

def take_bet(chips): # calls class chips and methods attached 
    while True:
        try:
            chips.bet = int(input('Please enter betting amount for this round: ')) # Ask for INT() input 
        except:
            print("Sorry but you need to enter a number as an intiger")
            continue # keeps looping untill correct input
        else:
            if chips.bet > chips.total: # if bet is greater than total in pot
                print("Sorry but your total is {}, please try again".format(chips.total))
            else:
                break 
                
def hit(deck,hand):
    hand.add_card(deck.deal()) # HIT = .add_card to Hand()
    hand.adjust_for_ace() # when hit use adjust_for_aces to check/alter for aces

def hit_or_stand(deck,hand):
    global playing  # to control an upcoming while loop
    
    while True:
        x = input("Please Choose to 'Hit' or 'Stand': ") # ask player to play 
        
        if x[0].lower() == 'h': # if [0] from input == h = hit = add card to hand 
            hit(deck,hand)
        
        elif x[0].lower() == 's': # if [0] from input == s = stand = change turn 
            print("Player stands, Computer's turn")
            playing = False # player playering loop to stop
            
        else:
            print("Sorry please try again")
            continue
        break

def show_some(player,dealer):
    print("\nDealer's Hand: ")
    print(" <Hidden Card> ")
    print("",dealer.cards[1])
    print("\nPlayer's Hand: ", *player.cards, sep='\n ')
    
def show_all(player,dealer):
    print("\nDealer's Hand:", *dealer.cards, sep='\n ')
    print("Dealer's Hand =",dealer.value)
    print("\nPlayer's Hand:", *player.cards, sep='\n ')
    print("Player's Hand =", player.value)
    
def player_busts(player, dealer, chips):
    print("Oops your Hand is Bust")
    chips.lose_bet()

def player_wins(player,dealer,chips):
    print("Congratulations you've wone")
    chips.win_bet()

def dealer_busts(player,dealer,chips):
    print("Dealer's Hand is Bust")
    chips.win_bet()
    
def dealer_wins(player,dealer,chips):
    print("Computer won, you lost")
    chips.lose_bet()
    
def push(player,dealer):
    print("Funny it's a Draw")

while True:
    # Print an opening statement
    print("Hello and welcome to this game of Black Jack. \nYou know the rules, lets get playing!\nFYI the computer will Stand on 17 or greater")
    
    # Create & shuffle the deck, deal two cards to each player
    deck = Deck()
    deck.shuffle()
    
    player_hand = Hand() # calling HAND() class to player_hand
    player_hand.add_card(deck.deal()) # class HAND(method add_card) / class Deck(method deal)
    player_hand.add_card(deck.deal()) # 2 cards required for game play
    
    dealer_hand = Hand() # computer hand set as veriable using HAND class
    dealer_hand.add_card(deck.deal())
    dealer_hand.add_card(deck.deal())
    
    # Set up the Player's chips
    player_chips = Chips() # will ask user for amount in bank
    
    # Prompt the Player for their bet
    take_bet(player_chips) # class TAKE_BET ask for bet amount 
    
    # Show cards (but keep one dealer card hidden)
    show_some(player_hand,dealer_hand) # (show_some) function passing through player_habd and dealer_hand
    
    while playing:  # recall this variable from our hit_or_stand function
        
        # Prompt for Player to Hit or Stand
        hit_or_stand(deck, player_hand)
        
        # Show cards (but keep one dealer card hidden)
        show_some(player_hand,dealer_hand)
        
        # If player's hand exceeds 21, run player_busts() and break out of loop
        if player_hand.value > 21:
            player_busts(player_hand,dealer_hand,player_chips)
            break

    # If Player hasn't busted, play Dealer's hand until Dealer reaches 17
    if player_hand.value < 21:
        
        while dealer_hand < 17:
            hit(deck,dealer_hand)
    
        # Show all cards
        show_all(player_hand,dealer_hand)
        
        # Run different winning scenarios
        if dealer_hand.value > 21:
            dealer_wins(player_hand, dealer_hand, player_chips)
        
        elif dealer_hand.value > player_hand.value:
            dealer_wins(player_hand,dealer_hand,player_chips)
        
        elif dealer_hand.value < player_hand.value:
            player_wins(dealer_hand, player_hand, player_chips)
        
        else:
            push(player_hand, dealer_hand)
        
    # Inform Player of their chips total 
    print("\nPlayer's winnings are ",player_chips.total)
    
    # Ask to play again
    new_game = inupt("Would you like to play again? yes or no?: ")
    if new_game[0].lower() == 'y':
        playing = True
        continue
    else:
        print("Thanks for playing")
        break



