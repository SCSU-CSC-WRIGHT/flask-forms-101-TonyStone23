# Flask Login App

## Overview

This project is a simple Flask application that demonstrates:

- Flask form usage with Flask-WTF
- Basic login and registration using Flask-Login
- SQLite database integration using SQLAlchemy
- Clean project structure for educational or GitHub deployment

## File Structure and Purpose

- **`run.py`**: Entry point of the app. Runs the Flask server.
- **`config.py`**: Stores config variables like secret keys and DB paths.
- **`app/__init__.py`**: Initializes Flask app, database, and login manager.
- **`app/routes.py`**: Contains all route handlers for pages like login, register, and logout.
- **`app/forms.py`**: Defines form classes for user input.
- **`app/models.py`**: Declares the User model used for authentication.
- **`app/templates/`**: Contains Jinja2 HTML templates for rendering views.
- **`requirements.txt`**: Lists all Python dependencies.

## How to Run The Application

```bash
git clone https://github.com/yourusername/flask-login-app.git
cd flask-login-app
# OPTIONAL: python -m venv venv; source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
flask run
```
Then visit: `http://localhost:5000`

## Interacting With the Database

You can work with the SQLite DB directly using the Flask shell:

```bash
flask shell
```

The database file is located in the `instance/` directory as `app.db`. You'll notice that the application redirects you there when the shell is activated. 

Note: Use exit() to exit the shell.

```python
# Flask Shell Queries for Exploring and Modifying the User Database

# Import the User model
from app.models import User

# View all users
User.query.all()

# Get a user by username
User.query.filter_by(username="jane").first()

# Get a user by ID
User.query.get(1)

# Search for users with a username that starts with 'a'
User.query.filter(User.username.startswith("a")).all()

# Count how many users are in the database
User.query.count()

# Change a user's password
from werkzeug.security import generate_password_hash
user = User.query.filter_by(username="jane").first()
user.password = generate_password_hash("new_secure_password")
db.session.commit()

# Delete a specific user
user = User.query.filter_by(username="jane").first()
db.session.delete(user)
db.session.commit()

# Delete all users (careful!)
User.query.delete()
db.session.commit()

# Add a new user manually
from werkzeug.security import generate_password_hash
new_user = User(username="john", password=generate_password_hash("johnpassword"))
db.session.add(new_user)
db.session.commit()

# Get all usernames in the database
[u.username for u in User.query.all()]
```

