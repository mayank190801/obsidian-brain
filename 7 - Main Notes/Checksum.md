
2024-07-17 10:07
Status: 
Tags:

# Checksum

- In a distributed system, while moving data between components, it is possible that the data fetched from a node may arrive corrupted
- To calculate a checksum, a cryptographic hash function like MD5, SHA-1, SHA-256, or SHA-512 is used. The hash function takes the input data and produces a string (containing letters and numbers) of fixed length; this string is called the checksum.
- When a system is storing some data, it computes a checksum of the data and stores the checksum with the data.
- When a client retrieves data, it verifies that the data it received from the server matches the checksum stored. If not, then the client can opt to retrieve that data from another replica.

####  Uses of Checksum
- Data Integrity Checks - ( you wanna make sure it doesn’t get altered during transmission)
- **Error Detection** - (helping systems know when they need to try downloading it again)
- **Data Retrieval and Verification** - (download software or a file from a website, they often provide a Checksum value, help to verify that it is exactly what the creators intended, no nasty surprises hiding inside)
- **Networking** - (Checksums help detect errors in packets of data sent over a network)
- Secure Storage - (Periodically, the stored data is checked against the Checksum)
- **Password Verification** - (store only checksum, and if password entered convert to checksum and then compare)
- **Preventing Accidental Duplicates** - (If two pieces of data have the same Checksum, they might be duplicates, saving storage space and preventing redundancy!)









# **References**