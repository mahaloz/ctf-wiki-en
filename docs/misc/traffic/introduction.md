In CTFs, analyzing traffic packets is an important part of performing an investigation.  

Often the competition will provide a traffic packets PCAP file, where players need to repair or rebuild the files transferred in the PCAP file to perform analysis.

PCAP is the key research direction, the complication is that the packets are filled with a lot of irrelevant traffics, so filter out the irrelevant traffics will be necessary.


Overall, there are the following steps:


- Overall Grasp
  - Agreement Rating
  - Endpoint Statistics
- Filter Relevant Information
  - Filter Syntax
  - Host, Protocol, Contains, Flags
- Find Exceptions
  - Special Strings
  - A Protocol Field
  - Flag Located On The Server
- Data Extraction
  - Strings Extraction
  - Files Extraction


In general, CTF traffic packets analysis falls into these 3 categories:


- Repair Traffic Packet (PCAP) File
- Protocol Analysis
- Data Extraction
