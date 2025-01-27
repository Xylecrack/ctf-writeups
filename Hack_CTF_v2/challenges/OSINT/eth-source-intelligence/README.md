# Eth-source Intelligence

## Description

there are a lot of chained transactions and message data, can you retrace and find the flag?

[Final Transaction](https://sepolia.etherscan.io/tx/0x9bd77b2bd621e1bc6f1a9e6eb9798aac910194a76a1f8f565b59c182c6dec565)

### Steps involved:

1. **Transaction Details**:
   - Transaction Hash: [`0x9bd77b2bd621e1bc6f1a9e6eb9798aac910194a76a1f8f565b59c182c6dec565`](https://sepolia.etherscan.io/tx/0x9bd77b2bd621e1bc6f1a9e6eb9798aac910194a76a1f8f565b59c182c6dec565)

2. **Contract Involved**:
   - Contract Address: [`0xa725bbfbdeb0d36d904dc9b9fcc556d2ca3db902`](https://sepolia.etherscan.io/address/0xa725bbfbdeb0d36d904dc9b9fcc556d2ca3db902)

3. **Contract Creator**:
   - Creator Address: [`0x906Ec2A8BdCc27e4b884629F6379B0fdc2728E25`](https://sepolia.etherscan.io/address/0x906Ec2A8BdCc27e4b884629F6379B0fdc2728E25)

4. **Referenced Contract**:
   - Contract Address: `0x27257324f9832Bb9AC0676234cCb3E909ed44c03`
   - Input Data:
     ```
     00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000042307862656338633236326634316234353734666333623236373265616334366238663831303338333437633738323934633965613632396166666636363432383861000000000000000000000000000000000000000000000000000000000000
     ```

---

### Steps Taken:

#### 1. **Decoded Input Data**:
   The transaction's input data was decoded, revealing the following arguments:
   - `_message (string)`: `0xbec8c262f41b4574fc3b2672eac46b8f81038347c78294c9ea629afff664288a`

   **Interpretation**: This string appeared to reference an Ethereum address (`0xbec8c262f41b4574fc3b2672eac46b8f81038347c78294c9ea629afff664288a`).

#### 2. **Analyzed the Referenced Address**:
   - Visiting the address `0xbec8c262f41b4574fc3b2672eac46b8f81038347c78294c9ea629afff664288a` revealed additional input data containing:
     ```
     9Êk hacks{ethersc4n_o5Int)
     ```

#### 3. **Extracting the Flag**:
   - The flag format followed the pattern: `hacks{...}`.
   - From the data, we extracted the flag:

### Flag
hacks{ethersc4n_o5Int}
