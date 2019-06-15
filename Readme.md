## Overview

BrainLearn is a free, powerful UCI chess engine derived from BrainFish ([https://zipproth.de/Brainfish/download/](https://zipproth.de/Brainfish/download/)). It is not a complete chess program and requires a UCI-compatible GUI (e.g. XBoard with PolyGlot, Scid, Cute Chess, eboard, Arena, Sigma Chess, Shredder, Chess Partner or Fritz) in order to be used comfortably. Read the documentation for your GUI of choice for information about how to use Stockfish with it.

## Files

This distribution of Stockfish consists of the following files:

- Readme.md, the file you are currently reading.
- Copying.txt, a text file containing the GNU General Public License version 3.
- src, a subdirectory containing the full source code, including a Makefile that can be used to compile Stockfish on Unix-like systems.

## UCI parameters

BrainLearn hash the same options as BrainFish, but it implement a persisted learning algorithm, reading and creating the following files types:

- pawn.bin with the learning when there are max a total of 2 pieces for white and black
- experience.bin with the learning for
  - opening variation of max 16 moves (8 half-moves) and a total of at least 7 pieces (no pawns) for white and black
  - positions with max 6 pieces (no pawns) for white and black
- One or many .bin files, each one associated to a single position biunivocally associated to the (technically, hashKey), in an opening variation of max 8 moves (16 half-moves) and a total of at least 7 pieces (no pawns) for white and black. This position is also in the experience.bin. So, these files are to speed the load in memory.

Every .bin file is so a collection of one or more positions stored with the following format (similar to in memory Stockfish Transposition Table):

- _best move_
- _board signature (hash key)_
- _best move depth_
- _best move score_

At the engine loading, there is an automatic merge to pawn.bin and experience.bin files, if we put the other ones, based on the following convention:

&lt;fileType&gt;&lt;qualityIndex&gt;.bin

where

- _fileType=&quot;experience&quot;/&quot;bin&quot;_
- _qualityIndex_ , an integer, incrementally from 0 on based on the file&#39;s quality assigned by the user (0 best quality and so on)

The opening files can be simply copied and, in case of conflict/same name, the user must choice the one to use.

N.B.

Because of disk access, to be effective, the learning must be made at no bullet time controls (less than 5 minutes/game).

## Terms of use

BrainLearn is free, and distributed under the **GNU General Public License version 3** (GPL v3). Essentially, this means that you are free to do almost exactly what you want with the program, including distributing it among your friends, making it available for download from your web site, selling it (either by itself or as part of some bigger software package), or using it as the starting point for a software project of your own.

The only real limitation is that whenever you distribute Stockfish in some way, you must always include the full source code, or a pointer to where the source code can be found. If you make any changes to the source code, these changes must also be made available under the GPL.

For full details, read the copy of the GPL v3 found in the file named _Copying.txt_.