# 27 May 2023

  - Javascript Nodejs
  
      - testing dependencies
      - mock functions
      - testing functions but with valid export reason of that function (good guideline)
      - wc a terminal command to implement using node js
      
  - Swamiji session
  
      - building io, calc, repl
      - testing for io and calc and repl
      - insight and discussion about good practices of unit test [microsoft](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)
      - to recollect ideas and discuss with others
      - also to look back into github commits to understand the evolution of code 
      - code snippets refer
        - [sauma](https://saumasaha.github.io/todayilearned/)     
  
  - Jayant session
        
      - introduction to markdown
      - some basic formatting and adding links, inlinks and images
      - creating table and alignment
      - to host our own github pages

-----

# 30 May 2023

  - Presentation till now
    - BP => Geetanjali & Gayatri 
    - Azhar, Sneha, Prafulla and Sapna
    - National Grid => Aashrita
    - NPCI => Rishav 
    - UBS => 
      - Infra Consultant => Prafulla, 
      - Team Nemo => Chhavi
      - Team Shark => Annakamma
    - Seek => 
      - Team Sumo => Suresh
    - Metro => Prajakta
    - Atlassian => Lakshmi and Subhash
    - E4R => 
      - YASKA => Nitin 
      - DIC => Manikanta

## Some common keywords used in projects (will soon include their meaning)
- POC - Proof Of Concept
- Hotfix
- QA
- KT - Knowledge Transfer. People share their coding knowledge to others
- Starters - Giving detail about what have been done till now
- Retros - Doing reflection session with team members to find out progress and issues
- Interfencing Pipeline 

-------

# 3 June 2023

- Presentations (2)
  - McKindsey => Ritika(3 months)
  - Mercedes => Tanmay, Swapnil, Vivek, Nilam
  
## Takeaways
- Billable - when client pays to company for some recognizable work which is professional.
- Not everyone becomes billable 
- You may have to present a feature to client and your team members too.
- Seek for other opportunity to increase your learnings
- There may be delay in access, but in the meantime try to get context of the project you're working on. It will boost the work progress later and won't take too much time.
- People may delay in response, so have patience.
- Always avoid code push in hurry
- Not all meetings are necessary to attend, so get info about the necessary meetings that are necessary.

-----------

# 5 June 2023

- Ashish Session
  - we learnt about event
  - we saw the usage of createReadStream, how we can use in file
  - also covered eventEmitter
    - eventEmitter.on
    - eventEmitter.emit
- Seniors showed their games that they build before entering into projects
  - Scotland Yard
  - Cashflow
  - Cluedo
  - Acquire

- Common challanges and takeaways
  - Collaboration with others
  - there will be sprint of three days, showcase to show your demo and progress
  - it will be a highly competitive and intensive learning process
  - there will be QA, BA, Developer roles switching, in order to get the experience

------------

# 6 June 2023

- Presentation 
  - tdm => Sakshi
    - Domain is related to maintaining stock market data
  - Axis => Abin, Sampriti, Sanjana, Prem
    - Domain related to banking website and introducing new loan
    - they also had to maintain the RBI guideline and complete requirement within time
  - Takeaway
    - maintain work life balance
    - make friends, it will help to cover task easily and it smooth
    - take ownership and responsibily of your work
    - be ready to adapt in new changes
- Swamiji games show
  - one was about insects moivng around in screen
  - pad ball => save the ball from falling down
  - learning part
    - stdout has many things that are helpful like
      - getWindowSize() 
      - cursorTo() => moves the cursor to the specified position
      - clearScreenDown 
      - we also see the rows and columns
  
 -----------
 # 7 June 2023
 
 - tried to create trafficRider game with Swagato and Biswa
 - learning part
  - there was line where the program was potential to crash if invalid move is provided 
  - safety point of program from being crash
  - we can do 'key in objectName', it will return true or false

 ------------ 
 # 10 June 2023
 
 - learned that testing provides async testing
    - the second parameter of test is usually for that purpose
    - if we invoke the parameter that we passed, it means that I have done with running async function now you assert
    - also learned about context
    - there is calls, callCount, and under count there is arguments which shows what parameter has been passed

 - Jayanth Session
    - showed us about a way to approach to think of model , controller and viewer
    - i was surprised that without board we are able to play tictactoe, board wasn't the main 
    - we were able to understand the structuring of model, and it's easy to test without injecting
    - we tried to think in terms of entity, how independent they are
    - controller doesn't hold the logic part, it's just a medium to interact with your game   
    - code snippet
    
     ```javascript
        const { EventEmitter } = require('events');
        
        const Symbols = { X: 'X', O: 'O', EMPTY: ' ' };
        
        class Player {
          #name;
          #moves;
          #symbol;
          constructor(name, symbol) {
            this.#name = name;
            this.#symbol = symbol;
            this.#moves = new Set();
          }
        
          recordMove(move) {
            this.#moves.add(move);
          }
        
          getDetails() {
            return this.#name;
          }
        
          numberOfMoves() {
            return this.#moves.size;
          }
        
          movesMade() {
            return [...this.#moves].map(move => [move, this.#symbol]);
          }
        }
        
        class Players {
          #players;
          constructor(player1, player2) {
            this.#players = [player1, player2];
          }
        
          changeTurn() {
            this.#players.reverse();
          }
        
          recordMove(move) {
            this.#players[0].recordMove(move);
          }
        
          getCurrentPlayer() {
            // try not to break encapsulation?
            return this.#players[0].getDetails();
          }
        
          totalMovesMade() {
            return this.#players
              .map(player => player.numberOfMoves())
              .reduce((a, b) => a + b);
          }
        
          hasWon() {
            return false;
          }
        
          movesMade() {
            return Object.fromEntries(
              this.#players.flatMap(player => player.movesMade())
            );
          }
        }
        
        class Game {
          #players;
          #isGameOver;
          #winner;
          constructor(players) {
            this.#players = players;
          }
        
          makeMove(move) {
            this.#players.recordMove(move);
          
            if (this.#players.hasWon()) {
              this.#isGameOver = true;
              this.#winner = this.#players.getCurrentPlayer();
              return;
            }
          
            if (this.#players.totalMovesMade() === 9) {
              this.#isGameOver = true;
              return;
            }
          
            this.#players.changeTurn();
          }
        
          status() {
            return {
              moves: this.#players.movesMade(),
              currentPlayer: this.#players.getCurrentPlayer(),
              isGameOver: this.#isGameOver,
              winner: this.#winner,
            };
          }
        }
        
        class GameController {
          #game;
          #inputController;
          #renderer;
          constructor(game, inputController, renderer) {
            this.#game = game;
            this.#inputController = inputController;
            this.#renderer = renderer;
          }
        
          start() {
            this.#inputController.on('move-entered', move => {
              this.#game.makeMove(move);
              this.#renderer.render(this.#game.status());
            });
          
            this.#inputController.on('illegal-move', move => {
              console.log('Illegal move entered!');
            });
          
            this.#inputController.start();
          }
        }
        
        class KeyboardController extends EventEmitter {
          #stdin;
          #keymap;
          constructor(stdin, keymap) {
            super();
            this.#stdin = stdin;
            this.#keymap = keymap;
          }
        
          start() {
            this.#stdin.setRawMode(true);
            this.#stdin.setEncoding('utf-8');
            this.#stdin.on('data', data => {
              if (data === '\u0003') {
                this.#stdin.setRawMode(false);
                return;
              }
              if (this.#keymap[data] === undefined) {
                this.emit('illegal-move');
                return;
              }
              const [event, eventData] = this.#keymap[data];
              this.emit(event, eventData);
            });
          }
        }
        
        class GameRenderer {
          render({ moves, currentPlayer }) {
            for (let i = 0; i < 9; i += 3) {
              const row = [i, i + 1, i + 2].map(x => moves[x] || ' ').join('|');
              console.log(row);
            }
            console.log('');
            console.log(currentPlayer, "'s turn");
          }
        }
        
        module.exports = {
          Player,
          Players,
          Game,
          GameController,
          Symbols,
          KeyboardController,
          GameRenderer,
        };
    ```
    and the main.js

  ```javascript
    const {
      Symbols,
      Game,
      GameController,
      Player,
      Players,
      KeyboardController,
      GameRenderer,
    } = require('./ttt.js');
    // const EventEmitter = require('events');
    
    const keymap = {
      q: ['move-entered', 0],
      w: ['move-entered', 1],
      e: ['move-entered', 2],
      a: ['move-entered', 3],
      s: ['move-entered', 4],
      d: ['move-entered', 5],
      z: ['move-entered', 6],
      x: ['move-entered', 7],
      c: ['move-entered', 8],
    };
    
    const main = () => {
      const p1 = new Player('bittu', Symbols.X);
      const p2 = new Player('riya', Symbols.O);
      const players = new Players(p1, p2);
      const game = new Game(players);
      const keyboardController = new KeyboardController(process.stdin, keymap);
      const gc = new GameController(game, keyboardController, new GameRenderer());
      gc.start();
    };
    
    main();
  ```
  
----------
12 June 2023

Ashish and Dheeraj session about HTML
  - Before writing anything the whole thing is inside html tag
  - There are tags like head, body, table etc
  - In table tags there are other tags like
      - table row
      - table data
  - There are listing tags also 
      - ordered list 
      - unordered list
      - list tag needs to be included to list down items
  - There is anchor tag
      - We can use it to give hytext links
  - We came to know that tags have their attributes
    - attributes like style inside which we can select font size and color, border size type and color
    - you can separate the same properties by spaces and others by semicolons
    - for border  (example)
       - style="border: 1px solid black; // here it is separated by spaces
  - learned about pre which keeps the text as it is

----------
13 June 2023

Ashish and Dheeraj session about HTML 02
  - Learned about img tag in HTML
  - need to mention src 
    - it can be local or online source
  - in case you add alt which is alternative source or text you want to show in case the first source doesn't works
  - we made wikipedia

------------

20 June 2023

Suresh session about html

1st Half the topics we have covered
  - creating css files and linking it
  - discussed about rgba, hsl
  - we came to know about that if height is mentioned then we can mention the width via aspect ratio
  - CSS specificity
  - Related to Background
      - Image
      - Gradient (linear gradient to be specific)
      - Size
      - Repeat
      - Clip
        - -webkit (to make it compatible to other browser)

2nd Half the topics we have covered
  - box-shadow 
    - it consist of two co-ordinates, the widespread of the shadow effect and the color you want
  - position
    - absolute (it takes reference of the increment of co-ordinate from the corner of the screen also it removes the element)
    - relative (it take reference from the initial position of the element and it doesn't remove the space taken by it)
    - fixed (it remains stay on the screen and it overlap if any other element comes)
    - sticky (it stays on the screen on given co-ordinates as long as the parent has scrollable area) 

