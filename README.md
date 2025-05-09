index.html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>CSS3 Transitions and Animations</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <header>
    <h1>CSS3 Transitions & Animations</h1>
  </header>

  <section>
    <button id="animateButton">Click Me for Animation</button>
    <div id="animatedBox" class="box"></div>
    <button id="savePreferences">Save Preferences</button>
  </section>

  <section>
    <h2>Your Preferences</h2>
    <div id="userPreferences"></div>
  </section>

  <script src="script.js"></script>
</body>
</html>


style.css
body {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 20px;
  background-color: #f9f9f9;
}

h1 {
  font-size: 2em;
  margin-bottom: 20px;
}

button {
  padding: 10px 20px;
  font-size: 1em;
  margin: 10px;
  cursor: pointer;
}

#animatedBox {
  width: 100px;
  height: 100px;
  margin: 20px auto;
  background-color: #3498db;
  transition: transform 1s ease, background-color 1s ease;
}

/* Animation trigger */
.animate {
  transform: rotate(360deg);
  background-color: #e74c3c;
}

/* Simple fade-in effect */
.fadeIn {
  animation: fadeIn 2s ease-out;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

 script.js
 // Store and Retrieve user preferences from localStorage
document.getElementById("savePreferences").addEventListener("click", function () {
  // Simulate user preference data
  const userPreferences = {
    theme: "dark",
    fontSize: "16px",
  };

  // Store in localStorage
  localStorage.setItem("preferences", JSON.stringify(userPreferences));

  // Display saved preferences
  displayPreferences();
});

// Function to display preferences from localStorage
function displayPreferences() {
  const savedPreferences = JSON.parse(localStorage.getItem("preferences"));
  const userPreferencesDiv = document.getElementById("userPreferences");

  if (savedPreferences) {
    userPreferencesDiv.innerHTML = `
      <p>Theme: ${savedPreferences.theme}</p>
      <p>Font Size: ${savedPreferences.fontSize}</p>
    `;
  } else {
    userPreferencesDiv.innerHTML = `<p>No preferences saved yet.</p>`;
  }
}

// Trigger CSS animation on button click
document.getElementById("animateButton").addEventListener("click", function () {
  const box = document.getElementById("animatedBox");

  // Add animation class
  box.classList.add("animate");

  // Remove the animation class after it's done to allow retrigger
  setTimeout(() => {
    box.classList.remove("animate");
  }, 1000); // Match duration of the CSS animation
});

// Fade-in animation when the page loads
window.addEventListener("load", function () {
  document.body.classList.add("fadeIn");
  displayPreferences(); // Display preferences on load
});



