# Why are vanilla servers lagging?

- The main reasons for causing the loss of ticks are mobs/entities and, in frequent case - chunks
- Of course, a patch with a new chunk system from SpottedLeaf has been published in the new versions of Paper, but this does not cancel any load of chunks on your vanilla server. Especially new chunks - they are the most difficult to process by the server. Imagine, if 50 players of your server go to load new chunks + mobs and entities load your server. For example, your MSPT (Milliseconds per tick) is ~25-35 due to the number of mobs and entities, then when uploading new chunks, this can increase your average MSPT, for example, from 35 to 45-55 or even to 60-75 for a short time and then go back again.

# How to deal with mobs and entities?

- Unfortunately, there is currently no public stable way to get all mobs into multithreaded CPU mode. Of course, there are developments from various developers, but they can cause a lot of problems that you may not fix in the configuration or you will damage the files of your world in this way, so they are always marked by the authors as:

- Under Heavy Development
- Not recommended for production
- Heavy Alpha
- PreAlpha
- Unstable

- ...
