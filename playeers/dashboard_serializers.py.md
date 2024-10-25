# 📄 Dashboard Serializers Documentation

Welcome to the documentation for `dashboard_serializers.py`. This file contains serializers that help in structuring and organizing data related to player lobbies and wallet transactions in a manner suitable for API responses. These serializers are used to format the data sent to the frontend, ensuring a consistent and efficient communication between the server and client.

## 🗂️ Table of Contents
- [Introduction](#introduction)
- [Classes](#classes)
  - [ListDashboardLobbiesSerializer](#listdashboardlobbiesserializer)
  - [ListWalletTransactionSerializer](#listwallettransactionserializer)
- [Fields and Methods](#fields-and-methods)
  - [Common Fields](#common-fields)
  - [Custom Methods](#custom-methods)
- [Usage](#usage)
- [Conclusion](#conclusion)

## Introduction

This file leverages Django Rest Framework's serializers to convert complex data types, such as querysets and model instances, into native Python data types that can then be easily rendered into JSON or other content types. The serializers defined in this file are specifically tailored to handle data related to game lobbies and player transactions.

## Classes

### ListDashboardLobbiesSerializer

This serializer extends the `LobbyListSerializer` and is responsible for handling the data representation of player lobbies. It includes fields that describe the lobby, including its status, rules, and player participation.

```python
class ListDashboardLobbiesSerializer(LobbyListSerializer):
    ''' List Enrolled Lobbies '''
```

**Meta Class:**
- **Model:** `Lobby`
- **Fields:** A comprehensive list of fields that describe the lobby's attributes, such as `id`, `game`, `name`, `reward`, `enrolled_players`, and more.

### ListWalletTransactionSerializer

This serializer is dedicated to handling wallet transactions. It includes detailed information about the transaction, including the involved parties, transaction date, and payment method.

```python
class ListWalletTransactionSerializer(serializers.ModelSerializer):
    ''' List Wallet Transactions Serializer '''
```

**Meta Class:**
- **Model:** `TransactionDetail`
- **Fields:** This includes transaction identifiers, participant details, financial amounts, and status indicators.

## Fields and Methods

### Common Fields

- **id:** Unique identifier for the lobby or transaction.
- **game:** Reference to the game associated with the lobby.
- **name:** Name of the lobby.
- **reward:** Reward structure for the lobby.
- **enrolled_players:** Number of players enrolled in the lobby.
- **amount:** Transaction amount.
- **current_wallet_balance:** The current balance of the wallet after the transaction.

### Custom Methods

These custom methods are used to derive or format certain fields:

- **get_payee:** Returns the payee's details including ID, name, and role.
- **get_receiver:** Provides the receiver's details in a similar format to the payee.
- **get_transaction_date:** Formats the transaction date into a standard string representation.
- **get_transaction_payment_method:** Retrieves the human-readable payment method associated with the transaction.
- **get_is_free_lobby:** Determines if a lobby or tournament is free based on specific conditions.

## Usage

These serializers are typically used within Django views or viewsets to serialize data from the database before sending it to the client. They ensure that the data is presented in a structured format, adhering to the specifications required by the frontend application.

## Conclusion

The `dashboard_serializers.py` file plays a crucial role in the data management of game lobbies and transactions. By utilizing Django Rest Framework serializers, it ensures data consistency and integrity, facilitating smooth and efficient communication between the server and the client.