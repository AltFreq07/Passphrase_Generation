<template>
  <v-app dark>
    <v-main>
      <br />
      <v-container>
        <v-btn color="primary" @click="generatePassword()"
          >Generate Mneumonic Password</v-btn
        ><br /><br />
        <v-textarea
          v-model="generatedPassword"
          outlined
          name="input-7-4"
          label="Generated Password"
          readonly
        ></v-textarea>
        <span
          >Generates a mneumonic password using the
          <a href="https://www.eff.org/document/passphrase-wordlists"
            >EFF Wordlist</a
          >
          containing 7776 words and aims to produce a password with greater than
          256 entropy as defined by log2(7776^20). This wordlist results in
          higher entropy for less words as seen
          <a href="https://coldbit.com/can-bip-39-passphrase-be-cracked/"
            >here</a
          > </span
        ><br /><br />*Note the hash function used here is weaker than
        Argon2id*<br /><br />
        <v-img src="/classes.png"></v-img>
        <v-img src="bip39.png"></v-img>
        <v-img src="dice.png"></v-img>
      </v-container>
    </v-main>
  </v-app>
</template>
<script>
import EFFDicewarePassphrase from '@small-tech/eff-diceware-passphrase'

export default {
  data() {
    return {
      generatedPassword: '',
    }
  },
  methods: {
    generatePassword() {
      console.log('Loading')
      // console.log(Generate.words(8))

      const generate = new EFFDicewarePassphrase()
      const passphrase = generate.entropy(256)
      this.generatedPassword = passphrase.join(' ')
    },
  },
}
</script>
