# Peer-to-peer-architecture-implementation-to-transfer-the-file-between-machines
The file owner has a file, and it breaks the file into chunks of 100KB, each stored as a 
separate file. Note that the last chunk can be smaller than 100KB. The minimum number
of chunks that the file can be split into is 5. The file owner listens on a TCP port. It 
should be designed as a server that can run multiple threads to serve multiple clients 
simultaneously.
Each peer should be able to connect to the file owner to download some chunks. It then 
should have two threads of control, one acting as a server that uploads the local chunks to 
another peer (referred to as upload neighbor), and the other acting as a client that 
downloads chunks from a third peer (referred to as download neighbor). So each peer has 
two neighbors, one of which will get chunks from this peer and the other will send 
chunks to this peer. You can arbitrarily decide on the neighboring relationship as long as 
the network is connected --- there is a direct path from any peer to any other peer. The 
neighboring relationship may be encoded through input parameters (see below).
1. Start the file owner process, giving a listening port.
2. Start five peer processes, one at a time, giving the file owner’s listening port, the 
peer’s listening port, and its download neighbor’s (another peer) listening port. 
3. Each peer connects to the server’s listening port. The latter creates a new thread to 
upload one or several file chunks to the peer, while its main thread goes back to 
listening for new peers.
4. After receiving chunk(s) from the file owner, the peer stores them as separate file(s)
and creates a summary file, listing the IDs of the chunks it has.
5. The peer then proceeds with two new threads, with one thread listening to its upload
neighbor to which it will upload file chunks, and the other thread connecting to its 
download neighbor. 
6. The peer requests for the chunk ID list from the download neighbor, compares with 
its own to find the missing ones, and randomly requests a missing chunk from the 
neighbor. In the meantime, it sends its own chunk ID list to its upload neighbor, and 
upon request uploads chunks to the neighbor. 
7. After a peer has all file chunks, it combines them for a single file. 
8. A peer MUST output its activity to its console whenever it receives a chunk, sends a 
chunk, receives a chunk ID list, sends out a chunk ID list, requests for chunks, or 
receives such a request. 

Instruction to run file

1.Open 6 terminal and locate each file.

2.store file in fileowner which is to be transfered

3.In fileOwner terminal type python FileOwner.py 5000

4.In peer 1 type python peer.py 5000 5001 5002 same in peer 2 type python peer.py 5000 5002 5003

5.in peer 3 type python peer.py 5000 5003 5004 similarly for 4 type python peer.py 5000 5004 5005 and 5 type python peer.py 5000 5005 5001

6.After this run all file simultaneously so it will transfer file in each of the peer

7.This is also can be done in different computer also .
