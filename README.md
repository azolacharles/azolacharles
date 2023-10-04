
 recipiimport sqlite3
# Function to create the database table for chat messages
def create_chat_table():
 conn = sqlite3.connect('whatsapp_chat.db')
 cursor = conn.cursor()
 
 cursor.execute('''
 CREATE TABLE IF NOT EXISTS messages (
 id INTEGER PRIMARY KEY AUTOINCREMENT,
 sender TEXT,ent TEXT,
 message TEXT
 )
 ''')
 conn.commit()
 # Function to insert a message into the database
def insert_message(sender, recipient, message):
 conn = sqlite3.connect('whatsapp_chat.db')
 cursor = conn.cursor()
 
 cursor.execute("INSERT INTO messages (sender, recipient, 
message) VALUES (?, ?, ?)", (sender, recipient, message))
 
 conn.commit()
 conn.close()
 if __name__ == "__main__":
 create_chat_table()
 user_name = input("Enter your name: ")
 friend_name = input("Enter your friend's name: ")
 print(f"Welcome to your chat with {friend_name}!\n")
 while True:
 message = input("You: ")
 insert_message(user_name, friend_name, message)
 reply = input(f"{friend_name}: ")
 insert_message(friend_name, user_name, reply)
 # Display chat history
 display_chat_history(user_name, friend_name)
