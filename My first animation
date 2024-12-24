const express = require("express");
const multer = require("multer");
const bodyParser = require("body-parser");
const path = require("path");

// Create Express app
const app = express();

// Middleware for parsing form data
app.use(bodyParser.urlencoded({ extended: true }));

// Serve static files
app.use(express.static("public"));

// File upload configuration
const storage = multer.diskStorage({
  destination: (req, file, cb) => {
    cb(null, "uploads/");
  },
  filename: (req, file, cb) => {
    cb(null, `${Date.now()}-${file.originalname}`);
  },
});
const upload = multer({ storage });

// Handle form submission
app.post("/submit", upload.single("image"), (req, res) => {
  const { name, age } = req.body;
  const imagePath = req.file ? `/uploads/${req.file.filename}` : "";

  // Send data back to the frontend
  res.send(`
    <!DOCTYPE html>
    <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Christmas Gift</title>
      <style>
        body {
          font-family: Arial, sans-serif;
          text-align: center;
          background: #2b5876;
          color: white;
          margin: 0;
          padding: 0;
        }
        .gift {
          margin-top: 50px;
          padding: 30px;
          background: rgba(255, 255, 255, 0.1);
          border-radius: 15px;
          box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
          display: inline-block;
        }
        .uploaded-image {
          max-width: 150px;
          border-radius: 50%;
          margin-top: 20px;
          border: 3px solid gold;
        }
        .verse {
          font-size: 1.5em;
          margin: 20px 0;
        }
      </style>
    </head>
    <body>
      <h1>🎄 Merry Christmas, ${name}! 🎄</h1>
      <div class="gift">
        <p>Age: ${age}</p>
        <p class="verse">"For unto us a child is born, unto us a son is given." - Isaiah 9:6</p>
        <img src="${imagePath}" alt="User Image" class="uploaded-image">
        <p>Best wishes from Yabesh Gotame!</p>
      </div>
      <a href="/">Go Back</a>
    </body>
    </html>
  `);
});

// Serve uploaded images
app.use("/uploads", express.static(path.join(__dirname, "uploads")));

// Start the server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
