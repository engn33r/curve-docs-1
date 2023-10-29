AVAX: https://snowtrace.io/address/0x9B7f0b68d70A741B8CB08A8e8423CcB72e630Db6#code



## **Gauge Types**

### `get_gauge_type`
!!! description "`GaugeTypeOracle.get_gauge_type(_gauge: address) -> uint256:`"

    Getter for the gauge type of an account.

    Returns: gauge type (`uint256`).

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `_gauge` |  `address` | gauge address |

    ??? quote "Source code"

        ```python
        gauge_type: HashMap[address, uint256]  # a value of 0 signifies the account is not a valid gauge

        @view
        @external
        def get_gauge_type(_gauge: address) -> uint256:
            """
            @notice Get the gauge type of an account
            @dev This method will revert if the gauge type has not been set yet
            """
            return self.gauge_type[_gauge] - 1
        ```

    === "Example"

        ```shell
        >>> GaugeTypeOracle.get_gauge_type('todo')
        ```


### `set_gauge_type`
!!! description "`GaugeTypeOracle.set_gauge_type(_gauge: address, _type: uint256):`"

    Function to set the gauge type of an account.

    Emits: `SetGaugeType`

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `_gauge` |  `address` | gauge address |
    | `_type` |  `address` | gauge type |

    ??? quote "Source code"

        ```python
        event SetGaugeType:
            gauge: indexed(address)
            type: uint256

        gauge_type: HashMap[address, uint256]  # a value of 0 signifies the account is not a valid gauge

        @external
        def set_gauge_type(_gauge: address, _type: uint256):
            """
            @notice Set the gauge type of an account
            @dev This method will increment the value of `_type` by 1 prior to storing,
                since a value of 0 signifies an invalid gauge.
            """
            assert msg.sender == self.owner  # dev: only owner

            self.gauge_type[_gauge] = _type + 1
            log SetGaugeType(_gauge, _type)
        ```

    === "Example"

        ```shell
        >>> GaugeTypeOracle.set_gauge_type('todo')
        ```


## **Ownership**

### `owner`
!!! description "`GaugeTypeOracle.owner() -> address: view`"

    Getter for the owner of the contract.

    Returns: owner (`address`).

    ??? quote "Source code"

        ```python
        owner: public(address)
        ```

    === "Example"

        ```shell
        >>> GaugeTypeOracle.owner()
        '0x487802abfdec059bfea7f319e0e5f7257a53b434'
        ```


### `future_owner`
!!! description "`GaugeTypeOracle.future_owner() -> address: view`"

    Getter for the future owner of the contract.

    Returns: future owner (`address`).

    ??? quote "Source code"

        ```python
        future_owner: public(address)
        ```

    === "Example"

        ```shell
        >>> GaugeTypeOracle.future_owner()
        '0x487802abfdec059bfea7f319e0e5f7257a53b434'
        ```


### `commit_transfer_ownership`
!!! description "`GaugeTypeOracle.commit_transfer_ownership(_future_owner: address):`"

    !!!guard "Guarded Method"
        This function is only callable by the `owner` of the contract.

    Function to commit a transfer of ownership to `_future_owner`.

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `_future_owner` |  `address` | future owner address |

    ??? quote "Source code"

        ```python
        owner: public(address)
        future_owner: public(address)

        @external
        def commit_transfer_ownership(_future_owner: address):
            """
            @notice Transfer ownership to `_future_owner`
            @param _future_owner The account to commit as the future owner
            """
            assert msg.sender == self.owner  # dev: only owner

            self.future_owner = _future_owner
        ```

    === "Example"

        ```shell
        >>> GaugeTypeOracle.commit_transfer_ownership('todo')
        ```


### `accept_transfer_ownership`
!!! description "`GaugeTypeOracle.accept_transfer_ownership()`"

    !!!guard "Guarded Method"
        This function is only callable by the `future_owner` of the contract.

    Function to accept the transfer ownership.

    Emits: `TransferOwnership`

    ??? quote "Source code"

        ```python
        event TransferOwnership:
            owner: indexed(address)

        owner: public(address)
        future_owner: public(address)

        @external
        def accept_transfer_ownership():
            """
            @notice Accept the transfer of ownership
            @dev Only the committed future owner can call this function
            """
            assert msg.sender == self.future_owner  # dev: only future owner

            self.owner = msg.sender
            log TransferOwnership(msg.sender)
        ```

    === "Example"

        ```shell
        >>> GaugeTypeOracle.accept_transfer_ownership()
        ```