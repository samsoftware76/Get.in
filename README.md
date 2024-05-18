# Get.in
Get.in
Orbis Code Snippet:
```
contract EventCreator {
	// Define event structure
	struct Event {
		address organizer;
		string title;
		uint256 ticketPrice;
		uint256 numTickets;
	}
	
	// Mapping of events
	mapping (address => Event[]) public events;
	
	// Function to create new event
	function createEvent(string title, uint256 ticketPrice, uint256 numTickets) {
		// Create new event struct
		Event newEvent = Event(msg.sender, title, ticketPrice, numTickets);
		// Add event to mapping
		events[msg.sender].push(newEvent);
	}
	
	// Function to purchase ticket
	function buyTicket(address eventAddress, uint256 numTickets) {
		// Get event details
		Event event = events[eventAddress][0];
		// Check if tickets available
		require(event.numTickets >= numTickets, "Not enough tickets available");
		// Update ticket count
		event.numTickets -= numTickets;
		// Transfer ticket price to organizer
		payable(event.organizer).transfer(event.ticketPrice * numTickets);
	}
}
```