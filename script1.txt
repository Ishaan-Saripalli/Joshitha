const canvas = document.getElementById('confetti');
const context = canvas.getContext('2d');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const confettiElements = [];
const colors = ['#f94144', '#f3722c', '#f9c74f', '#90be6d', '#577590'];

for (let i = 0; i < 200; i++) {
    confettiElements.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        radius: Math.random() * 10 + 2,
        color: colors[Math.floor(Math.random() * colors.length)],
        speedX: Math.random() * 2 - 1,
        speedY: Math.random() * 3 + 2
    });
}

function renderConfetti() {
    context.clearRect(0, 0, canvas.width, canvas.height);
    
    confettiElements.forEach((confetti) => {
        context.beginPath();
        context.arc(confetti.x, confetti.y, confetti.radius, 0, Math.PI * 2);
        context.fillStyle = confetti.color;
        context.fill();

        confetti.x += confetti.speedX;
        confetti.y += confetti.speedY;

        if (confetti.y > canvas.height) {
            confetti.y = -confetti.radius;
            confetti.x = Math.random() * canvas.width;
        }
    });
    requestAnimationFrame(renderConfetti);
}

renderConfetti();
