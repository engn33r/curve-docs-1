https://snowtrace.io/address/0x4bE991EDbd59FFc6bBD4cE69C90f1d8b56297f65#code


### `ORACLE`
!!! description "`Minter.oracle() -> address: view`"

    Getter for the gauge type oracle contract.

    Returns: gauge type oracle contract (address).

    ??? quote "Source code"

        ```python
        ORACLE: public(immutable(address))

        @external
        def __init__(_oracle: address, _token: address, _type: uint256):
            ORACLE = _oracle
            TOKEN = _token
            TYPE = _type
        ```

    === "Example"

        ```shell
        >>> Minter.ORACLE()
        '0x9b7f0b68d70a741b8cb08a8e8423ccb72e630db6'
        ```


### `TOKEN`
!!! description "`Minter.TOKEN() -> address: view`"

    Getter for the CRV cross-chain token.

    Returns: crv20 (address).

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `input` |  `type` | Contract input |

    ??? quote "Source code"

        ```python
        TOKEN: public(immutable(address))

        @external
        def __init__(_oracle: address, _token: address, _type: uint256):
            ORACLE = _oracle
            TOKEN = _token
            TYPE = _type
        ```

    === "Example"

        ```shell
        >>> Minter.TOKEN()
        '0x54D16C3E54731560940F71877568Fb0b859FC05d'
        ```


### `TYPE`
!!! description "`Minter.TYPE() -> uint256: view`"

    Getter for the gauge type.

    Returns: gauge type (uint256).

    Emits:

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `input` |  `type` | Contract input |

    ??? quote "Source code"

        ```python
        TYPE: public(immutable(uint256))

        @external
        def __init__(_oracle: address, _token: address, _type: uint256):
            ORACLE = _oracle
            TOKEN = _token
            TYPE = _type
        ```

    === "Example"

        ```shell
        >>> Minter.TYPE()
        8
        ```


### `minted`
!!! description "`Minter.minted(arg0: address, arg1: address) -> uint256: view`"

    Getter method to check how many tokens were minted from gauge `arg1` for address `arg0`. 

    Returns: token amount minted (uint256).

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `arg0` |  `address` | wallet address |
    | `arg1` |  `address` | gauge address |

    ??? quote "Source code"

        ```python
        minted: public(HashMap[address, HashMap[address, uint256]])
        ```

    === "Example"

        ```shell
        >>> Minter.minted('todo')
        
        ```




### `mint`
!!! description "`Minter.mint(_gauge: address, _for: address = msg.sender):`"

    Function to mint and send all tokens from `_gauge` which belong to `_for`. 

    Emits: `Minted`

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `_gauge` |  `address` | gauge address |
    | `_for` |  `address` | wallet address; defaults to `msg.sender` |

    ??? quote "Source code"

        ```python
        event Minted:
            recipient: indexed(address)
            gauge: indexed(address)
            amount: uint256

        @external
        @nonreentrant('lock')
        def mint(_gauge: address, _for: address = msg.sender):
            """
            @notice Mint everything which belongs to `_for` and send to them
            @param _gauge `Gauge` address to get mintable amount from
            """
            self._mint_for(_gauge, _for)

        @internal
        def _mint_for(_gauge: address, _for: address):
            assert GaugeTypeOracle(ORACLE).get_gauge_type(_gauge) == TYPE  # dev: gauge is not permitted

            Gauge(_gauge).user_checkpoint(_for)
            total_mint: uint256 = Gauge(_gauge).integrate_fraction(_for)
            to_mint: uint256 = total_mint - self.minted[_for][_gauge]

            if to_mint != 0:
                MERC20(TOKEN).mint(_for, to_mint)
                self.minted[_for][_gauge] = total_mint

                log Minted(_for, _gauge, total_mint)
        ```

    === "Example"

        ```shell
        >>> Minter.mint('todo')
        ```


### `mint_many`
!!! description "`Minter.mint_many(_gauges: DynArray[address, 32], _for: address = msg.sender):`"

    Function to mint and send all tokens from a array if multiple gauges which belong to `_for`. 

    Emits: `Minted`

    | Input      | Type   | Description |
    | ----------- | -------| ----|
    | `_gauges` |  `DynArray[address, 32]` | gauge addresses |
    | `_for` |  `address` | wallet address; defaults to `msg.sender` |

    ??? quote "Source code"

        ```python
        event Minted:
            recipient: indexed(address)
            gauge: indexed(address)
            amount: uint256

        @external
        @nonreentrant('lock')
        def mint_many(_gauges: DynArray[address, 32], _for: address = msg.sender):
            """
            @notice Mint everything which belongs to `_for` across multiple gauges
            @param _gauges List of `Gauge` addresses
            """
            for gauge in _gauges:
                self._mint_for(gauge, _for)

        @internal
        def _mint_for(_gauge: address, _for: address):
            assert GaugeTypeOracle(ORACLE).get_gauge_type(_gauge) == TYPE  # dev: gauge is not permitted

            Gauge(_gauge).user_checkpoint(_for)
            total_mint: uint256 = Gauge(_gauge).integrate_fraction(_for)
            to_mint: uint256 = total_mint - self.minted[_for][_gauge]

            if to_mint != 0:
                MERC20(TOKEN).mint(_for, to_mint)
                self.minted[_for][_gauge] = total_mint

                log Minted(_for, _gauge, total_mint)
        ```

    === "Example"

        ```shell
        >>> Minter.mint_many('todo')
        ```