# Reminder Service

The **Reminder Service** is a microservice designed to handle email notifications and reminders for an Airline Booking System. It allows scheduling and sending emails using RabbitMQ for message queuing and dedicated jobs for processing reminders.

## 🚀 Technologies Used

- **Node.js**: Runtime environment.
- **Express.js**: Web framework for building the API.
- **MySQL**: Relational database for storing ticket/reminder information.
- **Sequelize**: ORM for database interaction.
- **RabbitMQ**: Message broker for handling asynchronous communication (using `amqplib`).
- **Nodemailer**: Module for sending emails.
- **Node-Cron**: Task scheduler for running periodic jobs.

## 🛠️ Setup and Installation

### 1. Prerequisites
Ensure you have the following installed on your machine:
- [Node.js](https://nodejs.org/) (v14 or higher)
- [MySQL](https://www.mysql.com/)
- [RabbitMQ](https://www.rabbitmq.com/)

### 2. Clone the Repository
```bash
git clone <repository-url>
cd ReminderService
```

### 3. Install Dependencies
```bash
npm install
```

### 4. Configuration
Create a `.env` file in the root directory and add the following environment variables:

```env
PORT=3003
EMAIL_ID=your_email@gmail.com
EMAIL_PASS=your_email_app_password
MESSAGE_BROKER_URL=amqp://localhost
EXCHANGE_NAME=AIRLINE_BOOKING
REMINDER_BINDING_KEY=REMINDER_SERVICE
```
> **Note**: For Gmail, use an [App Password](https://support.google.com/accounts/answer/185833) instead of your regular password.

### 5. Database Setup
Initialize the database and run migrations:

```bash
npx sequelize db:create
npx sequelize db:migrate
```

## 🏃‍♂️ Usage

### Start the Server
```bash
npm start
```
The server will start on the port specified in your `.env` file (default is 3003).

### API Endpoints

#### Create a Notification Ticket
- **URL**: `/api/v1/tickets`
- **Method**: `POST`
- **Body**:
    ```json
    {
        "subject": "Flight Reminder",
        "content": "Your flight is scheduled for tomorrow.",
        "recepientEmail": "user@example.com",
        "notificationTime": "2023-10-27T10:00:00"
    }
    ```
- **Response**:
    ```json
    {
        "success": true,
        "data": { ... },
        "message": "Successfully registered an email reminder"
    }
    ```

## 🔄 Message Queue (RabbitMQ)
This service subscribes to the `REMINDER_SERVICE` binding key on the `AIRLINE_BOOKING` exchange. It listens for events to trigger email notifications asynchronously.
