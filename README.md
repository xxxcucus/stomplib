# stomp
StompLib is a Qt library for  clients communicating with the Stomp protocol. It includes the following functionality:

A communication frame is modelled in the class StompFrame.

In the StompFrameCreator class:
  1. Create a CONNECT frame
  2. Create a STOMP frame
  3. Create a SUBSCRIBE frame
  4. Create a MESSAGE frame
  5. Create a UNSUBSCRIBE frame
  6. Create a DISCONNECT frame

In the StompFrameParser class the parsing of STOMP text messages is implemented. The method responsible for this is called parseFromTextMessage. 
The method implements unescaping of special symbols. 

The StompClient class encapsulates a QWebSocket object that communicates with the server. 
Various methods for communicating through the web socket as well as signals and slots are implemented.

Example usage:

# Connecting to the server
m_StompClient->setUrl(server_url);
m_StompClient->connectToServer();

# Connecting through STOMP
StompFrameCreator stompFrameCreator;
auto connectFrame = stompFrameCreator.createConnectFrame("1.2", "", "", "", 10000, 10000);
m_StompClient->sendFrame(connectFrame);

# Subscribing to a topic
StompFrameCreator stompFrameCreator;
QString topicName = "/topic/myTopic";
auto subscribeFrame = stompFrameCreator.createSubscribeFrame(1, topicName, "auto");
m_StompClient->sendFrame(subscribeFrame);

# Sending text message
auto publishFrame = stompFrameCreator.createSendTextFrame("/controller/address", message);
m_StompClient->sendFrame(publishFrame);

# Unsubscribe from topic
StompFrameCreator stompFrameCreator;
auto unsubscribeFrame = stompFrameCreator.createUnsubscribeFrame(1);
m_StompClient->sendFrame(unsubscribeFrame);

# Close connection to STOMP
auto disconnectFrame = stompFrameCreator.createDisconnectFrame(1);
m_StompClient->sendFrame(disconnectFrame);

# Receiving message from server
connect(m_StompClient, &StompClient::stompMessageReceived, this, &MyClass::stompReceivedSlot);

