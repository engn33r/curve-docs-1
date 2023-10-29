https://snowtrace.io/address/0xD44eB2061362D28f741Bb3547b1a36aB13A8a582#code



### `quote`
!!! description "`Bridge.quote(_native_amount: uint256 = 0) -> uint256:`"

    Getter for the cost of calling the `bridge` method.

    Returns: cost (`uint256`).

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `_native_amount` |  `uint256` | todo |

    ??? quote "Source code"

        ```python
        @view
        @external
        def quote(_native_amount: uint256 = 0) -> uint256:
            """
            @notice Quote the cost of calling the `bridge` method
            """
            adapter_params: Bytes[86] = b""
            if _native_amount == 0:
                adapter_params = concat(
                    b"\x00\x01",
                    convert(500_000, bytes32)
                )
            else:
                adapter_params = concat(
                    b"\x00\x02",
                    convert(500_000, bytes32),
                    convert(_native_amount, bytes32),
                    b"\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00"
                )

            return Endpoint(LZ_ENDPOINT).estimateFees(
                LZ_CHAIN_ID,
                self,
                concat(empty(bytes32), empty(bytes32)),
                False,
                adapter_params
            )
        ```

    === "Example"

        ```shell
        >>> Bridge.quote(0)
        601771504190764
        ```


### `CRV20`
!!! description "`Bridge.CRV20() -> address: view`"

    Getter for the mutli-chain CRV token.

    Returns: CRV20 (`address`).

    ??? quote "Source code"

        ```python
        CRV20: public(immutable(address))

        @external
        def __init__(_delay: uint256, _limit: uint256, _lz_chain_id: uint16, _lz_endpoint: address, _crv: address, _minter: address):
            self.delay = _delay
            log SetDelay(_delay)

            self.limit = _limit
            log SetLimit(_limit)

            self.owner = msg.sender
            log TransferOwnership(msg.sender)

            LZ_CHAIN_ID = _lz_chain_id
            LZ_ADDRESS = concat(
                slice(convert(self, bytes32), 12, 20), slice(convert(self, bytes32), 12, 20)
            )
            KECCAK_LZ_ADDRESS = keccak256(LZ_ADDRESS)
            LZ_ENDPOINT = _lz_endpoint
            CRV20 = _crv
            MINTER = _minter
        ```

    === "Example"

        ```shell
        >>> Bridge.CRV20()
        '0x54d16c3e54731560940f71877568fb0b859fc05d'
        ```


### `MINTER`
!!! description "`Bridge.method_name(input: type) -> output_type: scope`"

    Getter for the minter contract.

    Returns: minter (`address`).

    ??? quote "Source code"

        ```python
        MINTER: public(immutable(address))

        @external
        def __init__(_delay: uint256, _limit: uint256, _lz_chain_id: uint16, _lz_endpoint: address, _crv: address, _minter: address):
            self.delay = _delay
            log SetDelay(_delay)

            self.limit = _limit
            log SetLimit(_limit)

            self.owner = msg.sender
            log TransferOwnership(msg.sender)

            LZ_CHAIN_ID = _lz_chain_id
            LZ_ADDRESS = concat(
                slice(convert(self, bytes32), 12, 20), slice(convert(self, bytes32), 12, 20)
            )
            KECCAK_LZ_ADDRESS = keccak256(LZ_ADDRESS)
            LZ_ENDPOINT = _lz_endpoint
            CRV20 = _crv
            MINTER = _minter
        ```

    === "Example"

        ```shell
        >>> Bridge.MINTER()
        '0x4be991edbd59ffc6bbd4ce69c90f1d8b56297f65'
        ```


### `LZ_ENDPOINT`
!!! description "`Bridge.LZ_ENDPOINT -> address: view`"

    Getter for the chain specific layer-zero endpoint.

    Returns: endpoint (`address`).

    ??? quote "Source code"

        ```python
        LZ_ENDPOINT: public(immutable(address))

        @external
        def __init__(_delay: uint256, _limit: uint256, _lz_chain_id: uint16, _lz_endpoint: address, _crv: address, _minter: address):
            self.delay = _delay
            log SetDelay(_delay)

            self.limit = _limit
            log SetLimit(_limit)

            self.owner = msg.sender
            log TransferOwnership(msg.sender)

            LZ_CHAIN_ID = _lz_chain_id
            LZ_ADDRESS = concat(
                slice(convert(self, bytes32), 12, 20), slice(convert(self, bytes32), 12, 20)
            )
            KECCAK_LZ_ADDRESS = keccak256(LZ_ADDRESS)
            LZ_ENDPOINT = _lz_endpoint
            CRV20 = _crv
            MINTER = _minter        
        ```

    === "Example"

        ```shell
        >>> Bridge.LZ_ENDPOINT()
        '0x3c2269811836af69497e5f486a85d7316753cf62'
        ```


### `LZ_CHAINID`

### `integrate_fraction`
### `issued`
### `delayed`

### `bridge`
### `lzReceive`
### `retry`
### `user_checkpoint`

### `delay`
### `set_delay`
### `limit`
### `set_limit`
### `is_killed`
### `set_killed`


### `owner`
### `future_owner`
### `commit_transfer_ownership`
### `accept_transfer_ownership`




!!! description "`Bridge.method_name(input: type) -> output_type: scope`"

    Description of the contract method. Returns: whatever contract returns.

    Returns:

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `input` |  `type` | Contract input |


    ??? quote "Source code"

        ```python
        some_python_code_here
        ```

    === "Example"

        ```shell
        >>> Bridge.
        ```
