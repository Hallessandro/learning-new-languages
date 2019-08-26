---
layout: post
title: "#15 - Getting Started with Python and MongoDB"
author: "Hallessandro D´villa"
categories: programming
tags: [python, mongodb, mongo, programming]
image: coverPosts/python_and_mongo.png
header-img: "coverPosts/python_and_mongo.png"
---

Hey, everyone, what's up! 

My name is Hallessandro, I am a software developer that currently works and live in Brazil and in this post we will see how to integrate Python and MongoDB. 

> This tutorial assumes that a MongoDB instance installed and running on your machine on the default host and port, if you don't have MongoDB installed, check how to do this in the following link: 

[How to Install MongoDB on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-18-04)

### Installing PyMongo

Before we start you need install the PyMongo, a Python driver for MongoDB: 

```python
python -m pip install pymongo        
```
To get a specific version of PyMongo, run this command: 
```python
python -m pip install pymongo==3.5.1
```
If you already have a distribution of PyMongo on your machine, you can update it using this command:

```python
python -m pip install --upgrade pymongo
```
For test your distribution of PyMongo, in the Python shell run the following command. If everything is ok, the command will run without any exception.

```python
import pymongo
```

### Making a Connection

For now this is all folks, thanks for reading and feel free to contact me. 