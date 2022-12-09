# django_challenge

In order persist game data for users of the OKKO app, we need a new backend API to calculate game scores and save them to the database.

Create a new API endpoint that does the following:
* Accepts a payload of game data.
* Calculates a game score based on some logic
* Stores the game data and score to the database (using an appropriate Django model).
* Returns an appropriate response in JSON format.

## Getting started

You can **either**: 
- start a fresh django project 

or:
- Clone this repo
- Run `pip install -r requirements.txt`

## What we're expecting

- A working Django project 
- Code that conforms to the [PEP 8 Style Guide](https://peps.python.org/pep-0008/)
- Clean, well considered code
- Tests if appropriate

## Detail

### API Payload (game data)

The API endpoint should accept the following JSON data.

```
{
    "results": 
    [
        {
            "difficulty": 1,
            "tapped": true,
            "reaction_time": 1.237824
        },
        {
            "difficulty": 1,
            "tapped": true,
            "reaction_time": 2.192153
        },
        {
            "difficulty": 2,
            "tapped": true,
            "reaction_time": 2.85
        },
        {
            "difficulty": 2,
            "tapped": false,
            "reaction_time": null
        },
        {
            "difficulty": 3,
            "tapped": true,
            "reaction_time": 2.11299
        },
        {
            "difficulty": 3,
            "tapped": true,
            "reaction_time": 0.28299
        },
        {
            "difficulty": 4,
            "tapped": true,
            "reaction_time": 3.21234
        },
        {
            "difficulty": 4,
            "tapped": true,
            "reaction_time": 3.1222
        },
        {
            "difficulty": 5,
            "tapped": false,
            "reaction_time": null
        },
        {
            "difficulty": 5,
            "tapped": false,
            "reaction_time": null
        }
    ]
}
```

### Logic for calculating the game score

The game data consists of 10 rounds. Each data set has a session code and each round has:

- a difficulty integer between 1 and 5
- a boolean representing if the player tapped the object
- a float field representing the time in seconds it took to tap the object, between 0 and 5

The score is calculated as follows:

- if the object was tapped within 1 second you score 5 multiplied by the difficulty
- or if the object was tapped within 2 seconds you score 4 multiplied by the difficulty
- or if the object was tapped within 3 seconds you score 3 multiplied by the difficulty
- or if the object was tapped within 4 seconds you score 2 multiplied by the difficulty
- or if the object was tapped within 5 seconds you score 1 multiplied by the difficulty
- or if the object was not tapped you score no points


### Structure of Game Data (Database model)

The data to be stored is as follows:

- Session: uuid.uuid4, auto generated
- Score: int
- Results:
  - Difficulty: int
  - Tapped: bool
  - Reaction Time: float





An example expected return JSON is as follows:

```
{
    "session": "b3564555-264b-496d-acd7-0c896710de52",
    "score": 53
}
```


## Submission
- Please only spend a maximum of 2 hours on this task
- Please email a ZIP file of the project to [darren@okkohealth.com](mailto:darren@okkohealth.com) or a Github repo (if private please invite [@okko-darren](https://github.com/okko-darren))
- Any queries please email [darren@okkohealth.com](mailto:darren@okkohealth.com)
