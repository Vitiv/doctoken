# aVa Doctoken (draft ICRC-7 version)

## Overview

Coming soon...

## ICRC-7 Specification

For standard methods and structures documentation, read the [specifications](https://github.com/dfinity/ICRC/blob/main/ICRCs/ICRC-7/ICRC-7.md).

### Deployment

### Available methods
All ICRC-7 methods available except icrc7_transfer

Additional method: 

#### addUser
Add the member to the whitelist for update calls.
The deployer is whitelisted by default.

```candid "Methods" +=
addUser : (principal) -> (bool);
```

#### removeUser
Remove the principal from the whitelist.
The last user will not be deleted.

```candid "Methods" +=
removeUser : (principal) -> (bool);
```

#### burn
```candid "Methods" +=
burnArg : (TransferArgs) -> (variant { Ok: nat; Err: TransferError; });
```

```candid "Type definitions" +=
type Subaccount = blob;

type Account = record {
		owner: principal; 
		subaccount: opt blob;
  };
  
type TransferArgs = record {
    spender_subaccount: opt Subaccount; // the subaccount of the caller (used to identify the spender)
    from: opt Account;     /* if supplied and is not caller then is permit transfer, if not supplied defaults to subaccount 0 of the caller principal */
    to: Account;
    token_ids: vec {nat};   
    memo: ?Blob;
    created_at_time: opt nat64;
    is_atomic: opt bool;
  };

type TransferError = variant {
    Unauthorized: record { token_ids: vec (nat) };
    TooOld;
    CreatedInFuture: record { ledger_time: nat };
    Duplicate: record { duplicate_of: nat };
    TemporarilyUnavailable: {};
    GenericError: record { error_code: nat; message: text };
  };
```





