---
layout: post
title: "[CC150v5] 8.7 Design Online Chat Server (1)"
comments: true
category: CC150v5

---

### Question 

> Explain how you would design a chat server. In particular, provide details about the various back end components, classes, and methods. 

> What would be the hardest problems to solve?

### Solution

First, decide the objects and methods. Here we'll focus on the core user management and conversation aspects.

#### Class

1. UserMgmt (business logic)
1. User (includes basic info, UserStatus, a map of conversation, a map of requests)
1. UserStatus (on/offline, status message)
1. Conversation Abstract Class (a list of user and a list of messages)
	1. PrivateChat (private conversation)
	1. GroupChat
1. Message (a string and a date/time) 
1. Request (add request and delete request, involves 2 Users)

#### Functions 

1. Sign in and log off (update availability)
1. update status message
1. add/delete request
1. send/accept/reject a request
1. create a conversation (group or private)
1. add a new message (group or private)

### Code

The most important classes is User and UserMgmt. The others are simply data containers. 

UserManager.java

	public class UserManager {
		private static UserManager instance;
		private HashMap<Integer, User> usersById = new HashMap<Integer, User>();
		private HashMap<String, User> usersByAccountName = new HashMap<String, User>();
		private HashMap<Integer, User> onlineUsers = new HashMap<Integer, User>();
		
		public static UserManager getInstance() {
			if (instance == null) {
				instance = new UserManager();
			}
			return instance;
		}
		
		public void addUser(User fromUser, String toAccountName) {
			User toUser = usersByAccountName.get(toAccountName);
			AddRequest req = new AddRequest(fromUser, toUser, new Date());
			toUser.receivedAddRequest(req);
			fromUser.sentAddRequest(req);
		}
		
		public void approveAddRequest(AddRequest req) {
			req.status = RequestStatus.Accepted;
			User from = req.getFromUser();
			User to = req.getToUser();
			from.addContact(to);
			to.addContact(from);
		}
		
		public void rejectAddRequest(AddRequest req) {
			req.status = RequestStatus.Rejected;
			User from = req.getFromUser();
			User to = req.getToUser();
			from.removeAddRequest(req);
			to.removeAddRequest(req);		
		}
		
		public void userSignedOn(String accountName) {
			User user = usersByAccountName.get(accountName);
			if (user != null) {
				user.setStatus(new UserStatus(UserStatusType.Available, ""));			
				onlineUsers.put(user.getId(), user);
			}
		}
		
		public void userSignedOff(String accountName) {
			User user = usersByAccountName.get(accountName);
			if (user != null) {
				user.setStatus(new UserStatus(UserStatusType.Offline, ""));
				onlineUsers.remove(user.getId());
			}
		}	
	}

User.java

Property: 

1. id and name
1. a map of conversations
1. a map of sent request
1. a map of received request
1. a map of friends list

Methods: 

1. sendMessageToUser(User)
1. addContact(User)
1. receivedAddRequest(Request)
1. sentAddRequest(Request)
1. removeAddRequest(Request)
1. addConversation(Conversation)

Note that all user actions are controlled by the UserManager Class. For example, when adding a friend: 

1. User A clicks "add user" on the client. 
2. User A calls requestAddUser (User B).
3. This method calls UserManager.addUser(User a, userBid).
4. UserManager calls both User A.sentAddRequest() and User B.receivedAddRequest().

Code:

	public class User {
		private int id;
		private UserStatus status = null;
		private HashMap<Integer, PrivateChat> privateChats = new HashMap<Integer, PrivateChat>();
		private ArrayList<GroupChat> groupChats = new ArrayList<GroupChat>();
		private HashMap<Integer, AddRequest> receivedAddRequests = new HashMap<Integer, AddRequest>();
		private HashMap<Integer, AddRequest> sentAddRequests = new HashMap<Integer, AddRequest>();
    
		private HashMap<Integer, User> contacts = new HashMap<Integer, User>();
		private String accountName;
		private String fullName;
		
		public User(int id, String accountName, String fullName) {
			this.accountName = accountName;
			this.fullName = fullName;
			this.id = id;
		}
		
		public boolean sendMessageToUser(User toUser, String content) {
			PrivateChat chat = privateChats.get(toUser.getId());
			if (chat == null) {
				chat = new PrivateChat(this, toUser);
				privateChats.put(toUser.getId(), chat);
			}
			Message message = new Message(content, new Date());
			return chat.addMessage(message);
		}
		
		public boolean sendMessageToGroupChat(int groupId, String content) {
			GroupChat chat = groupChats.get(groupId);
			if (chat != null) {
				Message message = new Message(content, new Date());
				return chat.addMessage(message);
			}
			return false;
		}
		
		public void setStatus(UserStatus status) {
			this.status = status;
		}
		
		public UserStatus getStatus() {
			return status;
		}
		
		public boolean addContact(User user) {
			if (contacts.containsKey(user.getId())) {
				return false;
			} else {
				contacts.put(user.getId(), user);
				return true;
			}
		}
		
		public void receivedAddRequest(AddRequest req) {
			int senderId = req.getFromUser().getId();
			if (!receivedAddRequests.containsKey(senderId)) {
				receivedAddRequests.put(senderId, req);
			}		
		}
		
		public void sentAddRequest(AddRequest req) {
			int receiverId = req.getFromUser().getId();
			if (!sentAddRequests.containsKey(receiverId)) {
				sentAddRequests.put(receiverId, req);
			}		
		}
		
		public void removeAddRequest(AddRequest req) {
			if (req.getToUser() == this) {
				receivedAddRequests.remove(req);
			} else if (req.getFromUser() == this) {
				sentAddRequests.remove(req);
			}
		}
		
		public void requestAddUser(String accountName) {
			UserManager.getInstance().addUser(this, accountName);
		}
		
		public void addConversation(PrivateChat conversation) {
			User otherUser = conversation.getOtherParticipant(this);
			privateChats.put(otherUser.getId(), conversation);
		}

		public void addConversation(GroupChat conversation) {
			groupChats.add(conversation);
		}	
		
		public int getId() {
			return id;
		}
		
		public String getAccountName() {
			return accountName;
		}
		
		public String getFullName() {
			return fullName;
		}
	}
