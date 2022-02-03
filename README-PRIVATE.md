***

# Mainnet-fork error

```vim 
  File "brownie/_cli/__main__.py", line 64, in main
    importlib.import_module(f"brownie._cli.{cmd}").main()
  File "brownie/_cli/run.py", line 44, in main
    network.connect(CONFIG.argv["network"])
  File "brownie/network/main.py", line 40, in connect
    web3.connect(host, active.get("timeout", 30))
  File "brownie/network/web3.py", line 67, in connect
    "Unknown URI - must be a path to an IPC socket, a websocket "
ValueError: Unknown URI - must be a path to an IPC socket, a websocket beginning with 'ws' or a URL beginning with 'http'
```

# Printing the private key in place of the address

```

print(f"Config wallet address: {val}")
        print(f"Config wallet address: {accounts.add(val)}")

          File "brownie/_cli/run.py", line 54, in main
    _include_frame=True,
  File "brownie/project/scripts.py", line 103, in run
    return_value = f_locals[method_name](*args, **kwargs)
  File "./scripts/get_weth.py", line 7, in main
    get_weth()
  File "./scripts/get_weth.py", line 22, in get_weth
    tx = weth.deposit({"from": account, "value": 0.1 * 10 ** 18})
  File "brownie/network/contract.py", line 1629, in __call__
    return self.transact(*args)
  File "brownie/network/contract.py", line 1495, in transact
    args, tx = _get_tx(self._owner, args)
  File "brownie/network/contract.py", line 1717, in _get_tx
    tx["from"] = accounts.at(tx["from"], force=True)
  File "brownie/network/account.py", line 244, in at
    address = _resolve_address(address)
  File "brownie/network/web3.py", line 193, in _resolve_address
    return to_address(domain)
  File "brownie/convert/main.py", line 43, in to_address
    return str(EthAddress(value))
  File "brownie/convert/datatypes.py", line 213, in __new__
    raise ValueError(f"'{value}' is not a valid ETH address") from None
ValueError: '0x87e99143b44a2a2a098253e4b7c2ad1cd423d58c8af3f9789734ae5b5988c441' is not a valid ETH address
```

# Lending pool address 
lending pool address can change quite a bit
Address provider which gives us the address of a particular market 
Address provider v2 is the most used on mainnet 
address provider registry will give us the address for different markets


getLendingPool()


# Adding a network 

brownie networks add development mainnet-fork-dev cmd=ganache-cli host=http://127.0.0.1 fork=https://eth-mainnet.alchemyapi.io/v2/4Vz3l5Ss42GEvoZ1hBOCJt0om2V-zU4v accounts=10 mnemonic=brownie port=8545


# Error when 0 ETH balance is present and we are trying to borrow against that on mainnet-fork 
```
You have 0 worth of ETH deposited.
You have 0 worth of ETH borrowed.
You can borrow 0 worth of ETH
Let's borrow
The DAI/ETH price is 0.00038270165
We are going to borrow 0.0 DAI
Transaction sent: 0x50a5f6a861a0f5d0abbe59ad326965ab54dfefdab4bd2ace612adc410a8f9d44
  Gas price: 0.0 gwei   Gas limit: 6721975   Nonce: 3
  Transaction confirmed (1)   Block: 14134904   Gas used: 48863 (0.73%)

  File "brownie/_cli/run.py", line 54, in main
    _include_frame=True,
  File "brownie/project/scripts.py", line 103, in run
    return_value = f_locals[method_name](*args, **kwargs)
  File "./scripts/aave_deposit.py", line 53, in main
    {"from": account},
  File "brownie/network/contract.py", line 1629, in __call__
    return self.transact(*args)
  File "brownie/network/contract.py", line 1513, in transact
    allow_revert=tx["allow_revert"],
  File "brownie/network/account.py", line 682, in transfer
    receipt._raise_if_reverted(exc)
  File "brownie/network/transaction.py", line 447, in _raise_if_reverted
    source=source, revert_msg=self._revert_msg, dev_revert_msg=self._dev_revert_msg
VirtualMachineError: revert: 1
```