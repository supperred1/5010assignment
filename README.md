# 5010assignment

```
let agents = []
let count = 300

function setup() {
  createCanvas(800, 800)

  for (let i = 0; i < count; i++) {
    let agent = {
      pos: createVector(random(width), random(height)),
      vel: p5.Vector.random2D(),
      acc: createVector(0, 0),
      maxSpeed: 2,

      update() {
        let mouse = createVector(mouseX, mouseY)
        let force = p5.Vector.sub(mouse, this.pos)

        force.setMag(0.1) 
        this.acc.add(force)

        this.vel.add(this.acc)
        this.vel.limit(this.maxSpeed)
        this.pos.add(this.vel)
        this.acc.mult(0)
      },

      draw() {
        textSize(40)
        text("😀",this.pos.x, this.pos.y)
      }
    }

    agents.push(agent)
  }

}

function draw() {
  background(0)

  agents.forEach(a => {
    a.update()
    a.draw()
  })
}

function mousePressed() {
  let mouse = createVector(mouseX, mouseY)

  agents.forEach(a => {
    let dir = p5.Vector.sub(a.pos, mouse)
    dir.setMag(random(5, 10)) 
    a.vel = dir
  })
}
```
I replaced all the point to 😀,and assign a force to each point directed toward the mouse position (by subtracting the particle's position from the mouse position), then apply an acceleration to the particle while limiting its maximum speed. After that, clear the acceleration using this.acc.mult(0) (to prevent excessive speed). Finally, when the mouse clicks on the screen, the particles will move away from the mouse (by subtracting the mouse position from the particle's position).
