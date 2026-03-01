# 5010assignment

```
let agents = []
let count = 500

function setup() {
  createCanvas(400, 400)

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
        noStroke()
        fill(random(0,255))
        circle(this.pos.x, this.pos.y,10)
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
