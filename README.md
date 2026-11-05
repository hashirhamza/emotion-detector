# Final Project

## Emotion Detector

A web application that analyzes text to identify **anger, disgust, fear, joy, and sadness** using IBM Watson NLP. Built with Python and Flask, it displays emotion scores and highlights the emotion with the highest score.

Developed as the final project for IBM's *Developing AI Applications with Python and Flask* course on Coursera, using the provided starter repository.

## Features

- Analyze customer feedback and other English text.
- Display scores for five emotions.
- Identify the dominant emotion.
- Return a clear message for blank input.
- Expose the detector through a reusable Python package.
- Test all five emotion categories using Python's `unittest`.

## Technology Stack

| Technology | Purpose |
| --- | --- |
| Python | Application logic |
| Flask | Web server and routes |
| IBM Watson NLP | Emotion prediction |
| Requests | HTTP requests to the NLP service |
| HTML, CSS, JavaScript | Provided browser interface |
| unittest | Automated tests |
| Pylint | Static code analysis |

## Project Structure

```text
oaqjp-final-project-emb-ai/
├── EmotionDetection/
│   ├── __init__.py
│   └── emotion_detection.py
├── static/
│   └── mywebscript.js
├── templates/
│   └── index.html
├── server.py
├── test_emotion_detection.py
├── README.md
└── LICENSE
```

## Environment Requirement

The emotion prediction endpoint used in this project is hosted on the **IBM Skills Network platform** and is accessible from the **Skills Network Theia Lab**.

Run the application and tests in that environment. Cloning this repository to a local computer does not provide access to the lab-hosted API.

## Setup and Run

In the Skills Network Theia Lab terminal:

### 1. Clone the repository

```bash
git clone https://github.com/hashirhamza/oaqjp-final-project-emb-ai.git
cd oaqjp-final-project-emb-ai
```

### 2. Install dependencies

```bash
python3 -m pip install requests flask pylint
```

### 3. Start the Flask server

```bash
python3 server.py
```

The server listens on port **5000**. Use the lab's **Launch Application** option with port `5000` to open the interface.

Enter text such as:

```text
I think I am having fun
```

Click the analysis button to display the emotion scores and dominant emotion. Keep the server terminal running while using the application.

## How It Works

1. The browser sends the input text to the Flask `/emotionDetector` route.
2. The server calls `emotion_detector` from the `EmotionDetection` package.
3. The function sends an HTTP POST request to Watson NLP.
4. The JSON response is parsed to extract five emotion scores.
5. The emotion with the highest score becomes `dominant_emotion`.
6. Flask formats the result for display in the browser.

The detector returns a dictionary with these keys:

| Key | Value |
| --- | --- |
| `anger` | Anger score |
| `disgust` | Disgust score |
| `fear` | Fear score |
| `joy` | Joy score |
| `sadness` | Sadness score |
| `dominant_emotion` | Name of the emotion with the highest score |

Use the package directly:

```python
from EmotionDetection import emotion_detector

result = emotion_detector("I am so happy I am doing this")
print(result)
```

Scores are produced by the service for each input.

## Error Handling

When the Watson service returns HTTP **400**, the detector returns all six dictionary keys with `None` values.

When `dominant_emotion` is `None`, the web application displays:

```text
Invalid text! Please try again!
```

## Unit Tests

Run:

```bash
python3 test_emotion_detection.py -v
```

The test suite checks the following statements:

| Statement | Expected dominant emotion |
| --- | --- |
| I am glad this happened | joy |
| I am really mad about this | anger |
| I feel disgusted just hearing about this | disgust |
| I am so sad about this | sadness |
| I am really afraid that this will happen | fear |

All five tests passed during lab testing. These tests call the live Watson service and require access to the Skills Network endpoint.

## Static Code Analysis

Check the Flask server with:

```bash
python3 -m pylint server.py
```

The server includes module and function docstrings. Pylint output should be checked in the lab to confirm the score for the current version.

## Credits

Implemented by **Hashir Hamza** as an IBM/Coursera course project.

The starter repository, frontend template, and lab-hosted NLP service were provided by IBM Skills Network.

Original repository: [ibm-developer-skills-network/oaqjp-final-project-emb-ai](https://github.com/ibm-developer-skills-network/oaqjp-final-project-emb-ai).

## License

See [LICENSE](LICENSE) for the license terms supplied with the repository.

