<template>
  <h1>Smash Rankings</h1>

  <table>
    <thead>
      <tr>
        <th>Rank</th>
        <th>Player</th>
        <th>Character(s)</th>
        <th>Record</th>
        <th>Score</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="player in players" :key="player.rank">
        <td>{{ player.rank }}</td>
        <td>{{ player.player }}</td>
        <td>
          <span v-for="char in player.characters" :key="char.name" style="margin-right: 8px">
            <img :src="ICON_PATH + char.icon" :alt="char.name" class="character-icon" />
          </span>
        </td>
        <td>{{ player.win }} - {{ player.loss }}</td>
        <td>{{ player.score }}<span v-if="player.win + player.loss < 20">?</span></td>
      </tr>
    </tbody>
  </table>
  <footer>
    <p>
      <a href="https://github.com/joey-bednar/smash-leaderboard">GitHub</a> &mdash; Last Modified:
      July 20, 2025
    </p>
  </footer>
</template>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #000103;
  margin: 20px;
}

h1 {
  text-align: center;
  color: #fffffa;
}

table {
  width: 80%;
  margin: 0 auto;
  border-collapse: collapse;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  background-color: #515052;
  color: #fffffa;
}

th,
td {
  padding: 12px 15px;
  text-align: center;
  border-bottom: 1px solid #2d2d2c;
}

th {
  background-color: #ff312e;
  color: #fffffa;
}

tr:hover {
  background-color: #333138;
}

.character-icon {
  height: 18px;
  width: 18px;
  vertical-align: middle;
}

footer {
  text-align: center;
  margin-top: 40px;
  font-size: 14px;
  color: #555;
}

footer a {
  color: #3c4c63;
  text-decoration: none;
}

footer a:hover {
  text-decoration: underline;
}
</style>

<script setup>
import { ref, onMounted } from 'vue'

const ICON_PATH = 'ssbuicons/'

const players = ref([])

onMounted(async () => {
  const res = await fetch('/data.json')
  const data = await res.json()

  // Sort players by score descending
  data.sort((a, b) => b.score - a.score)

  let lastScore = null
  let lastRank = 0

  data.forEach((player, index) => {
    if (player.score !== lastScore) {
      lastRank = index + 1
      lastScore = player.score
    }
    player.rank = lastRank
  })

  // // Assign rank based on sorted position
  // data.forEach((player, index) => {
  //   player.rank = index + 1
  // })

  players.value = data
})
</script>
