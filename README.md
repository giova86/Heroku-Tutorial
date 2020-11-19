# Heroku-Tutorial
Heroku is one of the easiest platforms for deploying and managing public Flask applications. The git & buildpack-based deployment of UIs of Heroku and Dash Enterprise are nearly identical, enabling an easy transition to Dash Enterprise if you are already using Heroku.

This tutorial will explain how to deploy a dash application on Heroku.

* app.py
```
import os

import dash
import dash_core_components as dcc
import dash_html_components as html

external_stylesheets = ['https://codepen.io/chriddyp/pen/bWLwgP.css']

app = dash.Dash(__name__, external_stylesheets=external_stylesheets)

server = app.server

app.layout = html.Div([
    html.H2('Hello World'),
    dcc.Dropdown(
        id='dropdown',
        options=[{'label': i, 'value': i} for i in ['LA', 'NYC', 'MTL']],
        value='LA'
    ),
    html.Div(id='display-value')
])

@app.callback(dash.dependencies.Output('display-value', 'children'),
              [dash.dependencies.Input('dropdown', 'value')])
def display_value(value):
    return 'You have selected "{}"'.format(value)

if __name__ == '__main__':
    app.run_server(debug=True)
```

* requirement.txt

```
pip freeze > requirements.txt
```

* Procfile

```
web: gunicorn app:server
```

* runtime.txt

```
python-3.8.2
