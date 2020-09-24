# Getting-Started-with-ml5.js
By Chloe Kim and Sarah Zaheer


### Adding a print statement to display the data to look at the object hierarchy in the console of ObjectDetector sketch.

```

let video;
let detector;
let detections;

function setup() {
    createCanvas(480, 360);
    
    video = createCapture(VIDEO);
    video.size(width, height);
    video.hide();

    detector = ml5.objectDetector('cocossd', modelReady)
}


function modelReady(){
  console.log('model loaded')
  detect();
}

function detect(){
  detector.detect(video, gotResults);
}

function gotResults(err, results){
  if(err){
    console.log(err);
    return
  }

  detections = results;
    print (detections);

  detect();
}

function draw() {
    image(video, 0, 0, width, height);

    if (detections) {
      detections.forEach(detection => {
        noStroke();
        fill(255);
        strokeWeight(2);
        text(detection.label, detection.x + 4, detection.y + 10)

        noFill();
        strokeWeight(3);
        if(detection.label === 'person'){
          stroke(0, 255, 0);
        } else {
          stroke(0,0, 255);
        }
        rect(detection.x, detection.y, detection.width, detection.height);  
      })
    } 
}

```


### "STOP LOOKING AT ME" in  PoseNet sketch

```
// Copyright (c) 2019 ml5
//
// This software is released under the MIT License.
// https://opensource.org/licenses/MIT

/* ===
ml5 Example
PoseNet example using p5.js
=== */

let video;
let poseNet;
let poses = [];

function setup() {
  createCanvas(640, 480);
  video = createCapture(VIDEO);
  video.size(width, height);

  // Create a new poseNet method with a single detection
  poseNet = ml5.poseNet(video, modelReady);
  // This sets up an event that fills the global variable "poses"
  // with an array every time new poses are detected
  poseNet.on('pose', function(results) {
    poses = results;
  });
  // Hide the video element, and just show the canvas
  video.hide();
}

function modelReady() {
  select('#status').html('Model Loaded');
}

function draw() {
  image(video, 0, 0, width, height);

  // We can call both functions to draw all keypoints and the skeletons
  drawKeypoints();
  drawSkeleton();
}

// A function to draw ellipses over the detected keypoints
function drawKeypoints()  {
  // Loop through all the poses detected
  for (let i = 0; i < poses.length; i++) {
    // For each pose detected, loop through all the keypoints
    let pose = poses[i].pose;
    for (let j = 0; j < pose.keypoints.length; j++) {
      // A keypoint is an object describing a body part (like rightArm or leftShoulder)
      let keypoint = pose.keypoints[j];
      // Only draw an ellipse is the pose probability is bigger than 0.2
      if (keypoint.score > 0.2) {
        fill(0);
        noStroke();
        rect(0, 0, 640, 480);
        fill(255);
text('Stop looking at me', 150, 150);
      }
    }
  }
}

// A function to draw the skeletons
function drawSkeleton() {
  // Loop through all the skeletons detected
  for (let i = 0; i < poses.length; i++) {
    let skeleton = poses[i].skeleton;
    // For every skeleton, loop through all body connections
    for (let j = 0; j < skeleton.length; j++) {
      let partA = skeleton[j][0];
      let partB = skeleton[j][1];
      stroke(255, 0, 0);
     
    }
  }
}


```
### "STOP LOOKING AT ME" in  ObjectDetector sketch


### Our Approach 

