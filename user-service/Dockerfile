# Use an official Python runtime as a parent image
FROM python:3.8-slim-buster

# Set the working directory in the container to /app
WORKDIR /usr/src/app

# Add the current directory contents into the container at /app
COPY requirements.txt /usr/src/app

# Install any needed packages specified in requirements.txt
RUN --mount=type=cache,target=/root/.cache/pip \
    pip3 install -r requirements.txt

COPY app.py /usr/src/app

EXPOSE 3001

CMD ["python3", "/usr/src/app/app.py"]