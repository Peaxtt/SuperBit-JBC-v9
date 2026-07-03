# JBC Robot — Practice Slides

---

## 🟣 Zone 1: เริ่มต้น — หุ่นพร้อม

### Practice 1.1 — เปิดหุ่น

```python
JBC.initRobot(67)
```

> หุ่นจะแสดง 😴 ระหว่างเตรียม แล้วแสดง 😊 เมื่อพร้อม
> ต้องรันบรรทัดนี้ก่อนทุกครั้ง ไม่งั้นหุ่นไม่ทำงาน

---

### Practice 1.2 — เดินตรง หยุด

```python
JBC.initRobot(67)

JBC.moveStraight(150, 2000)
```

> หุ่นเดินตรง 2 วินาที แล้วหยุดเอง
> ลองเปลี่ยน `2000` เป็น `500`, `1000`, `3000` — สังเกตว่าหุ่นเดินนานแค่ไหน

---

### Practice 1.3 — ปรับความเร็ว

```python
JBC.initRobot(67)

JBC.moveStraight(50, 2000)
JBC.moveStraight(150, 2000)
JBC.moveStraight(255, 2000)
```

> เดิน 3 รอบ ความเร็วต่างกัน 50 → 150 → 255
> สังเกตว่าความเร็วต่างกันแค่ไหน
> **ห้ามใส่เกิน 255**

---

## 🟣 Zone 2: เลี้ยว

### Practice 2.1 — หมุนขวา 90°

```python
JBC.initRobot(67)

JBC.turnDegrees(90)
```

> หุ่นหมุนขวา 90 องศา
> ลองเปลี่ยนเป็น `45`, `180`, `360`

---

### Practice 2.2 — หมุนซ้าย

```python
JBC.initRobot(67)

JBC.turnDegrees(-90)
```

> ใส่เลขติดลบ = หมุนซ้าย

---

### Practice 2.3 — เดินตรงแล้วเลี้ยว

```python
JBC.initRobot(67)

JBC.moveStraight(150, 2000)
basic.pause(500)
JBC.turnDegrees(90)
basic.pause(500)
JBC.moveStraight(150, 2000)
```

> เดินตรง → หยุดรอ → หมุนขวา → เดินตรงต่อ
> `basic.pause(500)` คือรอ 0.5 วินาที ให้หุ่นนิ่งก่อนทำสิ่งต่อไป

---

### Practice 2.4 — วนสี่เหลี่ยม

```python
JBC.initRobot(67)

JBC.moveStraight(150, 2000)
basic.pause(300)
JBC.turnDegrees(90)
basic.pause(300)
JBC.moveStraight(150, 2000)
basic.pause(300)
JBC.turnDegrees(90)
basic.pause(300)
JBC.moveStraight(150, 2000)
basic.pause(300)
JBC.turnDegrees(90)
basic.pause(300)
JBC.moveStraight(150, 2000)
basic.pause(300)
JBC.turnDegrees(90)
```

> หุ่นเดินเป็นรูปสี่เหลี่ยม 4 ด้าน แล้วกลับมาหน้าเดิม
> ถ้าหุ่นไม่กลับมาจุดเดิมพอดี → ลองปรับเวลา `2000` ให้เท่ากัน

---

## 🟣 Zone 3: อ่านค่า Heading

### Practice 3.1 — ดู heading ใน Data Viewer

```python
JBC.initRobot(67)

def on_forever():
    JBC.plot("heading", JBC.currentHeading())

basic.forever(on_forever)
```

> เสียบ USB → MakeCode → Show data Device
> กราฟจะแสดง heading ของหุ่น
> หมุนหุ่นด้วยมือ แล้วดูกราฟเปลี่ยน

---

### Practice 3.2 — ดู heading และ correction พร้อมกัน

```python
JBC.initRobot(67)

def on_forever():
    JBC.plot("heading", JBC.currentHeading())
    JBC.plot("correction", JBC.correction())

basic.forever(on_forever)
```

> `correction` คือค่าที่ PID สั่งมอเตอร์ให้ปรับทิศ
> ถ้า heading ตรงเป้า correction จะใกล้ 0

---

### Practice 3.3 — เดินตรงแล้วดู heading

```python
JBC.initRobot(67)

JBC.moveStraight(150, 3000)

def on_forever():
    JBC.plot("heading", JBC.currentHeading())

basic.forever(on_forever)
```

> ดูว่า heading เปลี่ยนแค่ไหนขณะเดินตรง
> ถ้า IMU ทำงานดี heading ควรใกล้ 0 ตลอด

---

## 🟣 Zone 4: Reset Heading

### Practice 4.1 — reset แล้วหมุน

```python
JBC.initRobot(67)

JBC.turnDegrees(90)
basic.pause(500)
JBC.resetHeading()
basic.pause(500)
JBC.turnDegrees(90)
```

