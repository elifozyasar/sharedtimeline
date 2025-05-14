<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Task Timeline</title>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.6.0/lib/p5.min.js"></script>
</head>
<body>
<script>
// Constants
let BASE_X = 190;
let BASE_Y = 30;
let RECT_W = 280;
let RECT_H = 100;
let SPACING_X = 70;
let SPACING_Y = 40;
let TASKS_PER_ROW = 5;
let RESIZE_HANDLE_SIZE = 10;
let CANCEL_HANDLE_SIZE = 20;
let state = 0;
let angles = [20, 40, 100];

// Global variables
let rectangles = [];
let selectedRectangle = null;
let addButton;
let conflictRects = [];
let dragStart;
let isResizing = false;
let isTyping = false;
let currentText = "";
let img1, img2;
let times = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  textFont('Arial', 20);
  img1 = loadImage('traffic.png');
  img2 = loadImage('weather.png');
  initializeRectangles();
  initializeAddButton();
}

function draw() {
  background(173, 216, 230);
  if (state === 0) {
    let nowH = hour() + minute() / 60.0;
    let GLOBAL_START_H = 8;
    let GLOBAL_END_H = 13;
    let GLOBAL_START_X = 150;
    let PIXELS_PER_HOUR = 420;
    let GLOBAL_END_X = GLOBAL_START_X + (GLOBAL_END_H - GLOBAL_START_H) * PIXELS_PER_HOUR;
    let highlightX = constrain(
      map(nowH, GLOBAL_START_H, GLOBAL_END_H, GLOBAL_START_X, GLOBAL_END_X),
      GLOBAL_START_X,
      GLOBAL_END_X
    );

    updateConflict();

    // Draw add button
    addButton.displayAddButton();

    // Sidebar blocks
    for (let i = 0; i < 4; i++) {
      let y = BASE_Y + i * (RECT_H + SPACING_Y) + 120;
      strokeWeight(2);
      fill(240, 225, 153);
      rect(20, y, 100, RECT_H);
    }

    // Bottom bar
    strokeWeight(4);
    stroke(0);
    fill(240, 225, 153);
    rect(width / 2 - 600, 850, 1200, 200);

    // Top-right panels
    strokeWeight(2);
    stroke(0);
    noFill();
    rect(width - 250, 10, 200, 100);
    stroke(200, 0, 0);
    image(img1, width - 280, -15, 160, 160);
    image(img2, width - 180, -15, 160, 160);
    rect(width - 240, 20, 75, 80);
    rect(width - 140, 20, 75, 80);

    // Draw all task rectangles
    rectangles.forEach(r => r.display(highlightX));

    // Highlight selected (blue)
    if (selectedRectangle) {
      selectedRectangle.displaySelected();
      selectedRectangle.displayHandles();
    }

    // Highlight conflicts (red)
    conflictRects.forEach(r => {
      noFill();
      stroke(200, 0, 0);
      strokeWeight(3);
      rect(r.x, r.y, r.w, r.h);
    });

    drawTextInput();
    drawTimeline();
  } else if (state === 1) {
    background(173, 216, 230);
    pieChart(700, angles);
  }
}

function pieChart(diameter, angArr) {
  let lastAngle = radians(30);
  angArr.forEach((a, i) => {
    let g = map(i, 0, angArr.length, 0, 255);
    fill(g);
    arc(width / 2, height / 2, diameter, diameter, lastAngle, lastAngle + radians(a));
    lastAngle += radians(a);
  });
}

function initializeAddButton() {
  addButton = new Rectangle(10, 10, 100, 50);
  addButton.isAddButton = true;
}

function initializeRectangles() {
  let numTasks = 20;
  for (let i = 0; i < numTasks; i++) {
    let col = i % TASKS_PER_ROW;
    let row = floor(i / TASKS_PER_ROW);
    let x0 = BASE_X + col * (RECT_W + SPACING_X);
    let y0 = BASE_Y + row * (RECT_H + SPACING_Y) + 120;
    rectangles.push(new Rectangle(x0, y0, RECT_W, RECT_H));
  }
}

function drawTimeline() {
  // background strip
  fill(255);
  stroke(0);
  strokeWeight(2);
  rect(0, 750, width, 60);

  // highlight up to current time
  let highlightX = 150 + ((hour() - 8) + minute() / 60.0) * 420;
  fill(240, 225, 153);
  rect(0, 750, highlightX, 60);

  // ticks and labels
  times = [];
  for (let h = 8; h < 13; h++) {
    for (let m = 0; m < 60; m++) {
      let xtime = 150 + ((h - 8) + m / 60.0) * 420;
      let label = nf(h, 2) + ':' + nf(m, 2);
      times.push({ text: label, x: xtime });
      if (m % 30 === 0) {
        fill(0);
        textSize(20);
        textAlign(CENTER, CENTER);
        text(label, xtime, 780);
      }
    }
  }
}

function drawTextInput() {
  fill(255);
  stroke(0);
  rect(600, 10, 600, 100);
  fill(0);
  textAlign(LEFT, TOP);
  textSize(16);
  text(currentText, 620, 20, 980, 80);
  if (isTyping && frameCount % 30 < 15) {
    let cursorX = 600 + textWidth(currentText) + 20;
    line(cursorX, 20, cursorX, 40);
  }
}

