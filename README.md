# Object-Detection
Object detection is a computer vision technique in which a software system can detect, locate, and trace the object from an image or video. YOLO (You Only Look Once) is a convolutional neural network for doing object detection. The algorithm applies a single neural network to the full image, and then divides the images into regions and predicts bounding boxes for each region. These bounding boxes are weighted by the predicted probabilities.

The most popular approach to implement YOLO is by using Darknet. For this OpenCV dnn module with a pre-trained YOLO model is used for detecting common objects. 
•	To use YOLO via OpenCV we need three files, ‘yoloV3.wieights’, ‘yoloV3.cfg’ and ‘coco.names’. First load the model using the function “cv2.dnn.readNet()”. This function loads the network into memory and automatically detects configuration and framework based on file name specified. Then we load all classes names in array using coco.names file. 
•	Next defines the output layers, from there we will be defining what object is detected by using net.getLayersNames() and net.getUnconnectedOutLayers().
•	We can’t give image directly to algorithm. So, we need to do some conversions, named blob conversion which is basically extracting features from image. We will detect objects in blob by using cv2.dnn.blobFromImage() and passing few variables: ‘img’ is the file name, scalefactor of 0.00392, size of image to be used in blob be (416,416), no mean subtraction from layers as (0,0,0), setting True flag means inverting blue with red since OpenCV uses BGR but we have channels in image as RGB. 
•	Now pass this blob to network using net.setInput(blob) and then forward this to the outputlayers. Here all objects have been detected and outs contains all the information we need to instruct to extract the position of the object like top, left, right, bottom positions, name of class.
•	Evaluate outs by showing information on screen. Mainly we will be trying to predict the confidence meaning how confident algorithm is when it predicts some object. For this, loop through outs, first get all the scores for each out in outs. Then get the class_id that has highest score amongst them and then assign confidence to value of scores by passing class_id. 
•	Assign the confidence level threshold as 0.5. Anything above 0.5 should mean object detected. Let also have the center_x, center_y,  w as width, h as height of the object detected. Here we will us height, width variables we saved previously of original image. We will also draw a circle of thickness 2 at centre of the object just for the sake of proof that object has been detected. Further draw rectangle around detected object by using center_x, center_y ,w, h. And append some information to that like class, confidence.
•	There might be a chance that multiple time the same object might be detected. This can be eliminated by using Non-Max Suppression(NMS) functionality. This will eliminate the boxes by using some threshold value and it determines that keep only the best of all boxes. And ‘indexes’ variable keeps track of such unique objects detected.
•	Using loop over all found boxes, if box is appearing in indexes then only draw rectangle, colour it, put text of class name on it.


For more information and weight files visit https://pjreddie.com/darknet/yolo/


