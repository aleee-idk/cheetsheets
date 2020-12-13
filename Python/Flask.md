# Flask Cheetsheet

## Jinja 2 Templates

TODO Improve this section

[Jinja2 Docs](https://jinja.palletsprojects.com/en/2.11.x/)
[Flask Templates Docs](https://flask.palletsprojects.com/en/1.1.x/tutorial/templates/)
[Resources](https://realpython.com/primer-on-jinja-templating/)

Jinja is the default template engine and comes pre installed with Flask, but can also be installed estandalone.

It’s worth noting that Jinja only supports a few control structures: if-statements and for-loops are the two primary structures.

The syntax is similar to Python, differing in that no colon is required and that termination of the block is done using an endif or endfor instead of whitespace.

You can also complete the logic within your controller or views and then pass each value to the template using the template tags. However, it is much easier to perform such logic within the templates themselves.

## Basic structure

The variables and/or logic are placed between tags or delimiters. For example, Jinja templates use {% ... %} for expressions or logic (like for loops), while {{ ... }} is used for outputting the results of an expression or a variable to the end user. The latter tag, when rendered, is replaced with a value or values, and is seen by the end user.

### Standalone

```Python
from jinja2 import Template
t = Template("Hello {{ something }}!")
t.render(something="World")

t = Template("My favorite numbers: {% for n in range(1,10) %}{{n}} " "{% endfor %}")
t.render()
```

[Load templates from local folder:](https://stackoverflow.com/questions/38642557/how-to-load-jinja-template-directly-from-filesystem)

```Python
#!/usr/bin/python
import jinja2

templateLoader = jinja2.FileSystemLoader(searchpath="./path/to/template/folder")
templateEnv = jinja2.Environment(loader=templateLoader)
TEMPLATE_FILE = "template.html"
template = templateEnv.get_template(TEMPLATE_FILE)
outputText = template.render()  # this is where to put args to the template renderer

print(outputText)
```

### Flask:

```Python
from flask import Flask, render_template
app = Flask(__name__)


@app.route("/")
def template_test():
    return render_template('template.html', my_string="Wheeeee!", my_list=[0,1,2,3,4,5])


if __name__ == '__main__':
    app.run(debug=True)
```

Template:

```HTML
<!DOCTYPE html>
<html>
  <head>
    <title>Flask Template Example</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" media="screen">
    <style type="text/css">
      .container {
        max-width: 500px;
        padding-top: 100px;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <p>My string: {{my_string}}</p>
      <p>Value from the list: {{my_list[3]}}</p>
      <p>Loop through the list:</p>
      <ul>
        {% for n in my_list %}
        <li>{{n}}</li>
        {% endfor %}
      </ul>
    </div>
    <script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
    <script src="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/js/bootstrap.min.js"></script>
  </body>
</html>
```

## Template Inheritance

Templates usually take advantage of inheritance, which includes a single base template that defines the basic structure of all subsequent child templates. You use the tags {% extends %} and {% block %} to implement inheritance.

### Parent Template

```HTML
<!DOCTYPE html>
<html>
  <head>
    <title>Flask Template Example</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel="stylesheet" media="screen">
    <style type="text/css">
      .container {
        max-width: 500px;
        padding-top: 100px;
      }
      h2 {color: red;}
    </style>
  </head>
  <body>
    <div class="container">
      <h2>This is part of my base template</h2>
      <br>
      {% block content %}{% endblock %}
      <br>
      <h2>This is part of my base template</h2>
    </div>
    <script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
    <script src="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/js/bootstrap.min.js"></script>
  </body>
</html>
```

### Child Template

```HTML
{% extends "layout.html" %}
{% block content %}
  <h3> This is the start of my child template</h3>
  <br>
  <p>My string: {{my_string}}</p>
  <p>Value from the list: {{my_list[3]}}</p>
  <p>Loop through the list:</p>
  <ul>
    {% for n in my_list %}
    <li>{{n}}</li>
    {% endfor %}
  </ul>
  <h3> This is the end of my child template</h3>
{% endblock %}
```