function mousePressed() {
  dragStart = createVector(mouseX, mouseY);
  // Add button
  if (addButton.contains(mouseX, mouseY)) {
    let nr = new Rectangle(mouseX - RECT_W / 2, mouseY - RECT_H / 2, RECT_W, RECT_H);
    rectangles.push(nr);
    selectRectangle(nr);
    saveState();
    return;
  }
  // Text input area
  if (mouseX < 410 && mouseY < 110) {
    isTyping = true;
    return;
  }
  // Toggle state (example condition)
  if (mouseX < -280 && mouseY > -15) {
    state = 1;
  } else {
    state = 0;
  }
  // Rectangle interactions
  for (let r of rectangles) {
    if (r.contains(mouseX, mouseY)) {
      if (r.isOverResizeHandle(mouseX, mouseY)) {
        isResizing = true;
      } else if (r.isOverCancelHandle(mouseX, mouseY)) {
        rectangles = rectangles.filter(x => x !== r);
        if (r === selectedRectangle) deselectCurrent();
        saveState();
      } else {
        selectRectangle(r);
      }
      return;
    }
  }
  // Deselect
  deselectCurrent();
  isTyping = false;
}

function mouseDragged() {
  if (!selectedRectangle) return;
  let dx = mouseX - dragStart.x;
  let dy = mouseY - dragStart.y;
  if (isResizing) {
    selectedRectangle.w = max(50, mouseX - selectedRectangle.x);
  } else {
    selectedRectangle.x += dx;
    selectedRectangle.y += dy;
  }
  dragStart.set(mouseX, mouseY);
  saveState();
}

function mouseReleased() {
  isResizing = false;
}

function keyPressed() {
  if (selectedRectangle) {
    if (keyCode === BACKSPACE) {
      currentText = currentText.slice(0, -1);
    } else if (keyCode === ENTER) {
      selectedRectangle.text = currentText;
      saveState();
    } else if (key.length === 1) {
      currentText += key;
    }
  }
}

function selectRectangle(rect) {
  deselectCurrent();
  selectedRectangle = rect;
  currentText = rect.text;
  isTyping = true;
}

function deselectCurrent() {
  selectedRectangle = null;
  currentText = "";
  isTyping = false;
}

function updateConflict() {
  conflictRects = [];
  for (let i = 0; i < rectangles.length; i++) {
    let r1 = rectangles[i];
    if (!r1.text || !r1.text.trim()) continue;
    for (let j = i + 1; j < rectangles.length; j++) {
      let r2 = rectangles[j];
      if (!r2.text || r1.text !== r2.text) continue;
      let overlap = (r1.x < r2.x + r2.w) && (r1.x + r1.w > r2.x);
      if (overlap) {
        conflictRects.push(r1, r2);
      }
    }
  }
}

function saveState() {
  let stateObj = { rectangles: [] };
  rectangles.forEach(r => {
    stateObj.rectangles.push({ text: r.text, x: r.x, y: r.y, width: r.w, height: r.h });
  });
  localStorage.setItem('rectangle_state', JSON.stringify(stateObj));
}

// Rectangle class
class Rectangle {
  constructor(x, y, w, h) {
    this.x = x;
    this.y = y;
    this.w = w;
    this.h = h;
    this.text = "";
    this.isAddButton = false;
  }

  display(highlightX) {
    stroke(0);
    strokeWeight(2);
    fill(225);
    rect(this.x, this.y, this.w, this.h);
    let fillW = constrain(highlightX - this.x, 0, this.w);
    if (fillW > 0) {
      fill(240, 225, 153);
      rect(this.x, this.y, fillW, this.h);
    }
    if (this.text) {
      fill(0);
      textSize(20);
      textAlign(CENTER, CENTER);
      text(this.text, this.x + this.w / 2, this.y + this.h / 2);
    }
  }

  displayAddButton() {
    fill(255);
    stroke(0);
    strokeWeight(2);
    rect(this.x, this.y, this.w, this.h);
    strokeWeight(3);
    let cx = this.x + this.w / 2;
    let cy = this.y + this.h / 2;
    line(cx - 20, cy, cx + 20, cy);
    line(cx, cy - 20, cx, cy + 20);
  }

  displaySelected() {
    noFill();
    stroke(0, 0, 255);
    strokeWeight(3);
    rect(this.x, this.y, this.w, this.h);
  }

  displayHandles() {
    fill(255, 0, 0);
    stroke(0);
    let hs = RESIZE_HANDLE_SIZE;
    rect(this.x + this.w - hs, this.y + this.h - hs, hs*2, hs*2);
    stroke(255, 0, 0);
    strokeWeight(3);
    let cs = CANCEL_HANDLE_SIZE;
    line(this.x - cs, this.y - cs, this.x + cs, this.y + cs);
    line(this.x + cs, this.y - cs, this.x - cs, this.y + cs);
  }

  contains(px, py) {
    return px >= this.x && px <= this.x + this.w && py >= this.y && py <= this.y + this.h;
  }

  isOverResizeHandle(px, py) {
    let hs = RESIZE_HANDLE_SIZE;
    return px >= this.x + this.w - hs && px <= this.x + this.w + hs && px >= this.y + this.h - hs && py <= this.y + this.h + hs;
  }

  isOverCancelHandle(px, py) {
    let dx = px - this.x;
    let dy = py - this.y;
    return abs(dx) <= CANCEL_HANDLE_SIZE && abs(dy) <= CANCEL_HANDLE_SIZE;
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
</script>
</body>
</html>
