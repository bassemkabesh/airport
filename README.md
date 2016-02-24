# Introduction
This is a visual puzzle solver for [Smartgames "Airport" puzzle.](http://www.smartgames.eu/en/smartgames/airport)

In this puzzle you are given a card with a 4x4 map showing the designated positions for the planes.
To solve the puzzle you have to place the 6 playing pieces on top the challenge card so that the planes
are in their designated positions and flying in the right directions.
![test](http://cdn2.smartgames.eu/sites/default/files/styles/medium/public/gamerules/airportSTEP_2.jpg?itok=wjkJFUT2)

This project tries to solve the puzzle by visually analysing the image of the card,
figuring out the planes designated positions and other constraints and finding the solution in the entire solution space.
Once found, the solution is displayed on the screen.

# Setup
TODO

# How does it work?
0.  In a preprocessing step we find ALL possible solutions. We try all the different ways to cover a 4x4 grid with the given pieces.
    When we succeed we store the solution in a database file for later retrieval.

    Fun fact, there are 18,432 solutions to this puzzle (which are actually 4,608 unique solutions).

    See `solutions.py` for more details. Here, for example, are two solutions from the database:

    ```
    ...
       AIR        AIR        AIR        AIR        AIR        AIR
       AIR      I_ORANGE   I_ORANGE    I_RED      I_RED       AIR
       AIR      L_BLACK    L_BLACK     L_BLUE     L_BLUE      AIR
       AIR      L_BLACK    L_GREEN     L_BLUE     L_RED       AIR
       AIR      L_GREEN    L_GREEN     L_RED      L_RED       AIR
       AIR        AIR        AIR        AIR        AIR        AIR
    ...
       AIR        AIR        AIR        AIR        AIR        AIR
       AIR      I_ORANGE   I_ORANGE    I_RED      I_RED       AIR
       AIR      L_BLACK    L_BLACK     L_BLUE     L_BLUE      AIR
       AIR      L_BLACK     L_RED      L_BLUE    L_GREEN      AIR
       AIR       L_RED      L_RED     L_GREEN    L_GREEN      AIR
       AIR        AIR        AIR        AIR        AIR        AIR
    ...
    ```


1.  Given an image frame from the camera, we first find the card's position in the image.

    ![](https://i.imgur.com/4MYaATp.jpg)


2.  Next, we divide the 4x4 grid into 16 black and white images.

    ![](https://i.imgur.com/SofbtJl.png)


3.  We use template matching to find the objects in these squares, specifically, planes with different orientations and local constraints.

    Now we have an internal representation of the board:

    ```
       AIR        AIR        AIR        AIR        AIR        AIR
       AIR        DOWN       AIR        AIR        LEFT       AIR
       AIR        AIR        AIR         UP        AIR        AIR
       AIR        AIR        LEFT       AIR        LEFT       AIR
       AIR        AIR        AIR        DOWN       AIR        AIR
       AIR        AIR        AIR        AIR        AIR        AIR
    ```

4.  We search for a solution by looking it up in the solutions database. Finally, we show the solution to the user.

    ![](https://i.imgur.com/rH8AIjU.png)


