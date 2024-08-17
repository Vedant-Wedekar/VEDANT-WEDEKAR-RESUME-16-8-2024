<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Zoom and Drag Notebook Page</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            cursor: grab;
        }
        .notebook-container {
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            cursor: grab;
        }
        .notebook-page {
            transition: transform 0.3s ease, transform-origin 0.3s ease;
            width: auto;
            height: 100%;
            max-height: 100%;
            object-fit: contain;
            cursor: grab;
        }
    </style>
</head>
<body>
    <div class="notebook-container" id="container">
        <img src="VedantNWedekarResume (1)-1.png" alt="Notebook Page" class="notebook-page" id="notebookImage">
    </div>

    <script>
        let scale = 1;
        let isDragging = false;
        let startX, startY, initialX = 0, initialY = 0;
        let currentX = 0, currentY = 0;
        const notebookImage = document.getElementById('notebookImage');
        const container = document.getElementById('container');

        // Zoom on scroll
        notebookImage.addEventListener('wheel', (event) => {
            event.preventDefault();

            const rect = notebookImage.getBoundingClientRect();
            const x = event.clientX - rect.left;
            const y = event.clientY - rect.top;

            notebookImage.style.transformOrigin = `${x}px ${y}px`;

            if (event.deltaY < 0) {
                scale += 0.1;
            } else {
                scale -= 0.1;
            }

            scale = Math.min(Math.max(1, scale), 3);
            notebookImage.style.transform = `scale(${scale}) translate(${currentX}px, ${currentY}px)`;
        });

        // Drag and move
        container.addEventListener('mousedown', (event) => {
            isDragging = true;
            startX = event.clientX - currentX;
            startY = event.clientY - currentY;

            document.body.style.cursor = 'grabbing';
        });

        container.addEventListener('mousemove', (event) => {
            if (isDragging) {
                currentX = event.clientX - startX;
                currentY = event.clientY - startY;

                notebookImage.style.transform = `scale(${scale}) translate(${currentX}px, ${currentY}px)`;
            }
        });

        container.addEventListener('mouseup', () => {
            isDragging = false;
            document.body.style.cursor = 'grab';
        });

        container.addEventListener('mouseleave', () => {
            isDragging = false;
            document.body.style.cursor = 'grab';
        });
    </script>
</body>
</html>
