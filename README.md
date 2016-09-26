# EVMDB

## Description
A simple Ethereum Virtual Machine Database (EVMDB).

It is used for creating and managing DBs on the EVM.

The functionality provided is simple:
- create a DB.
- insert, update, delete or read data from a DB.
- search a DB, where search is only exact search and only on one field ("the primary key") at the moment.

Further developments may include type checking, "select" search, complicated DB structues etc.

License:  MIT 

## Usage
The EVMDB can either be called from DAPPs or from another smart contract.

DB managing API:
- create(bytes32 _name, bytes32[] _headers): creates a DB called _name with headers _headers. Returns the ID of the newly created DB. It is assumed that _headers[0] is the primary key of the DB. Generates a 'DBCreated' event
- insert(uint256 _DB_id, bytes32[] _data): inserts row with data _data to _DB_ID. Returns the ID for the newly inserted row.
- erase(uint256 _DB_id, uint256 _row): erases row with id _row from _DB_id. Recall that in Solidity deletion of a row means exchanging all of its values with '0'.
- update(uint256 _DB_id, uint256 _row, bytes32[] _data): updates the data in row with id _row in _DB_id to be _data.

DB search API:
- search(uint256 _DB_id, bytes32 _value): a constant function. Searches the primary key (i.e, the first column) of _DB_id for _value. If found, returns the id of the row that contains the item (if the primary key allows duplications, then some row that fits the search is returned). If not found, returns '-1'.

DB read API:
- get_header(uint256 _DB_id). a constatnt function. Returns a bytes32[] array with the header names of _DB_id.
- get_row(uint256 _DB_id, uint256 _row). a constatnt function. Returns a bytes32[] array with data of row with id _row of _DB_id.
- get_row_col(uint256 _DB_id, uint256 _row, uint256 _col). a constatnt function. Returns the data in column id _col in row id _row in _DB_id. 
- get_DB_info(uint256 _DB_id). a constatnt function, returns an array of (DB address, DB owner (address), DB size) of _DB_id.
- get_number_of_DBs(). a constatnt function. Returns the number of DBs in the smart contract.

## Examples
A (demo Dapp)[link] using EVMDB was deployed to the ETH mainnet, testnet and ETC mainnet.

A demo smart contract using EVMDB is supplied in the examples folder in this repository (examples/EVMDB_SC_example.sol). 





