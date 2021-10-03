# example-python-flask

Following freeCodeCamp.org's tutorial "Learn Flask for Python": https://www.youtube.com/watch?v=Z1RJmh_OqeA 

note: steps below written as executed on Mac OSX

### Step 1. Set up Virtual Environment
```
cd path/to/project
pip install virtualenv
virtualenv env
source env/bin/activate
```

### Step 2. Install Python libraries 
```
pip install -r requirements.txt
```

### Step 3. Build code for Flask app
Code is in `app.py`, `base.html`, and `index.html` (styling via `static/css/main.css`)
   
### Step 4: Initialize database
In terminal, start an interactive python3 shell (while still in virtualenv "env"):
```python
from app import db
db.create_all()
```
This creates the sqlite database file test.db in the project root directory

### Step 5: Use app
In terminal, start the app:
```
python3 app.py
```

Not covering deployment to heroku, but he covers it in the tutorial here: https://youtu.be/Z1RJmh_OqeA?t=2484

### Appendix: Notes on features & conventions
* HTML template inheritance: The curly brace / percent signs (e.g. `{% block head %}{% endblock %}`) are [Jinja syntax](https://jinja.palletsprojects.com/en/3.0.x/templates/#base-template). In this example, the blocks define two blocks that child templates can fill in. All the block tag does is tell the template engine that a child template may override those placeholders in the template.
* CSS template `static/css/main.css` is linked in the HTML template `templates/base.html`
    - In `base.html`, we use the `Flask.url_for` method for static files explained here: https://flask.palletsprojects.com/en/2.0.x/tutorial/static/#static-files - Note: can also do this with other files, like JavaScript functions or logo images
* `app.py`
  - `Flask(__name__)`: This gets the import name of the place the app is defined.  This way, when using a package and app defined in `__init__.py`, then the `__name__` will still point to the correct place
* Program flow
  - `index.html` inherits from `base.html`
  - Create, Update, and Delete transactions to the sqlite database are handled via API endpoints defined in `app.py` (see the `@app.route`) lines
  - Current state of task table is queried from the sqlite database.  Example: `tasks = Todo.query.order_by(Todo.date_created).all()`