### Validating blockchain:

Erroneous data was inserted in the csv files. Validating that each transaction respects UTXOs spending rules and creating enables us to detect those anomalies. We find the following fraudulent transactions:
* 52534, 2 coinbases!
* 11181, tries to mint more 10 satoshis that are not in fees...
* 12042, Double spend attack for output 7998, spent at input 521...
* 15567, Tries to spend an output that does not exist (yet)
* 30223, Tries to double spend the same output (21928) in the same TX
* 56565, Tries to double spend output 65403
* 72902, Outputs higher (10 satoshis) then input
* 75047, Tries to have a negative 50 BTC output...
* 79885, Tries to spend an output from a block with 2 coinbases...
* 88755, Tries to spend the output that it creates to create it
* 96607  Tries to spend an output that has not been created yet.


### Basic data exploration

Number of UTXOs as of last block:
71887

Maximum value of an UTX0:
90000 BTC (90000 * 10^8 satoshis.)

Lowest address:
172
Amount UTXO:
998547.75176268001

Received most BTC (49980) in tx: 98122

### Potential issues with our clustering heuristics

False positives:
* exact change so we cluster input and output
* Roomates paying rent together (clustering inputs when two different ppl)

False negatives:
* Sending money to someone else (we cannot detect change adress)
* Sending money to oneself with two outputs
* Coinbases not found as belonging to same person until they are spent...

To make clustering more accurate we could:
* Try to use values to get a guess of who we can cluster (e.g if we know some item on
bitmazon is 0.06737461 BTC we might look for all the addresses that receive that amount and
say they all belong to bitmazon).
* Try to use time of the day: if they are the same person they are likely to spend at the same time
* Try to use other infos such as coinbase nonce patterns (some might chose at random, others increment).
* Look for adresses paying to the same third party, they are more likely to be the same person.
