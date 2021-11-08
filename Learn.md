# Visibility

Functions and state variables have to declare whether they are accessible by other contracts.

## Function visibility

Functions can be declared as

- `public` - any contract and account can call
- `private` - only inside the contract that defines the function
- `internal` - only inside contract that inherits an `internal` function
- `external` - only other contracts and accounts can call

## Private functions

Let's define a private function inside a contract:

```
contract BaseVisibility {
    function privateFunc() private pure returns (string memory) {
        return "private function called";
    }

    function testPrivateFunc() public pure returns (string memory) {
        return privateFunc();
    }
}
```

Private function can only be called inside this contract.
Hit `Run` you will see that 2nd test passes. Because `privateFunc` can be called only inside the contract.

## Accessing private functions from other contracts

Contracts that inherit `BaseVisibility` contract cannot call `privateFun` function.
Let's write a contract that inherits `BaseVisibility` contract:

```
contract ChildVisibility is BaseVisibility {
    function testPrivateFunc() public pure returns (string memory) {
        return privateFunc();
    }
}
```

Hit `Run` and you will see that 3rd test fails with DeclarationError: Undeclared identifier.
Because `privateFunc` is not accessible by `ChildVisibility` contract but only accessible by `BaseVisibility` itself.

Comment out `testPrivateFunc` function in `ChildVisibility` contract or else further test won't compile.

## Internal functions

Let's define an internal function inside a `BaseVisibility` contract:

```
    function internalFunc() internal pure returns (string memory) {
        return "internal function called";
    }
```

Internal function can be called:

- inside this contract
- inside contracts that inherit this contract

Let's write a function to call `internalFunc` from `ChildVisibility` contract:

```
    function testInternalFunc() public pure override returns (string memory) {
        return internalFunc();
    }
```

Hit `Run` and you will see that 4th test passes. Because `internalFunc` can be called from `ChildVisibility` contract.

## Public functions

Let's define a public function inside a `BaseVisibility` contract:

```
    function publicFunc() public pure returns (string memory) {
        return "public function called";
    }
```

Public functions can be called:

- inside this contract
- inside contracts that inherit this contract
- by other contracts and accounts

## External functions

Let's define an external function inside a `BaseVisibility` contract:

```
    function externalFunc() external pure returns (string memory) {
        return "external function called";
    }
```

External functions can only be called:

- by other contracts and accounts

## State variables visibility

State variables can be declared as `public`, `private`, or `internal` but not `external`.

```
    string private privateVar = "my private variable";
    string internal internalVar = "my internal variable";
    string public publicVar = "my public variable";
```
