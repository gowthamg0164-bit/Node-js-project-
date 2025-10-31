# Node-js-project-
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Email Reminder System</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    .container {
      background: white;
      padding: 30px;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
      width: 400px;
    }
    h2 { text-align: center; }
    input, textarea, button {
      width: 100%;
      padding: 10px;
      margin: 8px 0;
      border-radius: 4px;
      border: 1px solid #ccc;
    }
    button {
      background: #007bff;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover { background: #0056b3; }
  </style>
</head>
<body>
  <div class="container">
    <h2>Email Reminder System</h2>
    <form id="reminderForm">
      <label>Email:</label>
      <input type="email" id="email" required />

      <label>Subject:</label>
      <input type="text" id="subject" required />

      <label>Message:</label>
      <textarea id="message" required></textarea>

      <label>Reminder Time:</label>
      <input type="datetime-local" id="time" required />

      <button type="submit">Set Reminder</button>
    </form>
    <p id="status"></p>
  </div>
const express = require("express");
const nodemailer = require("nodemailer");
const bodyParser = require("body-parser");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(bodyParser.json());

app.post("/reminder", (req, res) => {
  const { email, subject, message, time } = req.body;

  const reminderTime = new Date(time).getTime();
  const delay = reminderTime - Date.now();

  if (delay < 0) {
    return res.json({ message: "Please select a future time." });
  }

  setTimeout(() => {
    sendEmail(email, subject, message);
  }, delay);

  res.json({ message: "Reminder scheduled successfully!" });
});

function sendEmail(to, subject, text) {
  const transporter = nodemailer.createTransport({
    service: "gmail",
    auth: {
      user: "yourgmail@gmail.com", // Replace with your email
      pass: "yourpassword" // Use app password if 2FA is on
    }
  });

  const mailOptions = {
    from: "yourgmail@gmail.com",
    to,
    subject,
    text
  };

  transporter.sendMail(mailOptions, (error, info) => {
    if (error) console.log(error);
    else console.log("Email sent: " + info.response);
  });
}

app.listen(3000, () => console.log("Server running on port 3000"));

  <script>
    const form = document.getElementById("
