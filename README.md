# Task-1
Q.1 import hashlib
import time

class Block:
    def __init__(self, index, data, previous_hash):
        self.index = index
        self.timestamp = time.time()
        self.data = data
        self.previous_hash = previous_hash
        self.nonce = 0
        self.hash = self.calculate_hash()

    def calculate_hash(self):
        block_string = f"{self.index}{self.timestamp}{self.data}{self.previous_hash}{self.nonce}"
        return hashlib.sha256(block_string.encode()).hexdigest()

# Build a chain of 3 blocks
blockchain = [Block(0, "Genesis Block", "0")]
blockchain.append(Block(1, "Second Block", blockchain[0].hash))
blockchain.append(Block(2, "Third Block", blockchain[1].hash))

# Print each block
for block in blockchain:
    print(f"Block {block.index}:")
    print(f"  Hash: {block.hash}")
    print(f"  Previous Hash: {block.previous_hash}")
    print(f"  Data: {block.data}")
    print()


    Q.2
    class MinerBlock(Block):
    def mine_block(self, difficulty):
        prefix = '0' * difficulty
        while not self.hash.startswith(prefix):
            self.nonce += 1
            self.hash = self.calculate_hash()
        return self.nonce

# Test mining
start_time = time.time()
mined_block = MinerBlock(0, "Mining Test Block", "0")
attempts = mined_block.mine_block(4)
end_time = time.time()

print(f"Block mined with nonce: {mined_block.nonce}")
print(f"Hash: {mined_block.hash}")
print(f"Attempts: {attempts}")
print(f"Time taken: {end_time - start_time:.2f} seconds")


Q.3
import random

# Proof of Work (PoW)
miners = {"MinerA": random.randint(1, 100), "MinerB": random.randint(1, 100)}
pow_winner = max(miners, key=miners.get)
print(f"PoW Winner: {pow_winner} with power {miners[pow_winner]}")

# Proof of Stake (PoS)
stakers = {"StakerA": random.randint(1, 100), "StakerB": random.randint(1, 100)}
pos_winner = max(stakers, key=stakers.get)
print(f"PoS Winner: {pos_winner} with stake {stakers[pos_winner]}")

# Delegated Proof of Stake (DPoS)
votes = {"Delegate1": 3, "Delegate2": 1}
dpos_winner = max(votes, key=votes.get)
print(f"DPoS Winner: {dpos_winner} with {votes[dpos_winner]} votes")
