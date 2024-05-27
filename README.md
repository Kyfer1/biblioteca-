from flask import Flask, render_template, jsonify
import json
import os

app = Flask(__name__)

# Ruta principal que muestra la página de inicio
@app.route('/')
def home():
    return render_template('home.html')

# Ruta para mostrar la biblioteca
@app.route('/biblioteca')
def biblioteca():
    return render_template('index.html')

# Ruta para obtener la lista de libros en formato JSON
@app.route('/api/libros')
def libros():
    with open('books/libros.json') as libros_file:
        libros_data = json.load(libros_file)
    return jsonify(libros_data)

if __name__ == '__main__':
    port = int(os.environ.get('PORT', 5000))
    app.run(debug=True, host='0.0.0.0', port=port)
