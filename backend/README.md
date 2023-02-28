# Backend - Trivia API

## Setting up the Backend

### Install Dependencies

1. **Python 3.7** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

2. **Virtual Environment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

3. **PIP Dependencies** - Once your virtual environment is setup and running, install the required dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

#### Key Pip Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in `app.py`and can reference `models.py`.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross-origin requests from our frontend server.

### Set up the Database

With Postgres running, create a `trivia` database:

```bash
createdb trivia
```

Populate the database using the `trivia.psql` file provided. From the `backend` folder in terminal run:

```bash
psql trivia < trivia.psql
```

### Run the Server

From within the `./src` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## To Do Tasks

These are the files you'd want to edit in the backend:

1. `backend/flaskr/__init__.py`
2. `backend/test_flaskr.py`

One note before you delve into your tasks: for each endpoint, you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior.

1. Use Flask-CORS to enable cross-domain requests and set response headers.
2. Create an endpoint to handle `GET` requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories.
3. Create an endpoint to handle `GET` requests for all available categories.
4. Create an endpoint to `DELETE` a question using a question `ID`.
5. Create an endpoint to `POST` a new question, which will require the question and answer text, category, and difficulty score.
6. Create a `POST` endpoint to get questions based on category.
7. Create a `POST` endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question.
8. Create a `POST` endpoint to get questions to play the quiz. This endpoint should take a category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions.
9. Create error handlers for all expected errors including 400, 404, 422, and 500.

## Documenting your Endpoints

You will need to provide detailed documentation of your API endpoints including the URL, request parameters, and the response body. Use the example below as a reference.

## Endpoints Documentation

1. `GET '/categories'`

- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a key, `categories`, that contains an object of `id: category_string` key: value pairs. `success` with value `True` and `total_categories` with value `len(formatted_categories)`

```json
success: True,
total_categories : len(formatted_categories),
categories: 
{
  "1": "Science",
  "2": "Art",
  "3": "Geography",
  "4": "History",
  "5": "Entertainment",
  "6": "Sports"
}
```

2. `GET '/questions'`

- Fetches a dictionary of all questions. which include id, question, answer, difficulty and category
- Request Arguments: `page=page_no`
- Returns: An object with a category, id, question, answer and difficulty. type of difficulty is `int`.

```json
success: True,
total_questions : len(Question.query.all()),
question: "what is udacity?",
answer: "LMS".
difficulty: 3,
category: 4
```

3. `GET '/categories/2/questions'`

- Fetches a dictionary of all questions by a specific id. which include id, question, answer, difficulty and category
- Request Arguments: `id`
- Returns: An object with a category, id, question, answer and difficulty. type of difficulty is `int`.

```json
success: True,
total_questions : len(Question.query.all()),
question: "what is udacity?",
answer: "LMS".
difficulty: 3,
category: 4
```

4. `POST '/questions'`

- Creates a new question. which include id, question, answer, difficulty and category
- Request Arguments: `id, question, answer, difficulty, category`
- Returns: An object with a category, id, question, answer and difficulty. type of difficulty is `int`.

```json
success: True,
created: {
  id: 4,
  question: "what is udacity?"
  answer: "LMS",
  difficulty: 5,
  category: 4
}
total_questions : len(Question.query.all()),
question: "what is udacity?",
answer: "LMS".
difficulty: 3,
category: 4
```

5. `DELETE '/questions/1'`

- Deletes a question from the resource.
- Request Arguments: `id`
- Returns: An object that question is being deleted.

```json
success: True,
deleted: {
  id: 4,
  question: "what is udacity?"
  answer: "LMS",
  difficulty: 5,
  category: 4
}
total_questions : len(Question.query.all()),
questions: [array of updated questions response]
```

6. `GET '/questions/search'`

- Fetches a question based on a search query.
- Request Arguments: `search`
- Returns: An array that question's are being matched with searched string.

```json
success: True,
deleted: {
  id: 4,
  question: "what is udacity?"
  answer: "LMS",
  difficulty: 5,
  category: 4
}
total_questions : len(Question.query.all()),
questions: [array of updated questions response],
categories: [all the categories],
current_category: None
```

7. `Post '/quizzes'`

- Fetches a random question based on a category and filtered from old questions.
- Request Arguments: `category_id and old_questions_array`
- Returns: a new question.

```json
success: True,
question: {
  id: 4,
  question: "what is udacity?"
  answer: "LMS",
  difficulty: 5,
  category: 4
}
```

### Documentation Example

`GET '/api/v1.0/categories'`

- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
- Request Arguments: None
- Returns: An object with a single key, `categories`, that contains an object of `id: category_string` key: value pairs.

```json
{
  "1": "Science",
  "2": "Art",
  "3": "Geography",
  "4": "History",
  "5": "Entertainment",
  "6": "Sports"
}
```

## Testing

Write at least one test for the success and at least one error behavior of each endpoint using the unittest library.

To deploy the tests, run

```bash
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
