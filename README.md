
# Error Handling

The "Error Handling" smart contract is a contract which is used and designed to demonstrate the error handling mechanisms in Solidity. This contract includes functions that uses require(), revert() and assert() statements to validate specific conditions and mange errors effectively.


## Contract Details
* Admin: The address that deploys the contract is set as the admin.
* Password: An address that can be set by the admin.
* Count: A counter that increments each time the onlyAdmin function is successfully called.

## Features
* require(): It is used for input validation. If `require()` statement fails, it reverts the transaction and refunds the remaining gas.
* revert(): It is used when an error condition is met, and execution should be stopped. When `revert()` is called, it reverts the transaction and refunds the remaining gas. Like require, it can take an optional error message.
* assert: It is used to check for conditions that should never be false. It is typically used for internal errors and to check invariants. If an `assert()` statement fails, it means there is a bug in the code. When an assert statement fails, it uses up all the remaining gas.
## Functions

    constructor(){
        admin = msg.sender;
        count = 0;
    }
The constructor sets value of the `admin`  to be the sender of the transaction that deployed this contract (i.e., it is run only once when the contract is first created). It also sets the `count` variable to 0 which will be useful for tracking actions performed by users later on.

    //require()
    function setPassword(address newPassword) public  {
        require(msg.sender == admin, "Only the admin can set a new password");
        require(newPassword != address(0), "New password address cannot be zero address");
        
        password=newPassword;
    }

This function take 1 paramteter and is used to set a new password. It uses `require()` to ensure that only admin can change the password and that new password address can not be zero address. 

    //revert()
    function onlyAdmin() public payable {
        if (msg.sender != admin) {
            revert("Only admin can call this action");
        }
        count++;
    }

This function can only be called by `admin`. If the caller is not admin, it uses `revert()` to throw an error and if the caller is admin it increments the count value by 1.

    function getCount() public view returns(uint256){
        return count;
    }

This function returns the current value of counter variable `count`.

    //assert()
    function checkAdmin() public view {
        assert(msg.sender == admin);
    }
This function also checks if the caller is admin or not. If the caller is not the admin, the transaction will fail and will consume all the remaining gas.
