# Smart Contract Architecture

## eco-token
- Address: TBD (deployed)
- Interface:
  - `initialize(admin: Address, name: String, symbol: String, decimal: u32)`
  - `mint(to: Address, amount: i128)`
  - `transfer(from: Address, to: Address, amount: i128)`
  - `balance(id: Address) -> i128`
- Storage: ephemeral balances, instance metadata
- Access Control: only admin can mint

## task-registry
- Interface:
  - `initialize(admin: Address)`
  - `create_task(creator: Address, task_type: String, location_hash: BytesN<32>, reward_amount: i128, expires_at: u64) -> u64`
  - `get_task(task_id: u64) -> Task`
  - `complete_task(task_id: u64, user: Address)`
  - `expire_task(task_id: u64)`
- Task struct stored on-chain

## reward-engine
- Interface:
  - `initialize(token: Address, registry: Address, oracle: Address)`
  - `process_reward(user: Address, task_id: u64, proof_cid: String, amount: i128)`
  - `dispute_reward(task_id: u64)`
