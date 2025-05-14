## a. How much data will the publisher program send to the message broker in one run?

The program sends 5 messages, each containing a `UserCreatedEventMessage` struct with two fields: `user_id` (String) and `user_name` (String).  
Each message is serialized using Borsh, which is a compact binary format.

For each message:
- `user_id`: e.g., `"1"` (1 byte for the character + 4 bytes for Borsh string length = 5 bytes)
- `user_name`: e.g., `"2306256425-Amir"` (15 bytes for the string + 4 bytes for Borsh string length = 19 bytes)

Total per message: 5 bytes (`user_id`) + 19 bytes (`user_name`) = **24 bytes**

For 5 messages: 24 bytes × 5 = **120 bytes**

So, the publisher will send approximately **120 bytes** of serialized message data to the broker in one run (excluding protocol overhead).

---

## b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?

This means both the publisher and subscriber are connecting to the same AMQP message broker (such as RabbitMQ) running on `localhost` (the local machine), using the default username (`guest`) and password (`guest`), and the default AMQP port (`5672`).  
This allows the publisher to send messages to the broker, and the subscriber to receive those messages from the same broker instance.