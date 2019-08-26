---
layout: post
title: "#16 - A Brief Introduction to Flask"
author: "Hallessandro D´villa"
categories: programming
tags: [python, flask, programming]
image: coverPosts/flask-python.png
header-img: "coverPosts/flask-python.png"
---

Hey, everyone, what's up! 

My name is Hallessandro, I am a software developer that currently works and live in Brazil and in this post we will see how 

```python
pip install flask
pip install ipython
```

```python
#Save the file with the name app.py
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "Hello World! &lt;strong&gt;I am learning Flask&lt;/strong&gt;", 200

app.run()
```

```python
python app.py
```
For now this is all folks, thanks for reading and feel free to contact me. 