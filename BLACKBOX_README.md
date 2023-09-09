 ## ASL to Text Converter

This project is an ASL to Text Converter built with React, ml5.js, and React Speech Kit. It utilizes a pre-trained machine learning model to classify hand gestures from a webcam and convert them into text. The converted text can then be spoken aloud using the React Speech Kit.

### Prerequisites

To run this project, you will need the following:

* Node.js installed on your system
* A webcam

### Setup

1. Clone the project repository:

```
git clone https://github.com/your-username/asl-to-text-converter.git
```

2. Install the dependencies:

```
npm install
```

3. Start the development server:

```
npm start
```

4. Open your browser and go to http://localhost:3000 to see the app in action.

### Code Explanation

The code for this project is divided into two main files: `App.js` and `package.json`.

#### `App.js`

The `App.js` file is the main component of the app. It contains the code that handles the user interface, as well as the logic for classifying hand gestures and converting them into text.

The first part of the code imports the necessary libraries and components.

```
import React, { useEffect, useRef, useState } from "react";
import ml5 from "ml5";
import useInterval from "@use-it/interval";
import { useSpeechSynthesis } from "react-speech-kit";

import "./App.css";
```

The `useEffect` hook is used to initialize the machine learning model and start the webcam.

```
useEffect(() => {
  classifier = ml5.imageClassifier("./model/model.json", () => {
    navigator.mediaDevices
      .getUserMedia({ video: true, audio: false })
      .then((stream) => {
        videoRef.current.srcObject = stream;
        videoRef.current.addEventListener("loadedmetadata", () => {
          videoRef.current.play();
          setLoaded(true);
        });
      });
  });

  // Add an event listener for the 'voiceschanged' event
  window.speechSynthesis.addEventListener("voiceschanged", () => {
    const availableVoices = window.speechSynthesis.getVoices();
    setVoices(availableVoices);

Generated by [BlackboxAI](https://www.useblackbox.ai)