# RPC

openapi: 3.0.3 info: title: Pocket Network description: This is the API definition Pocket Network core RPC calls. Pocket is a distributed network that relays data requests and responses to and from any blockchain system. Pocket verifies all relayed data and proportionally rewards the participating nodes with native cryptographic tokens. termsOfService: '[https://pokt.network/terms/](https://pokt.network/terms/)' contact: email: hola@pokt.network license: name: MIT License url: '[https://github.com/pokt-network/pocket-core/LICENSE.md](https://github.com/pokt-network/pocket-core/LICENSE.md)' version: 0.6.0 externalDocs: description: Find out more about Pocket Network url: '[https://pokt.network](https://pokt.network)' servers:

* url: '[http://localhost:8081/v1](http://localhost:8081/v1)'

  tags:

* name: version

  description: Version of the Pocket API

* name: client

  description: Dispatch and relay services

* name: query description: Blockchain queries paths: /: get: tags:

  * version

    summary: Get the current version of the Pocket Network API

    responses:

    '200':

    description: Version

    content:

      text/plain:

    ```text
    schema:
      type: string
      example: 0.0.1
    ```

    /client/dispatch:

    post:

    tags:

  * client

    requestBody:

    description: Sends a dispatch request to the network and get the nodes that will be servicing your requests for the session.

    required: true

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryDispatchRequest'
    ```

    responses:

    '200':

    description: A list of dispatch/service nodes

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryDispatchResponse'
    example:
      block_height: 1
      session:
        header:
          app_public_key: f6f1f166536c55d3ad7b1b2629f0bce8a0a3dbd455d576ccb235419bcbfed7fd
          chain: '0001'
          session_height: 1
        key: pY2rZUEkygFRUZ21iT0XiyQDkifIQC74IkoQN2YvisU=
        nodes:
          - address: ebea4171cee8eff0f388e1ed97c83a73022228d0
            chains:
              - '0001'
            jailed: false
            public_key: b31b52daa582838b72d71628814e8523d5b9ea08bb0b49a438693eb5269b4635
            service_url: https://foo.bar:8080
            status: 2
            tokens: '10000000'
            unstaking_time: '0001-01-01T00:00:00Z'
          - address: 8de67229b1232b2bb77dc2c3ab247a62f47968d3
            chains:
              - '0001'
            jailed: false
            public_key: 993366e5b648b1e9f544daab0652b8fc9b3657eb9a0ee54afc53852d66b1c2d5
            service_url: https://foo.bar:8080
            status: 2
            tokens: '10000000'
            unstaking_time: '0001-01-01T00:00:00Z'
          - address: fefe600f9b257e96633245731eff6c34efbb9a50
            chains:
              - '0001'
            jailed: false
            public_key: f6f1f166536c55d3ad7b1b2629f0bce8a0a3dbd455d576ccb235419bcbfed7fd
            service_url: https://foo.bar:8080
            status: 2
            tokens: '10000000'
            unstaking_time: '0001-01-01T00:00:00Z'
          - address: fe6bff490b6dc4b2435c5c9d4960f2e79c792b1d
            chains:
              - '0001'
            jailed: false
            public_key: 5527f0f7f3d16bcec4e268a5fa8a9745f60e1497ea6745e58e2d985f2ac03875
            service_url: https://foo.bar:8080
            status: 2
            tokens: '1000000000000000000'
            unstaking_time: '0001-01-01T00:00:00Z'
          - address: b97de5e4da9bb3978b4afb76abef9e04e6b86605
            chains:
              - '0001'
            jailed: false
            public_key: f11ab260c80cc835d5258c51f6aad69008bba1fd484f8c55d21e8bc85f737a21
            service_url: https://foo.bar:8080
            status: 2
            tokens: '10000000'
            unstaking_time: '0001-01-01T00:00:00Z'
    ```

    /client/relay:

    post:

    tags:

  * client

    requestBody:

    description: Request to be relayed to a target blockchain

    required: true

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryRelayRequest'
    ```

      example:

    ```text
    payload:
      data: '"jsonrpc":"2.0","method":"web3_sha3","params":["0x68656c6c6f20776f726c64"],"id":64'
      method: ''
      path: ''
    meta:
      block_height: 5
    proof:
      request_hash: 7b227061796c6f6164223a7b2264617461223a225c226a736f6e7270635c223a5c22322e305c222c5c226d6574686f645c223a5c22776562335f736861335c222c5c22706172616d735c223a5b5c223078363836353663366336663230373736663732366336345c225d2c5c2269645c223a3634222c226d6574686f64223a22222c2270617468223a22227d2c226d657461223a7b22626c6f636b5f686569676874223a357d2c2270726f6f66223a7b22726571756573745f68617368223a22222c22656e74726f7079223a302c2273657373696f6e5f626c6f636b5f686569676874223a302c2273657276696365725f7075625f6b6579223a22222c22626c6f636b636861696e223a22222c22616174223a7b2276657273696f6e223a22222c226170705f7075625f6b6579223a22222c22636c69656e745f7075625f6b6579223a22222c227369676e6174757265223a22227d2c227369676e6174757265223a22227d7d
      entropy: 32598345349034508
      session_block_height: 1
      servicer_pub_key: 76eb9563b731af2711f326deeaebef166ce1de42c2b60c5c9f50f996fbd318ad
      blockchain: 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
      aat:
        version: 0.0.1
        app_pub_key: 81068fcc400b476a332b1dcd17943cb05ffd4a3a030c6309de9bf02d8d91cd70
        client_pub_key: 81068fcc400b476a332b1dcd17943cb05ffd4a3a030c6309de9bf02d8d91cd70
        signature: c5923bd5a663d7bb3c990504a98008e4d32ab7c57a8689d9a494fa29274b497396cbffa9523a7acf8cdff8227b96a8bb3e2e1c1b008de32041aa86c68d0f2b08
      signature: e3e3a18fee96d25d913d2c62fc32febe58400cda17958916047945252a72adf96a92557774ba051c87a9c03e554136ef23b0de1bec167050e5be099bac52590d
    ```

    responses:

    '200':

    description: Response from the relayed request

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryRelayResponse'
    example:
      Proof:
        aat:
          app_pub_key: ba7107264037ed8a310fad0f708c3dc7eb3bca8f3a680bb8b216602f10ebe265
          client_pub_key: ba7107264037ed8a310fad0f708c3dc7eb3bca8f3a680bb8b216602f10ebe265
          signature: 8282c4d78729f0b6bd1182c8e60c8af2c4fbac0ed90fbf3ea994f4f234bffd36f9f28badc17e5236f3329faa90c77672472256c45851f619173a0ed6240eca0c
          version: 0.0.1
        blockchain: 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
        entropy: 0
        request_hash: ''
        servicer_pub_key: 5ad4a47a843151e18099c9752c23f392e7e918af88ed28fa8ca2b31a6c2a7a1e
        session_block_height: 1
        signature: ''
      payload: '0x47173285a8d7341e5e972fc677286384f802f8ef42a5ec5f03bbfa254cb01fad'
      signature: e7c347971c0a53f9d63fb5681e35a4c89d97e7c6703c0e3980c2a70dbc56cb0db11e24eb078a9ffbaf7f78970ff0ce2478d7485301e39c5950c45028283ef709
    ```

    '400':

    description: Error response from the relay request \(Dispatch Is Optional\)

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryErrorRelayResponse'
    example:
      error: '{code: 400, message: "encoding/hex: odd length hex string" }'
      dispatch:
        block_height: 3
        session:
          header:
            app_public_key: e9477af9b42001280033bab76670eac4274cb7321e52280ceba964e1c61db87c
            chain: 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
            session_height: 1
          key: OmEeJO2o6xvbldJxFpqI0rRVwVtBTmRGGSlGqzxGzgk=
          nodes:
            - address: afaa802b1736396d31825f60487e4da030ea85bb
              chains:
                - 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
              jailed: false
              public_key: a01bc947f512a971131474986cc0c8cb3caed6bcfca076e6b78ac2b838ebefed
              service_url: '0.0.0.0:8081'
              status: 2
              tokens: '1000000000000000000'
              unstaking_time: '0001-01-01T00:00:00Z'
            - address: 88967bf78114d5ea56e1a02fb3fd2cac3607d674
              chains:
                - 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
              jailed: false
              public_key: c61954ba119bbbb2c1efa1d44f5f4001438566fd8aee2892387ef55ded82c159
              service_url: '0.0.0.0:8081'
              status: 2
              tokens: '10000000'
              unstaking_time: '0001-01-01T00:00:00Z'
            - address: a0c005c63f97a13e540e6bb484821d77f3fdaf75
              chains:
                - 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
              jailed: false
              public_key: db07958aa0035fbb3e7e2575fbbb062a7d5ef5580cd0fe80142a4df5d31a316a
              service_url: '0.0.0.0:8081'
              status: 2
              tokens: '10000000'
              unstaking_time: '0001-01-01T00:00:00Z'
            - address: e3b15b922be9cabbe3b4a3a788dec8dc95c8f3dc
              chains:
                - 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
              jailed: false
              public_key: a9c5d4463d5e233dd9437a2044a6595fe69ced34716a8e1c8ad86d3196f3fd78
              service_url: '0.0.0.0:8081'
              status: 2
              tokens: '10000000'
              unstaking_time: '0001-01-01T00:00:00Z'
            - address: fa11cff20c510fa1588915bd48391fee802822c8
              chains:
                - 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
              jailed: false
              public_key: b62798f50be7055073f8b2f19ca4b2262a2c82f2ab16fc907e9db1cce551ffce
              service_url: '0.0.0.0:8081'
              status: 2
              tokens: '10000000'
              unstaking_time: '0001-01-01T00:00:00Z'
    ```

  /client/sim: post: tags:

  * client

    requestBody:

    description: Request to be simulated relayed to a target blockchain

    required: true

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QuerySimRequest'
    ```

      example:

    ```text
    payload:
      data: '"jsonrpc":"2.0","method":"web3_sha3","params":["0x68656c6c6f20776f726c64"],"id":64'
      method: 'POST'
      path: ''
    relay_network_id: '0021'
    ```

    responses:

    '200':

    description: Response from the relayed request

    content:

      application/json:

    ```text
    example:
      '0x47173285a8d7341e5e972fc677286384f802f8ef42a5ec5f03bbfa254cb01fad'
    ```

    /client/rawtx:

    post:

    tags:

  * client

    requestBody:

    description: Raw transaction to be relayed to a target address

    required: true

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryRawTXRequest'
    ```

    responses:

    '200':

    description: Response from the relayed raw request

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryRawTXResponse'
    example:
      height: '0'
      txhash: 5F7D1B8AA14025F6F5E50B35CE7BC7BD6F7153FCF4840138E3CB6C1E5B5C7E78
      raw_log: '[{"msg_index":0,"success":true,"log":"","events":[{"type":"message","attributes":[{"key":"action","value":"send"}]}]}]'
      logs:
        - msg_index: 0
          success: true
          log: ''
          events:
            - type: message
              attributes:
                - key: action
                  value: send
    ```

    /client/challenge:

    post:

    tags:

  * client

    requestBody:

    description: Request a Challenge for invalid data served through relay

    required: true

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryChallengeRequest'
    ```

    responses:

    '200':

    description: Returns Challenge Response

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryChallengeResponse'
    ```

    /query/account:

    post:

    tags:

  * query

    requestBody:

    description: 'Request account at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryAddressHeight'
    ```

      example:

    ```text
    address: 4920ce1d787c60e2eaeff366c79e8aa2b82525f1
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Returns account at the specified height

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/Account'
    ```

    '400':

    description: Failed to retrieve the account

    /query/accounttxs:

    post:

    tags:

  * query

    requestBody:

    description: Returns all transactions sent by the address; Max per\_page = 1000, sort can be "asc" or \(Default\) "desc"

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryAccountTXs'
    ```

      example:

    ```text
    address: '197e4d46009879f28f978a90627c7dfeab64b4777afcc24e2b9c3d72b4dada22'
    height: 99
    page: 1
    per_page: 1000
    sort: "desc"
    ```

    required: true

    responses:

    '200':

    description: Transaction list

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryAccountTXsResponse'
    ```

    '400':

    description: Failed to retrieve the transaction information

    /query/allParams:

    post:

    tags:

  * query

    requestBody:

    description: 'Returns the parameters at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeight'
    ```

      example:

    ```text
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Parameters

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/AllParams'
    example:
      app_params:
        - param_key: application/ParticipationRateOn
          param_value: 'false'
        - param_key: application/StabilityAdjustment
          param_value: '0'
        - param_key: application/ApplicationStakeMinimum
          param_value: '1000000'
        - param_key: application/AppUnstakingTime
          param_value: '1814400000000000'
        - param_key: application/BaseRelaysPerPOKT
          param_value: '100'
        - param_key: application/MaxApplications
          param_value: '9223372036854775807'
        - param_key: application/MaximumChains
          param_value: '15'
      auth_params:
        - param_key: auth/TxSigLimit
          param_value: '7'
        - param_key: auth/MaxMemoCharacters
          param_value: '256'
        - param_key: auth/FeeMultipliers
          param_value: '{"fee_multiplier":null,"default":"1"}'
      gov_params:
        - param_key: gov/daoOwner
          param_value: 640d766bd7b712b04582a557f072b377dd489540
        - param_key: gov/acl
          param_value: '{"type":"gov/non_map_acl","value":[{"acl_key":"auth/MaxMemoCharacters","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"auth/TxSigLimit","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"gov/daoOwner","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"gov/acl","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/StakeDenom","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pocketcore/SupportedBlockchains","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/DowntimeJailDuration","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/SlashFractionDoubleSign","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/SlashFractionDowntime","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"auth/FeeMultipliers","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"application/ApplicationStakeMinimum","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pocketcore/ClaimExpiration","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pocketcore/SessionNodeCount","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pocketcore/MinimumNumberOfProofs","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pocketcore/ReplayAttackBurnMultiplier","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/MaxValidators","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/ProposerPercentage","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"application/StabilityAdjustment","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"application/AppUnstakingTime","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"application/ParticipationRateOn","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/MaxEvidenceAge","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/MinSignedPerWindow","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/StakeMinimum","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/UnstakingTime","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/RelaysToTokensMultiplier","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"application/BaseRelaysPerPOKT","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pocketcore/ClaimSubmissionWindow","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/DAOAllocation","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/SignedBlocksWindow","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/BlocksPerSession","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"application/MaxApplications","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"gov/upgrade","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"application/MaximumChains","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/MaximumChains","address":"640d766bd7b712b04582a557f072b377dd489540"},{"acl_key":"pos/MaxJailedBlocks","address":"640d766bd7b712b04582a557f072b377dd489540"}]}'
        - param_key: gov/upgrade
          param_value: '{"type":"gov/upgrade","value":{"Height":"10000","Version":"2.0.0"}}'
      node_params:
        - param_key: pos/DowntimeJailDuration
          param_value: '600000000000'
        - param_key: pos/MinSignedPerWindow
          param_value: '0.500000000000000000'
        - param_key: pos/StakeMinimum
          param_value: '1000000'
        - param_key: pos/MaximumChains
          param_value: '15'
        - param_key: pos/SignedBlocksWindow
          param_value: '100'
        - param_key: pos/DAOAllocation
          param_value: '10'
        - param_key: pos/MaxValidators
          param_value: '5000'
        - param_key: pos/BlocksPerSession
          param_value: '25'
        - param_key: pos/ProposerPercentage
          param_value: '1'
        - param_key: pos/RelaysToTokensMultiplier
          param_value: '1000'
        - param_key: pos/SlashFractionDoubleSign
          param_value: '0.050000000000000000'
        - param_key: pos/SlashFractionDowntime
          param_value: '0.010000000000000000'
        - param_key: pos/StakeDenom
          param_value: upokt
        - param_key: pos/UnstakingTime
          param_value: '1814400000000000'
        - param_key: pos/MaxEvidenceAge
          param_value: '120000000000'
        - param_key: pos/MaxJailedBlocks
          param_value: '1000'
      pocket_params:
        - param_key: pocketcore/SupportedBlockchains
          param_value: '["0001"]'
        - param_key: pocketcore/ClaimExpiration
          param_value: '100'
        - param_key: pocketcore/MinimumNumberOfProofs
          param_value: '5'
        - param_key: pocketcore/SessionNodeCount
          param_value: '5'
        - param_key: pocketcore/ClaimSubmissionWindow
          param_value: '3'
        - param_key: pocketcore/ReplayAttackBurnMultiplier
          param_value: '3'
    ```

    '400':

    description: Failed to retrieve the node information

    /query/app:

    post:

    tags:

  * query

    requestBody:

    description: 'Rquest the app at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryAddressHeight'
    ```

      example:

    ```text
    address: 4920ce1d787c60e2eaeff366c79e8aa2b82525f1
    height: 2
    ```

    required: true

    responses:

    '200':

    description: 'Returns the app at the specified height,  height = 0 is used as latest'

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/Application'
    ```

    '400':

    description: Failed to retrieve the applications

    /query/apps:

    post:

    tags:

  * query

    requestBody:

    description: 'Request a page of applications known at the specified height and staking status, empty \(""\) staking\_status returns all apps, page &lt; 1 returns the first page, per\_page &lt; 1 returns 10000 elements per page'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeightAndApplicationsOpts'
    ```

      example:

    ```text
    height: 2
    opts:
      staking_status: 2
      page: 1
      per_page: 100
    ```

    required: true

    responses:

    '200':

    description: Returns the list of all applications known at the specified height and staking status

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryAppsResponse'
    ```

    '400':

    description: Failed to retrieve the applications

    /query/balance:

    post:

    tags:

  * query

    requestBody:

    description: 'Request the balance of the specified address at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryAddressHeight'
    ```

      example:

    ```text
    address: 1b1973906ee85993e994422eddeab89f385a00a4
    height: 2
    ```

    required: true

    responses:

    '200':

    description: 'Returns the balance of the specified address at the specified height,  height = 0 is used as latest'

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryBalanceResponse'
    example:
      balance: 1000000000
    ```

    '400':

    description: Failed to retrieve Information

    /query/block:

    post:

    tags:

  * query

    requestBody:

    description: 'Returns the block structure at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryBlock'
    ```

      example:

    ```text
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Block data

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryBlockResponse'
    example:
      block:
        data:
          txs: null
        evidence:
          evidence: null
        header:
          app_hash: ''
          chain_id: pocket-test
          consensus_hash: 90B6C64F69FDCF9746F038BD2D27DFFFAE814E19EA6F974C740896AA62EDDA1D
          data_hash: ''
          evidence_hash: ''
          height: '1'
          last_block_id:
            hash: ''
            parts:
              hash: ''
              total: '0'
          last_commit_hash: ''
          last_results_hash: ''
          next_validators_hash: AC2B8D79A789E27A51E809BED90DCA8EA0E640CA134F9ADDD1B4510E8CE8C1C0
          num_txs: '0'
          proposer_address: AD8EAF52981A102068AA1FE4108E5520542078C3
          time: '2020-03-10T00:04:35.159615Z'
          total_txs: '0'
          validators_hash: AC2B8D79A789E27A51E809BED90DCA8EA0E640CA134F9ADDD1B4510E8CE8C1C0
          version:
            app: '0'
            block: '10'
        last_commit:
          block_id:
            hash: ''
            parts:
              hash: ''
              total: '0'
          precommits: null
      block_meta:
        block_id:
          hash: D0A2AB1DE2FB356AEBF4CD9B18EA6E6754323512196858557787358C279E0473
          parts:
            hash: 581F3CCD645EB60EC4F16575F1C73393C9405C76E42C6C5D14938875FE4912F5
            total: '1'
        header:
          app_hash: ''
          chain_id: pocket-test
          consensus_hash: 90B6C64F69FDCF9746F038BD2D27DFFFAE814E19EA6F974C740896AA62EDDA1D
          data_hash: ''
          evidence_hash: ''
          height: '1'
          last_block_id:
            hash: ''
            parts:
              hash: ''
              total: '0'
          last_commit_hash: ''
          last_results_hash: ''
          next_validators_hash: AC2B8D79A789E27A51E809BED90DCA8EA0E640CA134F9ADDD1B4510E8CE8C1C0
          num_txs: '0'
          proposer_address: AD8EAF52981A102068AA1FE4108E5520542078C3
          time: '2020-03-10T00:04:35.159615Z'
          total_txs: '0'
          validators_hash: AC2B8D79A789E27A51E809BED90DCA8EA0E640CA134F9ADDD1B4510E8CE8C1C0
          version:
            app: '0'
            block: '10'
    ```

    '400':

    description: Failed to retrieve the block information

    /query/blocktxs:

    post:

    tags:

  * query

    requestBody:

    description: Returns all transactions at a certain block height; Max per\_page = 1000, sort can be "asc" or \(Default\) "desc"

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryBlockTXs'
    ```

      example:

    ```text
    height: 99
    page: 1
    per_page: 1000
    sort: "desc"
    ```

    required: true

    responses:

    '200':

    description: Transaction list

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryBlockTXsResponse'
    ```

    '400':

    description: Failed to retrieve the transaction information

    /query/height:

    post:

    tags:

  * query

    requestBody:

    description: Returns the current height

    content:

    application/json:

      schema: {}

    required: false

    responses:

    '200':

    description: Block height

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryHeightResponse'
    example:
      height: 10
    ```

    '400':

    description: Failed to retrieve the block height information

    /query/param:

    post:

    tags:

  * query

    requestBody:

    description: 'Returns the parameters at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeightAndKey'
    ```

      example:

    ```text
    height: 2
    key: 'application/ParticipationRateOn'
    ```

    required: true

    responses:

    '200':

    description: Parameters

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/SingleParam'
    example:
      param_key: application/ParticipationRateOn
      param_value: 'false'
    ```

    '400':

    description: Failed to retrieve the node information

    /query/nodeclaim:

    post:

    tags:

  * query

    requestBody:

    description: Returns the node pending claim for specific session

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryNodeReceipt'
    ```

    required: true

    responses:

    '200':

    description: Node claim

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/StoredReceipt'
    ```

    /query/nodeclaims:

    post:

    tags:

  * query

    requestBody:

    description: 'Returns the list of all pending claims submitted by node address at height,  height = 0 is used as latest, address = "" will return all claims for a height'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryPaginatedHeightAndAddrParams'
    ```

      example:

    ```text
    address: '0xA5DE6D4184016708c1040c355F1c958192276DB5'
    height: 2
    page: 1
    per_page: 1
    ```

    required: true

    responses:

    '200':

    description: Node claims

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryNodeClaimsResponse'
    ```

    '400':

    description: Failed to retrieve the node proof information

    /query/node:

    post:

    tags:

  * query

    requestBody:

    description: 'Returns the node at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryAddressHeight'
    ```

      example:

    ```text
    address: '0xA5DE6D4184016708c1040c355F1c958192276DB5'
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Node details

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/Node'
    example:
      address: 05d98fbedf63cd4b4e337ef488ec2ad7e5072cb2
      chains:
        - 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
      jailed: false
      public_key: bac2790f5786d4e016ed1f03a54205ba99b949e6a3c4b4641317977dfedfce79
      service_url: '0.0.0.0:8081'
      status: 2
      tokens: '1000000000000000'
      unstaking_time: '0001-01-01T00:00:00Z'
    ```

    '400':

    description: Failed to retrieve the node information

    /query/nodes:

    post:

    tags:

  * query

    requestBody:

    description: 'Request a page of nodes known at the specified height and with options, empty options returns all validators, page &lt; 1 returns the first page, per\_page &lt; 1 returns 10000 elements per page'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeightAndValidatorsOpts'
    ```

      example:

    ```text
    opts:
      staking_status: 0x02
      page: 1
      per_page: 100
      chain: ""
      JailedStatus: 1
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Returns the list of all nodes known at the specified height and staking status

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryNodesResponse'
    example:
      result:
        - address: 98a18a38aa6826a55dccce19f607e3171cf1436e
          public_key: d6b3785f00961059d2a5c6448cae7ddb02475de79c22261687a92cb905ff0de9
          jailed: false
          status: 2
          tokens: '1000000000000000'
          service_url: '0.0.0.0:8081'
          chains:
            - 36f028580bb02cc8272a9a020f4200e346e276ae664e45ee80745574e2f5ab80
          unstaking_time: '0001-01-01T00:00:00Z'
      page: 1
      total_pages: 100
    ```

    '400':

    description: Failed to retrieve the nodes' information

    /query/supply:

    post:

    tags:

  * query

    requestBody:

    description: 'Returns the list of node params specified in the height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeight'
    ```

      example:

    ```text
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Pocket Network parameters

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QuerySupplyResponse'
    ```

    '400':

    description: Failed to retrieve the supply information

    /query/supportedchains:

    post:

    tags:

  * query

    requestBody:

    description: 'Returns the list Network Identifiers supported by the network at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeight'
    ```

      example:

    ```text
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Pocket Network parameters

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QuerySupportedChainsResponse'
    ```

    '400':

    description: Failed to retrieve the application information

    /query/state:

    post:

    tags:

  * query

    requestBody:

    description: Returns the transaction by the hash

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeight'
    ```

      example:

    ```text
    height: '2'
    ```

    required: true

    responses:

    '200':

    description: Transaction data

    content:

      application/json:

    ```text
    example:
      app_hash: ''
      app_state:
        application:
          applications: [ ]
          exported: true
          params:
            app_stake_minimum: '1000000'
            base_relays_per_pokt: '167'
            max_applications: '9223372036854775807'
            maximum_chains: '15'
            participation_rate_on: false
            stability_adjustment: '0'
            unstaking_time: '1814000000000000'
        auth:
          accounts:
            - type: posmint/Account
              value:
                address: '009c0b262c6150d7dca0304acc0abc59d8086b0d'
                coins:
                  - amount: '0'
                    denom: upokt
                public_key:
                  type: crypto/ed25519_public_key
                  value: 5760934260f6893935a568eae97de00b21dfe539f9aa3b7d1de9d8824352a8f5
          params:
            fee_multipliers:
              default: '1'
              fee_multiplier:
            max_memo_characters: '75'
            tx_sig_limit: '8'
          supply:
            - amount: '650000000150000'
              denom: upokt
        gov:
          DAO_Tokens: '50000000000000'
          params:
            acl:
              - acl_key: application/ApplicationStakeMinimum
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: application/AppUnstakingTime
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: application/BaseRelaysPerPOKT
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: application/MaxApplications
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: application/MaximumChains
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: application/ParticipationRateOn
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: application/StabilityAdjustment
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: auth/MaxMemoCharacters
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: auth/TxSigLimit
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: gov/acl
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: gov/daoOwner
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: gov/upgrade
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pocketcore/ClaimExpiration
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: auth/FeeMultipliers
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pocketcore/ReplayAttackBurnMultiplier
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/ProposerPercentage
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pocketcore/ClaimSubmissionWindow
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pocketcore/MinimumNumberOfProofs
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pocketcore/SessionNodeCount
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pocketcore/SupportedBlockchains
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/BlocksPerSession
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/DAOAllocation
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/DowntimeJailDuration
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/MaxEvidenceAge
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/MaximumChains
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/MaxJailedBlocks
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/MaxValidators
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/MinSignedPerWindow
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/RelaysToTokensMultiplier
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/SignedBlocksWindow
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/SlashFractionDoubleSign
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/SlashFractionDowntime
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/StakeDenom
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/StakeMinimum
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
              - acl_key: pos/UnstakingTime
                address: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
            dao_owner: a83172b67b5ffbfcb8acb95acc0fd0466a9d4bc4
            upgrade:
              Height: '0'
              Version: '0'
        pocketcore:
          claims:
          params:
            claim_expiration: '120'
            minimum_number_of_proofs: '10'
            proof_waiting_period: '3'
            replay_attack_burn_multiplier: '3'
            session_node_count: '5'
            supported_blockchains:
              - '0001'
              - '0021'
        pos:
          exported: true
          missed_blocks: { }
          params:
            dao_allocation: '10'
            downtime_jail_duration: '3600000000000'
            max_evidence_age: '120000000000'
            max_jailed_blocks: '37960'
            max_validators: '5000'
            maximum_chains: '15'
            min_signed_per_window: '6.000000000000000000'
            proposer_allocation: '1'
            relays_to_tokens_multiplier: '0'
            session_block_frequency: '4'
            signed_blocks_window: '10'
            slash_fraction_double_sign: '0.050000000000000000'
            slash_fraction_downtime: '0.000001000000000000'
            stake_denom: upokt
            stake_minimum: '15000000000'
            unstaking_time: '1814000000000000'
          prevState_total_power: '76084066'
          prevState_validator_powers:
            - Address: 40c8973967b8d6b1123029819cad20fd44580e9e
              Power: '7641951'
            - Address: 5bcae50364952a5fa3a8363f93f2adffc9eff42e
              Power: '7641951'
            - Address: 8afc6b4195e3fd59fa3aa8bab65b2b7c497cedf9
              Power: '7641951'
            - Address: 8dd722c42425783b50db707995f841b3c7ccc827
              Power: '7641951'
            - Address: 913fed2298bc8af74989bc56d94e2e4ca95a6519
              Power: '7641951'
            - Address: a8943929b30cbc3e7a30c2de06b385bcf874134b
              Power: '7641951'
            - Address: c6dfe12a4ff2bc2b44c83c791853b6edb6c5eb58
              Power: '7641951'
            - Address: d46556719200aee73fc7446731ae58496978548d
              Power: '7641951'
            - Address: e09ce22e0abfd8129776128c0c9b3836024d8c6e
              Power: '7641951'
            - Address: e74727d0ba34d9f7f6f583cb4a87dbe91d692c5f
              Power: '7306507'
          previous_proposer: 913fed2298bc8af74989bc56d94e2e4ca95a6519
          signing_infos:
            '009c0b262c6150d7dca0304acc0abc59d8086b0d':
              address: '009c0b262c6150d7dca0304acc0abc59d8086b0d'
              index_offset: '0'
              jailed_blocks_counter: '2'
              jailed_until: '1970-01-01T00:00:00Z'
              missed_blocks_counter: '0'
              start_height: '0'
            016b81f94f552ecdc1ab9da437ae06686fca3674:
              address: 016b81f94f552ecdc1ab9da437ae06686fca3674
              index_offset: '0'
              jailed_blocks_counter: '2'
              jailed_until: '1970-01-01T00:00:00Z'
              missed_blocks_counter: '0'
              start_height: '0'
            01f1f9010e52c71b567f4759700df164b6074b04:
              address: 01f1f9010e52c71b567f4759700df164b6074b04
              index_offset: '0'
              jailed_blocks_counter: '2'
              jailed_until: '1970-01-01T00:00:00Z'
              missed_blocks_counter: '0'
              start_height: '0'
          validators:
            - address: '009c0b262c6150d7dca0304acc0abc59d8086b0d'
              chains:
                - '0001'
                - '0021'
              jailed: true
              public_key: 5760934260f6893935a568eae97de00b21dfe539f9aa3b7d1de9d8824352a8f5
              service_url: https://1.pockettuzem.com:443
              status: 2
              tokens: '17500000000'
              unstaking_time: '2020-11-10T00:00:00Z'
            - address: 016b81f94f552ecdc1ab9da437ae06686fca3674
              chains:
                - '0001'
                - '0021'
              jailed: true
              public_key: 4c51be986b3b81b00935a10fabcfcf78bc7068885e89f0ede96cfa3d98262ce7
              service_url: https://pocketnode2.lamref.cf:443
              status: 2
              tokens: '17500000000'
              unstaking_time: '2020-11-10T00:00:00Z'
            - address: 01f1f9010e52c71b567f4759700df164b6074b04
              chains:
                - '0001'
                - '0021'
              jailed: true
              public_key: 9acb7cb34b06e9573471f65191e507909c7b0a49b5296463c1c5be8faf747c90
              service_url: https://node2.protofire.io:443
              status: 2
              tokens: '15005000000'
              unstaking_time: '2020-11-10T00:00:00Z'
            - address: 03655eabc3a7337daa303576aa9bbe726f2320c8
              chains:
                - '0001'
                - '0021'
              jailed: true
              public_key: 5ab705112162d3b19d57e967e2eac03491914abc6cb11a00275242e8874580c7
              service_url: https://node2.musicabaile.com:443
              status: 2
              tokens: '208219000000'
              unstaking_time: '2021-05-15T00:00:00Z'
            - address: '04493410acf1e28ce254c36de8187fa29a4917c0'
              chains:
                - '0001'
                - '0021'
              jailed: true
              public_key: 3a6ae53636b3ec5708fbc41ffe8ec2fd952d9b9d5ef9ee22a325486dd08a7306
              service_url: https://node1.noderunnerpkt.xyz:443
              status: 2
              tokens: '15723270000'
              unstaking_time: '2020-11-10T00:00:00Z'
            - address: fe2006c9b958937923b31868ed265f4fa061cf9a
              chains:
                - '0001'
                - '0021'
              jailed: true
              public_key: 301c25510103bddbd9b213a1d54e52c8ba826ca066882efd831034bee586c1e8
              service_url: https://nodo1.misnodos.company:443
              status: 2
              tokens: '510000000000'
              unstaking_time: '2021-05-15T00:00:00Z'
      chain_id: "<Input New ChainID>"
      consensus_params:
        block:
          max_bytes: '4000000'
          max_gas: "-1"
          time_iota_ms: '1'
        evidence:
          max_age: '1000000'
        validator:
          pub_key_types:
            - ed25519
      genesis_time: '0001-01-01T00:00:00Z'
    ```

    '400':

    description: Failed to retrieve the transaction information

    /query/tx:

    post:

    tags:

  * query

    requestBody:

    description: Returns the transaction by the hash

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryTX'
    ```

      example:

    ```text
    hash: '0x197e4d46009879f28f978a90627c7dfeab64b4777afcc24e2b9c3d72b4dada22'
    prove: false
    ```

    required: true

    responses:

    '200':

    description: Transaction data

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/QueryTXResponse'
    ```

    '400':

    description: Failed to retrieve the transaction information

    /query/upgrade:

    post:

    tags:

  * query

    requestBody:

    description: 'Returns upgrade information specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeight'
    ```

      example:

    ```text
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Upgrade Response Information

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/UpgradeResponse'
    ```

    '400':

    description: Failed to retrieve the supply information

    /query/pocketparams:

    post:

    deprecated: true

    tags:

  * query

    requestBody:

    description: 'Returns the pocket parameters at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeight'
    ```

      example:

    ```text
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Pocket Network parameters

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/PocketParams'
    ```

    '400':

    description: Failed to retrieve the application information

    /query/nodeparams:

    post:

    deprecated: true

    tags:

  * query

    requestBody:

    description: 'Returns the node parameters at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeight'
    ```

      example:

    ```text
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Node parameters

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/NodeParams'
    ```

    '400':

    description: Failed to retrieve the node information

    /query/appparams:

    post:

    deprecated: true

    tags:

  * query

    requestBody:

    description: 'Returns the app parameters at the specified height,  height = 0 is used as latest'

    content:

    application/json:

      schema:

    ```text
    $ref: '#/components/schemas/QueryHeight'
    ```

      example:

    ```text
    height: 2
    ```

    required: true

    responses:

    '200':

    description: Application parameters

    content:

      application/json:

    ```text
    schema:
      $ref: '#/components/schemas/ApplicationParams'
    ```

    '400':

    description: Failed to retrieve the application information

    /private/stop:

    post:

    tags:

  * private

    parameters:

  * in: query

    name: authtoken

    schema:

      type: string

    description: Current Authorization Token from pocket core.

    responses:

    '200':

    description: Succesfull Stop

    content:

      text/plain:

    ```text
    schema:
      type: string
      example: ""
    ```

    '401':

    description: Wrong Authtoken

    content:

      application/json:

    ```text
    schema:
      type: object
      properties:
        code:
          type: integer
          description: The error code.
        message:
          type: string
          description: The error msg.
    ```

    components:

    schemas:

    ABCIEvent:

    type: object

    properties:

    type:

    type: string

    attributes:

    type: array

    items:

      type: object

      properties:

    ```text
    key:
      type: string
    value:
      type: string
    ```

    ABCIMessageLog:

    type: object

    properties:

    msg\_index:

    type: integer

    format: uint16

    description: Ordered index of the log message

    success:

    type: boolean

    description: Success or failure?

    log:

    type: string

    description: Full text of the log

    events:

    type: array

    items:

      $ref: '\#/components/schemas/ABCIEvent'

    Account:

    type: object

    properties:

    address:

    type: string

    coins:

    type: array

    items:

      $ref: '\#/components/schemas/Coin'

    public\_key:

    type: string

    Coin:

    type: object

    properties:

    amount:

    type: string

    denom:

    type: string

    Application:

    type: object

    properties:

    address:

    type: string

    description: The hex address of the application

    public\_key:

    type: string

    description: The hex public key of the application

    jailed:

    type: boolean

    description: Has the application been jailed from staked status

    default: false

    status:

    type: integer

    description: Application status

    chains:

    type: array

    items:

      type: string

    description: Blockchains supported

    tokens:

    type: string

    description: How many tokens has this node staked in uPOKT

    max\_relays:

    type: integer

    format: int64

    description: Maximum number of relays supported

    unstaking\_time:

    type: string

    description: 'If unstaking, the minimum time for the validator to complete unstaking'

    ApplicationParams:

    type: object

    properties:

    unstaking\_time:

    type: string

    description: duration of unstaking

    max\_applications:

    type: integer

    format: uint64

    description: maximum number of applications

    app\_stake\_minimum:

    type: integer

    format: int64

    description: minimum amount needed to stake as an application

    base\_relays\_per\_pokt:

    type: integer

    format: int64

    description: base relays per POKT coin staked

    stability\_adjustment:

    type: integer

    format: int64

    description: the stability adjustment from the governance

    participation\_rate\_on:

    type: boolean

    description: the participation rate affects the amount minted based on staked ratio

    Applications:

    type: array

    items:

    $ref: '\#/components/schemas/Application'

    Block:

    type: object

    properties:

    header:

    $ref: '\#/components/schemas/BlockHeader'

    data:

    type: string

    description: Data hash of the block

    evidence:

    type: string

    description: Evidence hash

    lastCommit:

    $ref: '\#/components/schemas/Commit'

    Blockchain:

    type: object

    properties:

    name:

    type: string

    description: Name of the blockchain

    net\_id:

    type: string

    description: Network identifier

    BlockHeader:

    type: object

    properties:

    version:

    $ref: '\#/components/schemas/Consensus'

    chain\_id:

    type: string

    height:

    type: integer

    format: int64

    time:

    type: string

    num\_txs:

    type: integer

    format: int64

    total\_txs:

    type: integer

    format: int64

    last\_block\_id:

    $ref: '\#/components/schemas/BlockID'

    last\_commit\_hash:

    type: string

    data\_hash:

    type: string

    validators\_hash:

    type: string

    next\_validators\_hash:

    type: string

    consensus\_hash:

    type: string

    app\_hash:

    type: string

    last\_results\_hash:

    type: string

    evidence\_hash:

    type: string

    proposer\_address:

    type: string

    BlockID:

    type: object

    properties:

    hash:

    type: string

    parts:

    $ref: '\#/components/schemas/PartSetHeader'

    BlockMeta:

    type: object

    properties:

    block\_id:

    $ref: '\#/components/schemas/BlockID'

    blockHeader:

    $ref: '\#/components/schemas/BlockHeader'

    Commit:

    type: object

    properties:

    block\_id:

    $ref: '\#/components/schemas/BlockID'

    commit\_signature:

    $ref: '\#/components/schemas/CommitSignature'

    CommitSignature:

    type: object

    properties:

    type:

    type: string

    height:

    type: integer

    format: int64

    round:

    type: integer

    block\_id:

    $ref: '\#/components/schemas/BlockID'

    timestamp:

    type: string

    validator\_address:

    type: string

    validator\_index:

    type: integer

    format: int32

    signature:

    type: string

    Consensus:

    type: object

    properties:

    block:

    type: integer

    format: int64

    app:

    type: integer

    format: int64

    Node:

    type: object

    properties:

    address:

    type: string

    description: The hex address of the validator

    chains:

    type: array

    items:

      type: string

    description: Blockchains supported

    jailed:

    type: boolean

    description: Has the validator been jailed from staked status

    default: false

    public\_key:

    type: string

    description: The validator public hex key

    service\_url:

    type: string

    description: The validator service url

    status:

    type: integer

    description: Validator status

    tokens:

    type: string

    description: How many tokens has this node staked in uPOKT

    unstaking\_time:

    type: string

    description: 'If unstaking, the minimum time for the validator to complete unstaking'

    AllParams:

    type: object

    properties:

    app\_params:

    type: array

    items:

      $ref: '\#/components/schemas/SingleParam'

      description: the APP module params

    node\_params:

    type: array

    items:

      $ref: '\#/components/schemas/SingleParam'

      description: the POS module params

    pocket\_params:

    type: array

    items:

      $ref: '\#/components/schemas/SingleParam'

      description: the Pocket params

    gov\_params:

    type: array

    items:

      $ref: '\#/components/schemas/SingleParam'

      description: the GOV module params

    auth\_params:

    type: array

    items:

      $ref: '\#/components/schemas/SingleParam'

      description: the Auth module params

    SingleParam:

    type: object

    properties:

    param\_key:

    type: string

    param\_value:

    type: string

    NodeParams:

    type: object

    properties:

    unstaking\_time:

    type: string

    format: date-time

    description: How much time must pass between the begin\_unstaking\_tx and the node transitioning to unstaked status

    max\_validators:

    type: integer

    format: int64

    description: Maximum number of validators in the network at any given block

    stake\_denom:

    type: string

    description: The monetary denomination of the coins in the network `uPOKT`

    stake\_minimum:

    type: integer

    format: int64

    description: Minimum amount of uPOKT needed to stake in the network as a node

    session\_block\_frequency:

    type: integer

    format: int64

    description: How many blocks are in a session

    dao\_allocation:

    type: integer

    format: int64

    description: Award percentage of the mint for the DAO

    proposer\_allocation:

    type: integer

    format: int32

    description: Award percentage of the mint for the proposer

    max\_evidence\_age:

    type: string

    description: Maximum age of tendermint evidence that is still valid \(currently not implemented in Cosmos or Pocket-Core\)

    signed\_blocks\_window:

    type: integer

    format: int64

    description: Window of time in blocks \(unit\) used for signature verification -&gt; specifically in not signing \(missing\) blocks

    min\_signed\_per\_window:

    type: integer

    format: int64

    description: Minimum number of blocks the node must sign per window

    downtime\_jail\_duration:

    type: integer

    format: int64

    description: Minimum amount of time node must spend in jail after missing blocks

    slash\_fraction\_double\_sign:

    type: integer

    format: int64

    description: The factor of which a node is slashed for a double sign

    slash\_fraction\_downtime:

    type: integer

    format: int64

    description: The factor of which a node is slashed for a double sign

    PartSetHeader:

    type: object

    properties:

    total:

    type: integer

    format: int64

    hash:

    type: string

    PocketParams:

    type: object

    properties:

    session\_node\_count:

    type: integer

    format: int64

    description: Number of nodes in this session

    proof\_waiting\_period:

    type: integer

    format: int64

    description: Proof waiting period

    supported\_blockchains:

    type: array

    description: Supported blockchains

    items:

      type: string

    claim\_expiration:

    type: integer

    format: int64

    description: Claim expiration

    RelayProof:

    type: object

    properties:

    request\_hash:

    type: string

    description: request hash identifier

    entropy:

    type: integer

    format: int64

    description: Entropy value to add uniqueness

    session\_block\_height:

    type: integer

    format: int64

    description: Height of the session

    servicer\_pub\_key:

    type: string

    description: Servicer public hex public key

    blockchain:

    type: string

    description: Blockchain hex string

    aat:

    $ref: '\#/components/schemas/AAT'

    signature:

    type: string

    description: client's signature in hex

    AAT:

    type: object

    properties:

    version:

    type: string

    app\_pub\_key:

    type: string

    description: Application hex public key

    client\_pub\_key:

    type: string

    description: Application hex public key associated with a client

    signature:

    type: string

    description: Application's signature in hex

    RelayHeader:

    type: object

    additionalProperties:

    type: string

    RelayMetadata:

    description: metadata for the relay request

    type: object

    properties:

    block\_height:

    type: integer

    format: int64

    RelayPayload:

    description: the data payload of the request

    type: object

    properties:

    data:

    type: string

    description: The actual data of the request string for the external chain

    method:

    type: string

    description: The HTTP CRUD method

    path:

    type: string

    description: The REST path

    headers:

    $ref: '\#/components/schemas/RelayHeader'

    SessionHeader:

    type: object

    properties:

    app\_public\_key:

    type: string

    description: Application hex public key associated with a client

    chain:

    type: string

    description: Network Identified in hex

    session\_height:

    type: integer

    format: int64

    description: Height of the session

    SimpleProof:

    type: object

    properties:

    total:

    type: integer

    format: int64

    index:

    type: integer

    format: int64

    leaf\_hash:

    type: string

    aunts:

    type: array

    items:

      type: string

    StoredReceipt:

    type: object

    properties:

    session\_header:

    $ref: '\#/components/schemas/SessionHeader'

    servicer\_address:

    type: string

    total\_relays:

    type: integer

    format: int64

    evidence\_type:

    type: integer

    format: int64

    MsgClaim:

    type: object

    properties:

    expiration\_height:

    type: integer

    format: int64

    description: height when the claim expires

    evidence\_type:

    type: integer

    format: int64

    description: Arbitrary Enum

    from\_address:

    type: string

    format: hex bytes

    total\_proofs:

    type: integer

    session\_header:

    $ref: '\#/components/schemas/SessionHeader'

    merkle\_root:

    $ref: '\#/components/schemas/HashSum'

    HashSum:

    type: object

    properties:

    hash:

    type: string

    description: byte array

    sum:

    type: integer

    description: uint64

    Transaction:

    type: object

    properties:

    hash:

    type: string

    description: Hash of the transaction

    height:

    type: integer

    format: int64

    description: Blockheight of the transaction

    index:

    type: integer

    format: int64

    tx\_result:

    $ref: '\#/components/schemas/TxResult'

    tx:

    type: string

    description: Raw data of the transaction

    proof:

    $ref: '\#/components/schemas/TXProof'

    stdTx:

    $ref:  '\#/components/schemas/StdTx'

    StdTx:

    type: object

    properties:

    entropy:

    type: integer

    fee:

    $ref: '\#/components/schemas/Coin'

    memo:

    type: string

    msg:

    type: object

    signature:

    type: object

    properties:

      pub\_key:

    ```text
    type: string
    ```

      signature:

    ```text
    type: string
    ```

    TxResult:

    type: object

    properties:

    code:

    type: integer

    format: int32

    data:

    type: string

    log:

    type: string

    info:

    type: string

    events:

    type: array

    items:

      type: string

    codespace:

    type: string

    signer:

    type: string

    recipient:

    type: string

    description: The receiver of the transaction, will be null if no receiver

    message\_type:

    type: string

    description: The type of the transaction, can be "app\_stake", "app\_begin\_unstake", "stake\_validator", "begin\_unstake\_validator", "unjail\_validator", "send", "upgrade", "change\_param", "dao\_tranfer", "claim", or "proof"

    TXProof:

    type: object

    description: Proof of the transaction

    properties:

    root\_hash:

    type: string

    data:

    type: string

    proof:

    $ref: '\#/components/schemas/SimpleProof'

    QueryAddressHeight:

    type: object

    properties:

    height:

    type: integer

    format: int64

    address:

    type: string

    QueryBalanceResponse:

    type: object

    properties:

    balance:

    type: integer

    format: int64

    QueryBlock:

    type: object

    properties:

    height:

    type: integer

    format: int64

    QueryBlockResponse:

    type: object

    properties:

    block:

    $ref: '\#/components/schemas/Block'

    block\_meta:

    $ref: '\#/components/schemas/BlockMeta'

    QueryDispatchRequest:

    $ref: '\#/components/schemas/SessionHeader'

    QueryDispatchResponse:

    type: object

    properties:

    session:

    $ref: '\#/components/schemas/Session'

    block\_height:

    type: integer

    format: int64

    Session:

    type: object

    properties:

    header:

    $ref: '\#/components/schemas/SessionHeader'

    key:

    type: string

    format: byte

    nodes:

    type: array

    items:

      $ref: '\#/components/schemas/Node'

    QueryHeightAndKey:

    type: object

    properties:

    height:

    type: integer

    format: int64

    key:

    type: string

    QueryHeight:

    type: object

    properties:

    height:

    type: integer

    format: int64

    QueryHeightResponse:

    type: object

    properties:

    height:

    type: integer

    format: int64

    QueryNodeReceipt:

    type: object

    properties:

    address:

    type: string

    description: Node address

    blockchain:

    type: string

    app\_pubkey:

    type: string

    description: Application hex public key associated with a client

    session\_block\_height:

    type: integer

    format: int64

    description: Session block height

    height:

    type: integer

    format: int64

    description: Height of the session

    QueryNodeReceiptsResponse:

    type: object

    properties:

    result:

    type: array

    items:

      $ref: '\#/components/schemas/StoredReceipt'

    page:

    type: integer

    format: int64

    description: current page

    total\_pages:

    type: integer

    format: int64

    description: maximum amount of pages

    QueryNodeClaimsResponse:

    type: object

    properties:

    result:

    type: array

    items:

      $ref: '\#/components/schemas/MsgClaim'

    page:

    type: integer

    format: int64

    description: current page

    total\_pages:

    type: integer

    format: int64

    description: maximum amount of pages

    QueryNodesResponse:

    type: object

    properties:

    result:

    type: array

    items:

      $ref: '\#/components/schemas/Node'

    page:

    type: integer

    format: int64

    description: current page

    total\_pages:

    type: integer

    format: int64

    description: maximum amount of pages

    QueryAppsResponse:

    type: object

    properties:

    result:

    type: array

    items:

      $ref: '\#/components/schemas/Application'

    page:

    type: integer

    format: int64

    description: current page

    total\_pages:

    type: integer

    format: int64

    description: maximum amount of pages

    QueryRawTXRequest:

    type: object

    properties:

    address:

    type: string

    raw\_hex\_bytes:

    type: string

    QueryRawTXResponse:

    type: object

    properties:

    height:

    type: integer

    format: int64

    description: Blockheight of the transaction

    txhash:

    type: string

    description: Hash of the transaction

    code:

    type: integer

    format: uint32

    description: Result code returned \(0 is OK; everything else is error\)

    data:

    type: string

    description: Raw transaction data

    raw\_log:

    type: string

    description: Raw transaction log

    logs:

    type: array

    items:

      $ref: '\#/components/schemas/ABCIMessageLog'

    description: ABCI Tendermint Logs

    info:

    type: string

    gas\_wanted:

    type: integer

    format: int64

    gas\_used:

    type: integer

    format: int64

    codespace:

    type: string

    timestamp:

    type: string

    description: Timestamp of the transaction

    QueryRelayRequest:

    type: object

    properties:

    payload:

    $ref: '\#/components/schemas/RelayPayload'

    meta:

    $ref: '\#/components/schemas/RelayMetadata'

    proof:

    $ref: '\#/components/schemas/RelayProof'

    QuerySimRequest:

    type: object

    properties:

    payload:

    $ref: '\#/components/schemas/RelayPayload'

    relay\_network\_id:

    type: string

    meta:

    $ref: '\#/components/schemas/RelayMetadata'

    proof:

    $ref: '\#/components/schemas/RelayProof'

    QueryRelayResponse:

    type: object

    properties:

    signature:

    type: string

    description: Signature from the node in hex

    payload:

    type: string

    description: string response to relay

    QueryErrorRelayResponse:

    type: object

    properties:

    error:

    type: string

    description: Amino JSON Error String

    dispatch:

    $ref: '\#/components/schemas/QueryDispatchResponse'

    QueryChallengeRequest:

    type: object

    properties:

    majority\_responses:

    type: array

    items:

      $ref: '\#/components/schemas/QueryRelayResponse'

    minItems: 1

    maxItems: 2

    minority\_response:

    $ref: '\#/components/schemas/QueryRelayResponse'

    address:

    description: reporter address

    type: string

    format: byte

    QueryChallengeResponse:

    type: object

    properties:

    response:

    type: string

    QueryHeightAndValidatorsOpts:

    type: object

    properties:

    height:

    type: integer

    format: int64

    page:

    type: integer

    format: int64

    per\_page:

    type: integer

    format: int64

    staking\_status:

    type: integer

    enum:

    * 1 // unstaking
    * 2 // staked

      jailed\_status:

      type: integer

      enum:

    * 1 // jailed
    * 2 // unjailed

      blockchain:

      type: string

      QueryHeightAndApplicationsOpts:

      type: object

      properties:

      height:

      type: integer

      format: int64

      page:

      type: integer

      format: int64

      per\_page:

      type: integer

      format: int64

      staking\_status:

      type: integer

      enum:

    * 1 // unstaking
    * 2 // staked

      blockchain:

      type: string

      QuerySupplyResponse:

      type: object

      properties:

      node\_staked:

      type: integer

      format: int64

      description: Amount staked by the node in uPOKT

      app\_staked:

      type: integer

      format: int64

      description: Amount staked by the app in uPOKT

      dao:

      type: integer

      format: int64

      description: DAO amount in uPOKT

      total\_staked:

      type: integer

      format: int64

      description: Total amount staked in uPOKT

      total\_unstaked:

      type: integer

      format: int64

      description: Total amount unstaked in uPOKT

      total:

      type: integer

      format: int64

      description: Total amount in uPOKT

      QuerySupportedChainsResponse:

      type: object

      properties:

      supported\_chains:

      type: array

      description: Supported blockchains

      items:

      type: string

      QueryTX:

      type: object

      properties:

      hash:

      type: string

      prove:

      type: boolean

      QueryTXResponse:

      type: object

      properties:

      transaction:

      $ref: '\#/components/schemas/Transaction'

      QueryPaginatedHeightAndAddrParams:

      type: object

      properties:

      height:

      type: integer

      format: int64

      address:

      type: string

      page:

      type: integer

      format: int64

      per\_page:

      type: integer

      format: int64

      QueryAccountTXs:

      type: object

      properties:

      address:

      type: string

      page:

      type: integer

      per\_page:

      type: integer

      prove:

      type: boolean

      received:

      type: boolean

      order:

      type: string

      required:

  * address

    QueryAccountTXsResponse:

    type: object

    properties:

    txs:

    type: array

    items:

      $ref: '\#/components/schemas/Transaction'

    total\_count:

    type: string

    QueryBlockTXs:

    type: object

    properties:

    height:

    type: integer

    page:

    type: integer

    per\_page:

    type: integer

    prove:

    type: boolean

    order:

    type: string

    required:

  * height

    QueryBlockTXsResponse:

    type: object

    properties:

    txs:

    type: array

    items:

      $ref: '\#/components/schemas/Transaction'

    total\_count:

    type: string

    UpgradeResponse:

    type: object

    properties:

    Height:

    type: string

    Version:

    type: string
