# DiceCodePy
import random
def rollDie():
    '''Return a random number 1-6
    '''
    return (random.randint(1,6))
    
def firstRoll():
    ''' Return a list of 14 numbers, each number
    selected at random from 1 to 6.
    '''
    group = []   #initalized aggrigator
    for number in range(14):    #create counted loop 
        group.append(rollDie())          #aggregated to the open list
    return group              #return the aggrigator     


def countFreq(dice, number):   #Accumulator pattern
    freq = 0                      #Initalize accumulator pattern
    for die in dice:
        if die == number:
            freq = freq + 1
    return freq
        
def findMode(dice):
    ''' Accepts a list of numbers 1-6.
    Returns the most common number in the list.
    Returns one of the most common if there is a tie.
    '''
    
    record = 0
    for number in [1, 2, 3, 4, 5, 6]:
        if countFreq(dice, number) > record:
            record = countFreq(dice, number)   #Set the new record
            mode = number
            ''' will return the number run, the amount of that number,
            and the mode after cycling that number.
            ''' 
    return mode   # Return the number of which has the most
    
def listUnmatchedDice(dice, target):
    '''Accepts dice :: a list of numbers
    target:: a number
    Return the indices where the element != target
    '''
    unmatchedList = []
    for index in range(14):
        if dice[index] != target:
            unmatchedList.append(index)
    return unmatchedList 
    
    
def rerollOne(dice, index):
    '''dice is a list of 14 numbers
    index is an int 0-13
    Return the list of dice, with a number randomly chosen 
    rom 1 to 6 to replace the item at index
    ''' 
    dice[index] = rollDie()
    return dice
    
def rerollMany(dice):
    '''Accept a list containg 14 values all of all of which are equal to
    a random int from [1, 2, 3, 4, 5, 6].
    The result wil be a new list in which all of the values at
    indices that were not equal to the "mode" have been rerolled
    '''
    mode = findMode(dice)
    multiRoll = listUnmatchedDice(dice, mode)
    for index in multiRoll:
        dice = rerollOne(dice, index)   
    return dice
        
def won(dice):
    '''dice is a list of 14 ints 1-6
    checks for 14 of a kind 
    returns True or False
    '''
    return dice == [dice[0]]*14  
    
def game(debug=False):
    dice = firstRoll()
    counter = 1
    while not won(dice):
        counter += 1
        print dice
        
        rerollMany(dice)
        if debug:
            '''print dice
            '''
    return counter
