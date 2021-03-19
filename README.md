# What is this
At the time of writing, I am a tutor at my university's math center, where students can stop by to get personalized help with homework. We were told that we were going to get a card reader that students can use to sign in to the math center. Before, students had to write their name in a folder along with their sign in and sign out time, but this record was hard to analyze with students often forgetting to fill out the sheet. Thus the school adopted [Starfish](https://www.hobsons.com/solution/starfish/) which helps the school monitor student performance and provide tools that connect students with university resources like the math center. Now as opposed to writing their name in a folder, students need to type in their student id number and last name on the sign in page provided by Starfish, and having a card reader would streamline the process.

I decided it would be funny to make an overkilled card reader that uses computer vision to read the data off our student id card and fill out the sign in page. [A demonstration can be found here.](https://www.youtube.com/watch?v=uWYgrGI7wMs)

# How does it work?
This project uses OpenCV to detect our red student id card. It then crops the photo to the card, aligns the card, and executes image processing for [Tesseract](https://github.com/tesseract-ocr/tesseract) to read off the student's name and id.

To get the OpenCV program to communicate with Starfish's sign in page, I generated a WebSocket server which the web browser connects to. This choice was made so that the computer vision task could be offloaded to another computer as opposed to being run on the computer serving the sign in page. When a card has been successfully read, the WebSocket server notifies the browser of the student's name and id which is then used to fill in the relevant text fields. Unfortunately this hacky solution requires that we inject some Javascript code into the sign in page so that we can communicate with the WebSocket server.

Obviously, using a card reader is the superior solution as it is faster, less error prone, and more intuitive to use. Nevertheless, this was a educational silly project made to solve a relatively simple problem with a high-powered solution.