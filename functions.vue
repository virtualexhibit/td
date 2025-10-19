comparePeople() {
  if (this.computedPeople.length < 2) return

  for (let i = 0; i < this.computedPeople.length - 1; i++) {
    const p1 = this.computedPeople[i]
    const p2 = this.computedPeople[i + 1]
    console.log(`${p1.name} vs ${p2.name}`)
    console.log(`${p1.bmi > p2.bmi ? p1.name : p2.name} has higher BMI.`)
  }
}