> หมุนขวา 90° → reset → หมุนขวาอีก 90°
> หลัง reset หุ่นถือว่าทิศปัจจุบันคือ 0 ใหม่
> ผลลัพธ์ = หมุนรวม 180° จากเริ่มต้น

---

### Practice 4.2 — reset ก่อนเริ่ม sequence

```python
JBC.initRobot(67)
JBC.resetHeading()

JBC.moveStraight(150, 2000)
basic.pause(300)
JBC.turnDegrees(90)
basic.pause(300)
JBC.moveStraight(150, 2000)
```

> reset ทันทีหลัง init เพื่อให้แน่ใจว่า heading เริ่มที่ 0
> แนะนำให้ทำทุกครั้งที่เริ่ม sequence ใหม่

---

## 🟣 Zone 5: คีม (Gripper)

### Practice 5.1 — หุบและแบคีม

```python
JBC.initRobot(67)

JBC.closeGripper()
basic.pause(1000)
JBC.openGripper()
```

> คีมหุบ รอ 1 วินาที แล้วแบ
> servo เคลื่อนช้าๆ ไม่กระตุก

---

### Practice 5.2 — เดินไปหยิบของ

```python
JBC.initRobot(67)
JBC.openGripper()
basic.pause(500)

JBC.moveStraight(150, 1500)
basic.pause(300)
JBC.closeGripper()
basic.pause(800)
JBC.moveStraight(-150, 1500)
```

> เปิดคีม → เดินเข้าหาของ → หุบคีม → ถอยหลัง
> `moveStraight(-150, ...)` = เดินถอยหลัง

---

## 🟣 Zone 6: รับคำสั่งจาก Joystick

### Practice 6.1 — Robot รอรับคำสั่ง

```python
JBC.initRobot(67)

def on_cmd_1():
    JBC.moveStraight(150, 2000)

def on_cmd_2():
    JBC.turnDegrees(90)

def on_cmd_3():
    JBC.robotStop()

JBC.onCmdReceived(1, on_cmd_1)
JBC.onCmdReceived(2, on_cmd_2)
JBC.onCmdReceived(3, on_cmd_3)
```

> หุ่นรอรับคำสั่งจาก Joystick ผ่าน radio
> กด A → เดินตรง, กด B → หมุน, กด A+B → หยุด

---

### Practice 6.2 — Joystick ส่งคำสั่ง

```python
JBCJoystick.init(67)

def on_button_a():
    JBCJoystick.sendCmd(1)

def on_button_b():
    JBCJoystick.sendCmd(2)

def on_button_ab():
    JBCJoystick.sendCmd(3)

input.on_button_pressed(Button.A, on_button_a)
input.on_button_pressed(Button.B, on_button_b)
input.on_button_pressed(Button.AB, on_button_ab)
```

> flash อันนี้ลงบน micro:bit ตัวที่ถือในมือ
> ตัวเลข cmd ต้องตรงกับที่ Robot รอรับ

---

## 🟣 Zone 7: ปิด IMU

### Practice 7.1 — เดินตรงโดยไม่ใช้ IMU

```python
JBC.initRobot(67)
JBC.setImu(False)

JBC.moveStraight(150, 2000)
```

> ปิด IMU → หุ่นเดินโดยไม่ปรับทิศ
> เปรียบเทียบกับเปิด IMU ว่าต่างกันแค่ไหน

---

### Practice 7.2 — เปรียบเทียบ IMU on/off

```python
JBC.initRobot(67)

JBC.setImu(True)
JBC.moveStraight(150, 3000)
basic.pause(1000)

JBC.resetHeading()
JBC.setImu(False)
JBC.moveStraight(150, 3000)
```

> รอบแรก IMU เปิด — หุ่นพยายามเดินตรง
> รอบสอง IMU ปิด — หุ่นเดินตามมอเตอร์ล้วนๆ
> สังเกตว่าหุ่นเบี้ยวต่างกันไหม

---

## สรุป block ที่ใช้ทั้งหมด

| Block | หน้าที่ |
|-------|--------|
| `JBC.initRobot(67)` | เตรียมหุ่น — ใส่ทุกครั้ง |
| `JBC.moveStraight(speed, ms)` | เดินตรง (speed ลบ = ถอย) |
| `JBC.turnDegrees(deg)` | หมุน (บวก=ขวา ลบ=ซ้าย) |
| `JBC.robotStop()` | หยุด |
| `JBC.closeGripper()` | หุบคีม |
| `JBC.openGripper()` | แบคีม |
| `JBC.currentHeading()` | อ่าน heading ปัจจุบัน |
| `JBC.resetHeading()` | reset heading เป็น 0 |
| `JBC.correction()` | ค่า PID output |
| `JBC.plot("name", value)` | ส่งค่าขึ้น Data Viewer |
| `JBC.setImu(True/False)` | เปิด/ปิด IMU |
| `JBC.onCmdReceived(n, fn)` | รับคำสั่งจาก Joystick |
