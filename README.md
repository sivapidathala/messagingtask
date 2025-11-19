Messaging System with RabbitMQ, Celery, Nginx & Python

This project demonstrates a simple messaging system built using RabbitMQ, Celery, Flask, Gunicorn, Nginx, and Ngrok.
It provides a production-like environment to showcase asynchronous task processing, reverse proxy setup, and public endpoint exposure.

1. Objective

The goal of the project is to implement a lightweight messaging system where:

Emails can be sent asynchronously using Celery workers

Server timestamps can be logged synchronously

The system is exposed via an ngrok public URL for external testing

Nginx acts as a reverse proxy, forwarding traffic to the Flask application
 2. System Architecture
Frontend — Nginx Reverse Proxy

Listens on port 80

Forwards requests to Gunicorn (running Flask)

Provides clean, production-style routing

Backend — Python Application (Flask/FastAPI)

Two endpoints:

Endpoint	Description
/action?sendmail=<email>	Sends an email asynchronously via Celery
/action?talktome	Logs current server time to app.log
Celery + RabbitMQ Task Queue

RabbitMQ = message broker

Celery = background task execution

Tasks implemented:

send_email_task → Sends email via SMTP

log_time_task → Logs timestamps (async optional)

Ngrok Integration

Provides public HTTPS URL

Allows testing from outside the local machine

 3. Functional Requirements
✔ Email Sending (?sendmail)

Accepts email parameter

Publishes task to RabbitMQ

Celery worker sends the email via SMTP

✔ Timestamp Logging (?talktome)

Logs the current time into app.log

Useful for verifying synchronous request handling

✔ Task Execution

Email sending → asynchronous

Time logging → synchronous (or async variant with Celery)

4. Implementation Steps (Summary)

Install Dependencies

RabbitMQ

Celery

Flask / FastAPI

Gunicorn / Uvicorn

Nginx

Ngrok

Set Up RabbitMQ

Start broker locally

Ensure Celery can connect

Configure Celery

Define task functions

Configure broker URL (AMQP)

Develop Python App

Create API routes

Trigger Celery tasks

Configure Email (SMTP)

Use environment variables

Test email sending via Celery

Deploy Behind Nginx

Reverse proxy configuration

Gunicorn used to serve Flask

Expose Public Endpoint

Run ngrok on port 80

Share public HTTPS URL for testing

 5. Testing Procedure
Send Email
https://<ngrok-id>.ngrok.io/action?sendmail=test@example.com


Expected: Email sent asynchronously.

Log Timestamp
https://<ngrok-id>.ngrok.io/action?talktome


Expected: New timestamp added to app.log.

 6. Deliverables (Completed)

✔ Running system exposed via ngrok

✔ Screen recording (≤ 3 minutes) showing:

RabbitMQ running

Celery worker processing tasks

Flask/Nginx handling requests

Email sent successfully

Log file updated

Ngrok endpoint testing

🛠️ 7. Technologies Used

RabbitMQ — Message Broker

Celery — Task Queue Manager

Flask / FastAPI — Python Web Framework

Gunicorn / Uvicorn — Application Server

Nginx — Reverse Proxy

SMTP — Email Sending

Ngrok — Public HTTPS Exposure

Python 3.9+

8. Conclusion

This project demonstrates a complete asynchronous task execution pipeline using RabbitMQ and Celery.
With Nginx handling routing and ngrok providing public access, the system simulates real-world production patterns.

It successfully proves:

Background task offloading

Message broker integration

Reverse proxy usage

Public API testing

Author

Siva Pidathala
