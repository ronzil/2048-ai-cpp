AI for the [2048 game](http://gabrielecirulli.github.io/2048/). This uses a random evaluation algorithm, along with a highly-efficient bitboard representation.

After seeing several AI projects for the game, I was interested in creating an AI that does not contain any hard-coded knowledge about the game (like scoring functions, hueristics etc). Instead the AI should "find out for itself" without me, the programmer having to know anything about game stratagy.

The implemented algorithm chooses which move to play like this: For each possible move, play it and then continue to play **random moves** until the game is finished. This is done many times and the move that returns the highest avarage score is chosen.

The success of the AI is surprising as a random-walk game finishes quite quickly, yet chosing the highest yielding move among the random-walk games, results in very good game play. 

The default build runs 10000 games per move and results in 100% success rate in achiving the 2048 tile, 70% for 4096 tile, and about 1% for the 8192 tile!

Apart from the basic algorithm of avaraging the end score per move, I tried a few other techniques including:
- Using the max, min, or some combination of them
- Using depth: Instead of avaraging each of the 4 moves, The AI avarages a move list's (for example left left up) results together.
- Using a type of Markov Chain: Creating a move tree of a given depth and calculating the conditional probablity of each state.

I didn't manage to gain any segnificant improvments with any of these changes. You can play around with them in the code.

Hat tip to nneonneo for creating this very clever and fast playing infrastucture.

For more detail on how it works, [check out my answer on stackoverflow](http://stackoverflow.com/a/22389702/1056032).

## Building

### Unix/Linux/OS X

Execute

    ./configure
    make

in a terminal. Any relatively recent C++ compiler should be able to build the output.

Note that you don't do `make install`; this program is meant to be run from this directory.

### Windows

You have a few options, depending on what you have installed.

- Pure Cygwin: follow the Unix/Linux/OS X instructions above. The resulting DLL can *only* be used with Cygwin programs, so
to run the browser control version, you must use the Cygwin Python (not the python.org Python). For step-by-step instructions, courtesy Tamas Szell (@matukaa), see [this document](https://github.com/nneonneo/2048-ai/wiki/CygwinStepByStep.pdf).
- Cygwin with MinGW: run

        CXX=x86_64-w64-mingw32-g++ CXXFLAGS='-static-libstdc++ -static-libgcc -D_WINDLL -D_GNU_SOURCE=1' ./configure ; make

    in a MinGW or Cygwin shell to build. The resultant DLL can be used with non-Cygwin programs.
- Visual Studio: open a Visual Studio command prompt, `cd` to the 2048-ai directory, and run `make-msvc.bat`.

## Running the command-line version

Run `bin/2048` if you want to see the AI by itself in action.

## Running the browser-control version

Install [Remote Control for Firefox](https://addons.mozilla.org/en-US/firefox/addon/remote-control/).

Open up the [2048 game](http://gabrielecirulli.github.io/2048/) or any compatible clone and start remote control.

Run `2048.py` and watch the game!
