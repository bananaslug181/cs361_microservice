# cs361_microservice
Microservice that loads or saves a file.

# How to Request Data:

Protocol: ZeroMQ (REQ/REP)
Port: tcp://localhost:5555
Format: JSON

# How to Request to Load a File:

- Keys: action, file_name
- Action needs to be "load". file_name should be an existing file.

- Example call:

      file_data = 
      {
        "action": "load",
        "file_name": "user123_boardA.json"
      }
          import json
      import zmq
      
      context = zmq.Context()
      
      socket = context.socket(zmq.REQ)
      socket.connect("tcp://localhost:5555")
      
      for request in range(10):
          socket.send_json(file_data)
          message = socket.recv_json()


  # How to Receive a Saved File:
- Keys: action, board_id, user_id, data
- Action needs to be "save". Board_id, user_id, data can be anything.

- Example call: 

        file_data = 
        {
          "action": "save",
          "board_id": "boardA",
          "data":
          {"not-started": [
              { "id": "task1", "title": "Set up repo", "assigned_to": "Ryan" }
            ],
            "in-progress": [
              { "id": "task2", "title": "Write microservice", "assigned_to": "You" }
            ],
            "completed": [
              { "id": "task3", "title": "Design board", "assigned_to": "Teammate" }
            ]}
        }
    
        import json
        import zmq
        
        context = zmq.Context()
        
        socket = context.socket(zmq.REQ)
        socket.connect("tcp://localhost:5555")
        
        for request in range(10):
            socket.send_json(file_data)
            message = socket.recv_json()


<img width="1590" height="1152" alt="image" src="https://github.com/user-attachments/assets/44a2ddb9-fef3-461e-97ee-48a55d4f0900" />




