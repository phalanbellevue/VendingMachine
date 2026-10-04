# TEST PLAN

## VendingMachine

| Method / Behavior | Valid Case(s) | Exception / Invalid Case(s) | Boundary Case(s) | Oracle / Expected Result | Related JUnit Test(s) |
|---|---|---|---|---|---|
| Constructor | Create a new machine | N/A | Initial balance = 0 | Javadocs say the machine starts empty with a balance of 0 | testConstructor_newMachine_hasZeroBalance |
| addItem() | Add item to empty slot | Occupied slot or invalid code | Slots A-D | Javadocs say item is added to the specified empty slot | testAddItem_emptySlot_storesItem, testAddItem_occupiedSlot_throwsException |
| getItem() | Get item from a slot | Invalid code | Empty slot returns null | Javadocs say it returns the item in the specified slot | testGetItem_occupiedSlot_returnsItem |
| removeItem() | Remove item from occupied slot | Empty slot or invalid code | Empty vs. occupied | Javadocs say the item is removed and returned | testRemoveItem_occupiedSlot_returnsItem, testRemoveItem_emptySlot_throwsException |
| insertMoney() | Insert positive amount | Negative amount | 0 is the minimum valid amount | Javadocs say amount must be >= 0 and is added to balance | testInsertMoney_validAmount_increasesBalance, testInsertMoney_negativeAmount_throwsException, testInsertMoney_validBoundaryAmounts_increasesBalance |
| getBalance() | Get current balance | N/A | Balance = 0 | Javadocs say the current balance is returned | testGetBalance_afterInsert_returnsCurrentBalance |
| makePurchase() | Purchase with enough money | Empty slot or insufficient money | Below, equal to, and above item price | Javadocs define when a purchase succeeds or fails | testMakePurchase_balanceClasses_returnsExpectedResult |
| returnChange() | Return current balance | N/A | Balance = 0 | Javadocs say balance is returned and reset to 0 | testReturnChange_positiveBalance_returnsCurrentBalance, testReturnChange_zeroBalance_returnsZero |

## VendingMachineItem

| Method / Behavior | Valid Case(s) | Exception / Invalid Case(s) | Boundary Case(s) | Oracle / Expected Result | Related JUnit Test(s) |
|---|---|---|---|---|---|
| Constructor | Positive price | Negative price | Price = 0 | Javadocs say price must be >= 0 | testConstructor_validPrice_createsItem, testConstructor_negativePrice_throwsException, testConstructor_zeroPrice_createsItem |
| getName() | Get item name | N/A | N/A | Javadocs say the item's name is returned | testGetName_createdItem_returnsName |
| getPrice() | Get item price | N/A | Price = 0 | Javadocs say the item's price is returned | testGetPrice_createdItem_returnsPrice |

## VendingMachineException

| Method / Behavior | Valid Case(s) | Exception / Invalid Case(s) | Boundary Case(s) | Oracle / Expected Result | Related JUnit Test(s) |
|---|---|---|---|---|---|
| Constructor | Create exception with message | N/A | N/A | Constructor stores the supplied exception message | testConstructor_withReason_storesMessage |

## Parameterized Test

`testMakePurchase_balanceClasses_returnsExpectedResult` uses six balance
values to test the same purchase behavior.

The values represent balances below, equal to, and greater than the item's
price. This tests the boundary where a purchase changes from failing to
succeeding.
