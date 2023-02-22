FROM python:3.10-slim-buster

#Going inside container
WORKDIR /backend-flask

# Coping all the required libraries we want to install inside container
COPY requirements.txt requirements.txt

#Installing Python libraries for the app
RUN pip3 install -r requirements.txt

COPY . .
# Set Env Variables 
ENV FLASK_ENV=development

EXPOSE ${PORT}
#python3 -m flask run --host=0.0.0.0 --port=4567

CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]