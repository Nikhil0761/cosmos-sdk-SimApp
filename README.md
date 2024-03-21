# cosmos-sdk-SimApp

# SimApp

SimApp is an application built using the Cosmos SDK for testing and educational purposes.

We will create a new blockchain, create 2 nodes and perforn transaction between them.



## Deployment

To get started creat a project folder and clone the repository.

```bash
  $ mkdir cosmos
  $ cd cosmos 
  $ git clone https://github.com/Nikhil0761/cosmos-sdk
  $ cd cosmos-sdk
```

Make sure you are using the same version used at the time of writing:

```bash
  $ git checkout v0.45.4
```
Build a node 

```bash
  $ make build
```
This command will build a node

Check and enter the build
```bash
  $ ls build/
  $ cd build/
```



## Initialisation

If you are returning and want to reset your blockchain to an uninitialised state

```bash
  $ ./simd comet unsafe-reset-all
```

To create a new blockchain 

```bash
  $ ./simd init demo
```

Since it is a new blockchain, it does not have any key.

Let's add a key
```bash
  $ ./simd keys add [key_name]
```
Since it's a new blockchain, it does not have any validators, so we have to bootstrap this process.

We will give our newly created key some tokens and then stake a large portion of its token
```bash
  $  ./simd add-genesis-account [key_name] [amount]
```

Now, to create a validator, we will stake a large portion of its token.
```bash
  $  ./simd gentx [key_name] [stake-amount] --chain-id [chain_id]
```

Now, gather all the inputs for genesis blockchain
```bash
  $  ./simd collect-gentxs
```
We can now start the blockchain
```bash
  $  ./simd start
```
You can see it create bocks and validate them.

## Transaction

To perform a Transaction, create a new node, e.g. student.

```bash
  $ ./simd keys add student
```
Since it is a new account, it will not have any balance.

Send some tokens from the first key to the student
```bash
  $ ./simd tx bank send $(./simd keys show [key_name] -a) $(./simd keys show student -a) [amount] --chain-id [chain_id]
```
Check the balance to verify.
