# pong
import turtle
from time import sleep

window = turtle.Screen()                        # Open the turtle app
window.title("Yamani PONG")                    # The title name
window.bgcolor("light blue")                    # The color of the background
window.setup(width=800, height=400)             # the window dimensions
window.tracer(0)                                # to stop updating, make it faster


# padle A
padle_a = turtle.Turtle()                           # Name the padle A & make it turtle object
padle_a.speed(0)                                    # The speed of the animation for padle A
padle_a.shape("square")                             # Give padle A a shape, there are some built in shapes in turtle
padle_a.color("black")                              # Give padle A a color
padle_a.shapesize(stretch_wid=5, stretch_len=1)      # change the shape length & width
padle_a.penup()
padle_a.goto(-350, 0)


# Padle B
padle_b = turtle.Turtle()                            # Name the padle B & make it turtle object
padle_b.speed(0)                                     # The speed of the animation for padle B
padle_b.shape("square")                              # Give padle B a shape, there are some built in shapes in turtle
padle_b.color("black")                               # Give padle B a color
padle_b.shapesize(stretch_wid=5, stretch_len=1)      # change the shape length & width
padle_b.penup()
padle_b.goto(350, 0)

# Ball
ball = turtle.Turtle()                   # Name the padle B & make it turtle object
ball.speed(0)                            # The speed of the animation for padle B
ball.shape("circle")                     # Give padle B a shape, there are some built in shapes in turtle
ball.color("black")                      # Give padle B a color
ball.penup()
ball.goto(0, 0)
ball.dx = 1                             # to make the ball start moving on its own by dx distance of
ball.dy = 1                             # to make the ball start moving on its own by dy distance

# score
score_a = 0
score_b = 0
score = turtle.Turtle()
score.speed(0)
score.color("White")
score.penup()
score.goto(0, 160)
score.write(":{} الحضرمي الساحلي :{}                الحضرمي العالمي   ".format(score_a, score_b), align="center", font=("Courier ", 24, "normal"))


def padle_a_up():
    y = padle_a.ycor()
    y += 40
    padle_a.sety(y)


def padle_a_down():
    y = padle_a.ycor()
    y -= 40
    padle_a.sety(y)


def padle_b_up():
    y = padle_b.ycor()
    y += 40
    padle_b.sety(y)


def padle_b_down():
    y = padle_b.ycor()
    y -= 40
    padle_b.sety(y)


# Keyboard binding
window.listen()                             # to make the window listen to what was typed on the keyboard
window.onkeypress(padle_a_up, "w")          # pass the function without() then the
window.onkeypress(padle_a_down, "s")
window.onkeypress(padle_b_up, "Up")
window.onkeypress(padle_b_down, "Down")

time = 0
# main fame loop
while score_a <= 10 or score_b <= 10:
    window.update()                     # to update the window

    # move the ball
    ball.setx(ball.xcor() + ball.dx)
    ball.sety(ball.ycor() + ball.dy)

    # Border check for y & x
    if ball.ycor() > 190:               # if it reaches the positive boarder
        ball.sety(190)                  # set the y to
        ball.dy *= -1                   # make it move inversly

    if ball.ycor() < -190:              # if it reaches the negative boarderw
        ball.sety(-190)                 # set y to
        ball.dy *= -1                   # make it move inversly

    if ball.xcor() > 390:               # if it reaches the end of the boarder
        ball.goto(0, 0)                 # make it go to the center
        ball.dx *= -1                   # and move it the other way
        score_a += 1
        score.clear()
        score.write(":{} الحضرمي الساحلي :{}                الحضرمي العالمي   ".format(score_a, score_b), align="center",font=("Courier ", 24, "normal"))

    if ball.xcor() < -390:
        ball.goto(0, 0)
        ball.dx *= -1
        score_b += 1
        score.clear()
        score.write(":{} الحضرمي الساحلي :{}                الحضرمي العالمي   ".format(score_a, score_b), align="center", font=("Courier ", 24, "normal"))

    # ball & padle collision
    # check if the ball is beyond the paddle in the x axis && check the y cordinates if its within the y padle
    if (ball.xcor() > 340 and ball.xcor() < 350) and (ball.ycor() < padle_b.ycor() + 50 and ball.ycor() > padle_b.ycor() - 50):
        ball.setx(340)
        ball.dx *= -1

    # check if the ball is beyond the paddle in the x axis && check the y cordinates if its within the y padle
    if (ball.xcor() <  -340 and ball.xcor() > -350) and (ball.ycor() < padle_a.ycor() + 50 and ball.ycor() > padle_a.ycor() - 50):
        ball.setx(-340)
        ball.dx *= -1

    if score_a >= 10 or score_b >= 10:
        b = turtle.Turtle()
        b.speed(0)
        b.color("White")
        b.penup()
        b.goto(0, 0)
        if score_a >= 10:
            b.write("الحضرمي العالمي فاز عليك" , align="center", font=("Courier ", 36, "normal"))
        else:
            b.write("الحضرمي الساحلي فاز عليك", align="center", font=("Courier ", 36, "normal"))
        sleep(10)
        break
        
