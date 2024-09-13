EventManager Smart Contract
Overview

The EventManager smart contract is designed to manage events in a decentralized manner using Ethereum. It allows users to create events, register for them, and sign in upon attending. The contract also integrates with ERC721 (NFT) tokens to ensure that users can only register for and attend events if they own a specific event-related NFT.
Key Features

    Event Management: Create events with different event types like Conference, Workshop, Seminar, and Hackathon.
    Registration: Users can register for events if they own a related NFT.
    Attendance Tracking: Users can sign in for events they registered for, and attendance is tracked.
    User Profiles: The contract keeps track of registered users and their event history.

Table of Contents

    Smart Contract Components
    Installation
    How to Use
    Contract Structure
    Error Handling
    Events
    Future Enhancements

Smart Contract Components
1. EventObj

Each event has the following properties:

    id: Unique event identifier.
    manager: Address of the event creator.
    eventName: Name of the event.
    eventType: Type of event (Conference, Workshop, Seminar, Hackathon).
    nftAddress: The associated NFT address that acts as a ticket.
    numberOfRegisteredPersons: How many people have registered.
    maxNumberOfRegistrations: Maximum allowed registrations.
    numberOfAttendees: Number of attendees who signed in.
    isDone: Whether the event is completed.
    hasCanceled: Whether the event was canceled.
    registeredPersons: List of addresses of registered participants.

2. User

Each user profile has the following properties:

    id: Unique identifier.
    name: Name of the user.
    registeredEventIds: Array of event IDs the user has registered for.
    attendedEventIds: Array of event IDs the user has attended.

Installation
Prerequisites

    Node.js (v14.x or higher)
    Hardhat (v2.x)
    Solidity (v0.8.24)
    OpenZeppelin Contracts

Steps

    Clone the repository:

    bash

git clone https://github.com/yourusername/EventManager.git
cd EventManager

Install dependencies:

bash

npm install

Compile the contract:

Use Hardhat to compile the Solidity contracts:

bash

npx hardhat compile

Run tests:

bash

npx hardhat test

Deploy the contract:

Update the deploy script in the scripts directory with your deployment configurations, and run:

bash

    npx hardhat run scripts/deploy.js --network yourNetwork

How to Use
1. Create an Event

To create a new event, use the createEvent function. It requires the NFT contract address, event name, event type, and the maximum number of registrations allowed.

solidity

function createEvent(
    address _nftAddress,
    string memory _eventName,
    EventType _eventType,
    uint256 _maxRegistrations
) external;

2. Register for an Event

Participants must own the event-related NFT to register. The registerForEvent function checks if the user holds the required NFT and registers them.

solidity

function registerForEvent(string memory _name, uint256 _eventId) external;

3. Sign In for the Event

After registering, participants can sign in on the event day by calling the signInForEvent function.

solidity

function signInForEvent(uint256 _eventId) external;

Contract Structure
Private/Internal Functions:

    _sanityCheck: Ensures the user or NFT address is valid.
    _zeroValueCheck: Validates that the provided value is not zero.
    _onlyEventManager: Ensures only the event manager can modify the event.

External Functions:

    createEvent: Creates a new event.
    registerForEvent: Allows users to register for an event, given they hold the required NFT.
    signInForEvent: Allows users to sign in for an event they have registered for.

Error Handling

The contract uses a custom error module imported as Errors. The following errors are defined in errors.sol:

    ZeroAddressNotAllowed: Thrown when a zero address is provided.
    ZeroValueNotAllowed: Thrown when a zero value is provided.
    NotAManager: Thrown when a non-manager tries to modify an event.
    CannotRegisterTwice: Thrown when a user tries to register for the same event more than once.
    DoesNotHaveEventNFT: Thrown when a user does not have the required NFT for registration.
    EventEndedAlready: Thrown when attempting to register or sign in for an ended event.

Events

The contract emits various events to notify external applications about the state of the contract:

    EventCreatedSuccessfully: Emitted when a new event is successfully created.
    EventSignInSuccessful: Emitted when a user signs in for an event.
    EventRegistrationSuccessful: Emitted when a user successfully registers for an event.

Future Enhancements

Potential future improvements:

    Implement a feature to update or cancel an event.
    Add dynamic pricing models for events.
    Integrate a reward system for event participants.
    Enable multi-day event tracking and attendance.

License

This project is licensed under the MIT License.

Feel free to contribute by submitting pull requests or reporting issues!

