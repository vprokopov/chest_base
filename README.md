# chest_base

The basic part for chess. 

From the functionality:
- the ability to walk on any squares
- Differentiation into pawns and special pieces
- move change 
- calculation of pieces knocked down
- round counting

If you have any questions, you can message me on Telegram - @vlprku

# Insert a function for creating the checkerboard and pawn designations
def p(fig) :
    return '  '+fig+'  '  
WhiteF = ['♖' , '♗', '♘', '♕', '♔','♘','♗','♖' ]
BlackF = ['♜' , '♝', '♞', '♚', '♛','♞','♝','♜' ]
WhiteF = list('LSHFKHSL')
BlackF = list('LSHKFHSL')
BLK, WHT = '○●'

# values that helps us to make turns
values = {  '1':0,
             '2':1,
             '3':2,
             '4':3,
             '5':4,
             '6':5,
             '7':6,
             '8':7,
             'A':0,
             'B':1,
             'C':2,
             'D':3,
             'E':4,
             'F':5,
             'G':6,
             'H':7
            


    }

# make a field with matrix
EMPTY = '  '
Desk  =  [

        
           
             
            [ BLK+fig  for fig in BlackF   ],         # special figures (such as ♖, ♗, ♘)
            [ BLK+'P' for counter in range(8)   ],     # pawns

            
            [EMPTY for counter in range(8)  ], #empty fields
            [EMPTY for counter in range(8) ],
            [EMPTY for counter in range(8) ],
            [EMPTY for counter in range(8) ],

            
            [ WHT+'P' for counter in range(8)  ], # pawns
            [  WHT+fig  for fig in WhiteF     ], # special figures (such as ♖, ♗, ♘)
             


            
           
        ]


deads = [] #for counting stacked figures

def show():
    print(deads)
    print( '\t     ', '═' * 55,sep='') # decoration
    print('\t   | ' , '   |  '.join('ABCDEFGH')+ '    |') #letter raw
    print()
    for y in range(8):
        #print( '\t      ', '═' *44,'║',sep='')
        #print('\t>     ', y+1 , '║  ', ' ║ '.join(Desk[y]) ,'  ║', y+1, '',sep ='')
        print('\t '+  str(y+1) + ' |'+ '|'.join(map(p,Desk[y])), '| ' +  str(y+1)) #creat field and borders

    print() 
    print('\t   | ' , '   |  '.join('ABCDEFGH')+ '    |') # down letter field
    print( '\t     ', '═' * 55,sep='') 
move = 0 # for counting moves
raund = 1 # for counting rounds
deads = []

act = WHT 
while True:
    print('Round number',1 + raund // 2)
    print('Move number',move+1)
    print('The move is <'+act+'>')
    show()
    
    move+=1

    while True:
         
        x,y = input('Enter the chip (e.g.: e1,h7) you want to walk with:').strip().upper()[0:2]
        y = values[y] #the first move input
        x = values[x] #the second move input
        who = Desk[y][x] 
        if who[0]!=act: #if the square entered is not equal to the move of the person who is moving, an error is displayed
            print(who,  ', it is not your move',act)
            continue
        Desk[y][x] = '  '

        
        if True:
            break


    x,y =   input('Where to go? ').strip().upper()[0:2] #choosing where to go, only two values are taken from the input
    y,x = values[y], values[x]

    
    trg = Desk[y][x] 
    Desk[y][x] = who

    # change moves
    act = WHT if act==BLK else BLK 
    # the act becomes white if it was black before, and if it was white it becomes black
