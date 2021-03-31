# data-hub-nifty-project

![nifties2](https://user-images.githubusercontent.com/477757/113214897-f581af80-922e-11eb-904a-29db1a6a3539.jpg)

A project for [MarkLogic Data Hub](https://github.com/marklogic/marklogic-data-hub) that ingests, maps, and masters [NFT](https://en.wikipedia.org/wiki/Non-fungible_token) (aka nifty) digital art data.

## Key Files

* **/input:** Source JSON documents with art, artist, and sales information. Each source document will generate a single Artist, Nft, Release, and Results document when mapped.
* **/entities:** Entity definitions for:
  - **Artist:** Creator of the NFT art
  - **Nft:** NFT art piece
  - **Release:** A collection of one or more NFT art pieces released at the same time
  - **Results:** Sales results of the NFT art
* **/flows:** Data Hub flows for transforming the data:
  - **mapNifties:** Ingest and map the data to the entity definitions
  - **masterNifties:** Match identical entity instances and merge them
* **/data:** Data Hub steps to define the data transformations 

## Relationships

* **Artist** ---1:N---> **Nft**
* **Artist** ---1:N---> **Release**
* **Release** ---1:N---> **Nft**
* **Nft** ---1:1---> **Results**

## Steps for Transforming the Data

1. Initialize the project in MarkLogic Data Hub.
2. Run the steps in the mapNifties flow to ingest and map the NFT data. There will be duplicate Artist and Release documents.
3. Run the steps in the masterNifties flow to deduplicate the Artist and Release documents.
