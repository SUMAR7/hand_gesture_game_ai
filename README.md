
## How it Works
A python application (app.py), detects the player’s hand using the TensorFlow object detection api,  and streams hand coordinates to the game interface — a web application served using FLASK — over websockets.

Hand detection is done using trained models from the [handtracking](https://github.com/victordibia/handtracking) repo. Note that hand detection is done on a frame-by-frame basis and the system does not automatically track hand across frames. However, this type of inter-frame tracking is useful as it can enable multiple user interaction where we need to track a hand across frames (think a bunch of friends waving their hands, each controlling their own paddle). To this end, the current implementation includes [naive euclidean distance](utils/object_id_utils.py) based tracking where hands seen in similar positions across frames are assigned same id.

Once each hand in the frame is detected (and a tracking id assigned), the hand coordinates are then sent to a web socket server which sends it out to connected clients.

The game web interface listens for hand detection data over a web socket. Each detected hand is used to generate a paddle, and the coordinate of the hand in the video frame is used to relatively position the paddle on the game screen.


## Installation

> The app has been tested using *Python 3*. Please use your Python 3 environment if possible.

Install requirements.

```
pip install -r requirements.txt
```

## Run  Application

```
python app.py
```

View the game interface (hand control) in your browser - `http://localhost:5005/hand` 

To view a simple mouse control version `http://localhost:5005` 

MIT License.
