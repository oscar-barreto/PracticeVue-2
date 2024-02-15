<script>
  export default{
    data() {
                return { 
                    characters: [
                        { name: 'Aang', element: ['Air', 'Earth', 'Fire', 'Water'] },
                        { name: 'Zuko', element: ['Fire'] },
                        { name: 'Toph', element: ['Earth'] },
                        { name: 'Katara', element: ['Water'] },
                        { name: 'Soka', element: [] }
                    ],
                    count: 0,
                    incrementAmount: 1,
                    counterTitle: 'Counter: '
                }
            },
            computed: {
                benderStatistics() {
                    const statistics = { Earth: 0, Air: 0, Water: 0, Fire: 0 };
                    this.characters.forEach(character => {
                        character.element.forEach(element => {
                            if (statistics.hasOwnProperty(element)) {
                                statistics[element]++;
                            }
                        });
                    });
                    return statistics;
                }
            },
            methods: {
                incrementCount() {
                    this.count += this.incrementAmount;
                },
                decrementCount() {
                    if (this.count > 0) {
                        this.count--;
                    }
                },
                changeIncrementAmount(event) {
                    this.incrementAmount = Number(event.target.value);
                }
            },
            watch: {
                count(newValue) {
                    if (newValue > 20) {
                        this.counterTitle += 'Very Long';
                    }
                }
            }
  }
</script>

<template>
  <h2>{{ benderStatistics }}</h2>
        <ul>
            <li>Earth: {{ benderStatistics.Earth }}</li>
            <li>Air: {{ benderStatistics.Air }}</li>
            <li>Water: {{ benderStatistics.Water }}</li>
            <li>Fire: {{ benderStatistics.Fire }}</li>
        </ul>
        <h2>Characters</h2>
        <p v-if="characters.length === 0">There are no characters</p>
        <ul v-else >
            <li v-for="character in characters">{{ character.name }}</li>
        </ul>
        <div>
            <p>Count: <span>{{ count }}</span></p>
            <h3>{{ incrementAmount }}</h3>
            <h2>{{ counterTitle }}</h2>
            <button @click="incrementCount">Increment</button>
            <button @click="decrementCount">Decrement</button>
            <label for="IncrementAmount">Increment Amount:</label>
            <input type="number" @input="changeIncrementAmount" v-model.number="incrementAmount">
        </div>
       
</template>
