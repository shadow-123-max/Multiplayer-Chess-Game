# Multiplayer-Chess-Game

A simple multiplayer chess game implemented using HTML5, CSS, and JavaScript. This game allows two players to play chess on a single board, with basic functionality for piece movement, capturing, and game state management.

![image](https://github.com/user-attachments/assets/c740189e-eab7-41e3-9175-b3b8082fc276)

## Features

- Chessboard: An 8x8 chessboard with alternating black and white tiles.
- Piece Movement: Support for standard chess piece movements including pawn, knight, bishop, rook, queen, and king.
- Capture Mechanics: Pieces can capture opponent's pieces.
- me State: Tracks casualties and victories for both white and black pieces.
- Turn Management: Alternates turns between white and black.
- Highlighting: Highlights valid moves and captures.

## Getting Started

To run the chess game, follow these steps:

1. Clone the Repository:
    ```bash
    git clone https://github.com/shadow-123-max/Multiplayer-Chess-Game-on-AWS-EC2
    ```
2. Navigate to the Project Directory:
    ```bash
    cd multiplayer-chess-game
    ```

3. Open the Project:
    Open the `index.html` file in your web browser.

## Project Structure

- `index.html`: The main HTML file containing the game structure and layout.
- `js/script.js`: JavaScript file containing the game logic and rendering functions.


## Key Files

### `index.html`

Contains the HTML structure of the chess game, including the canvas for drawing the board and pieces.

### `js/script.js`

Handles the game logic, including:
- Initialization of the game board and pieces.
- Piece movement and capturing logic.
- Drawing of the chessboard and pieces on the canvas.
- Handling user interactions such as clicks.

## Usage

1. Start a New Game:
    - The game automatically starts when the page loads.
    - White starts first, followed by black.

2. Make a Move:
    - Click on a piece to select it.
    - Click on a valid move location to move the piece.

3. Capture Pieces:
    - Move a piece to an opponent's piece to capture it.

4. End of Game:
    - The game resets if a king is captured.

## Customization

- Adjust Board Size: Modify `BOARD_WIDTH` and `BOARD_HEIGHT` in `script.js`.
- Change Piece Characters: Update `piecesCharacters` in `script.js` to use different symbols or images.

##Deploy this app to cloud (AWS EC2)

1.Create EC2 instance using amazon console, also in security group add a rule to allow HTTP incoming traffic.

2.Now connect to your instance using a command like this,
ssh -i "C:\Users\Viral\.ssh\chess.pem" ubuntu@ec2-3-133-88-210.us-east-2.compute.amazonaws.com

3.nginx setup:

          3.1-Install nginx on EC2 instance using these commands,
          sudo apt-get update
          sudo apt-get install nginx
          
          3.2-Above will install nginx as well as run it. Check status of nginx using
          sudo service nginx status
          
          3.3-Here are the commands to start/stop/restart nginx
          sudo service nginx start
          sudo service nginx stop
          sudo service nginx restart
          
          3.4-Now when you load cloud url in browser you will see a message saying "welcome to nginx" This means your nginx is setup and running.

4.Now you need to copy all your code to EC2 instance. You can do this either using git or copy files using winscp. We will use winscp. You can download winscp from here: https://winscp.net/eng/download.php

5.Once you connect to EC2 instance from winscp (instruction in a youtube video), you can now copy all code files into /home/ubuntu/ folder. The full path of your root folder is now: /home/ubuntu/Multiplayer Chess Game

6.After copying code on EC2 server now we can point nginx to load our property website by default. For below steps,

          6.1-Create this file /etc/nginx/sites-available/chess.conf. The file content looks like   this,
                            server {
                                listen 80;
                                    server_name bhp;
                                    root /home/ubuntu/BangloreHomePrices/client;
                                    index app.html;
                                    location /api/ {
                                         rewrite ^/api(.*) $1 break;
                                         proxy_pass http://127.0.0.1:5000;
                                    }
                            }
          
          6.2-Create symlink for this file in /etc/nginx/sites-enabled by running this command,
          sudo ln -v -s /etc/nginx/sites-available/chess.conf
          
          6.3-Remove symlink for default file in /etc/nginx/sites-enabled directory,
          sudo unlink default

6.4-Restart nginx,
sudo service nginx restart

7.Go to the File
/home/ubuntu/Multiplayer Chess Game/index.html
Running last command above will prompt that server is running on port 5000. 8. Now just load your cloud url in browser and this will be fully functional website running in production cloud environment

Enjoy the game..
