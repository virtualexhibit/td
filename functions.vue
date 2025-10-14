methods: {
  clickCompute() {
    if (this.personCount >= 2) {
      alert('Computed person reached the limit of 2. Compare or Reset.')
      return
    }

    if (!this.validateInputs()) {
      alert('⚠️ Please enter valid Name, Weight, and Height.')
      return
    }

    const bmi = this.computeBmi()
    const category = this.getCategory(bmi)
    this.savePersonData(bmi, category)
    this.updateLabelGuide()
    this.emitPersonDetails()
    this.resetInputs()
  },

  // ✅ Separate helper for input validation
  validateInputs() {
    const WeightKg = parseFloat(this.userInputs.weight)
    const HeightCm = parseFloat(this.userInputs.height)
    const name = this.userInputs.name.trim()

    if (
      !name ||
      isNaN(WeightKg) ||
      isNaN(HeightCm) ||
      HeightCm <= 0 ||
      WeightKg <= 0 ||
      HeightCm > 200 ||
      WeightKg > 200 ||
      /\d/.test(name) ||
      /[^\w\s]/.test(name)
    ) {
      return false
    }
    return true
  },

  // ✅ Separate helper to compute BMI
  computeBmi() {
    const WeightKg = parseFloat(this.userInputs.weight)
    const HeightCm = parseFloat(this.userInputs.height)
    const HeightM = HeightCm / 100
    return parseFloat((WeightKg / (HeightM * HeightM)).toFixed(2))
  },

  // ✅ Separate helper for BMI category
  getCategory(bmi) {
    if (bmi < 18.5) return 'Underweight'
    else if (bmi < 25) return 'Normal weight'
    else if (bmi < 30) return 'Overweight'
    else return 'Obese'
  },

  // ✅ Separate helper to store computed data
  savePersonData(bmi, category) {
    this.personCount++

    const newPerson = {
      person: this.personCount,
      name: this.userInputs.name,
      weight: this.userInputs.weight,
      height: this.userInputs.height,
      bmi,
      category,
    }

    this.computedPeople.push(newPerson)
    this.personDetails[`person${this.personCount}`] = {
      name: newPerson.name,
      bmi: newPerson.bmi,
      category: newPerson.category,
    }

    console.log(
      `Person ${this.personCount}\n` +
        `Name: ${newPerson.name}\n` +
        `Weight: ${newPerson.weight} kg\n` +
        `Height: ${newPerson.height} cm\n` +
        `BMI: ${newPerson.bmi}\n` +
        `Category: ${newPerson.category}\n`
    )
  },

  // ✅ Separate helper to update UI instruction label
  updateLabelGuide() {
    if (this.personCount === 1) {
      this.labelGuide = 'Nice. Enter details for Person 2'
    } else if (this.personCount === 2) {
      this.labelGuide = 'Great. You can now compare Person 1 & 2'
    }
  },

  // ✅ Separate helper to emit data upward
  emitPersonDetails() {
    this.$emit('personDetails', this.personDetails)
  },

  // ✅ Separate helper to reset form inputs
  resetInputs() {
    this.userInputs = { name: '', weight: '', height: '' }
  },
}

///////////////////////////

savePersonData(bmi, category) {
  this.personCount++

  const trimmedName = this.userInputs.name.trim()

  const newPerson = {
    person: this.personCount,
    name: trimmedName,
    weight: this.userInputs.weight,
    height: this.userInputs.height,
    bmi,
    category,
  }

  this.computedPeople.push(newPerson)
  this.personDetails[`person${this.personCount}`] = {
    name: newPerson.name,
    bmi: newPerson.bmi,
    category: newPerson.category,
  }

  console.log(
    `Person ${this.personCount}\n` +
      `Name: ${trimmedName}\n` +
      `Weight: ${newPerson.weight} kg\n` +
      `Height: ${newPerson.height} cm\n` +
      `BMI: ${newPerson.bmi}\n` +
      `Category: ${newPerson.category}\n`
  )
}

or

clickCompute() {
  // sanitize text fields
  this.userInputs.name = this.userInputs.name.trim()
  