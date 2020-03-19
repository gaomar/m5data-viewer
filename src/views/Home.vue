<template>
  <v-container>
    <v-layout
      text-center
      wrap
    >
      <v-flex xs12>
        <v-card>
            <v-container fluid grid-list-lg>
            <v-layout row wrap>
                <v-flex xs12>
                <v-card color="blue-grey darken-2" class="white--text">
                    <v-card-title primary-title>
                    <div>
                        <div class="headline">M5Stackカウンター：{{this.countM5Stack}}</div>
                    </div>
                    </v-card-title>
                </v-card>
                </v-flex>
            </v-layout>
            <v-layout row wrap>
                <v-flex xs12>
                <v-card color="blue-grey darken-2" class="white--text">
                    <v-card-title primary-title>
                    <div>
                        <div class="headline">M5StickCカウンター：{{this.countM5Stick}}</div>
                    </div>
                    </v-card-title>
                </v-card>
                </v-flex>
            </v-layout>
            </v-container>
        </v-card>
      </v-flex>

    </v-layout>
  </v-container>
</template>

<script>
import firebase from '../plugins/firebase'

export default {
  data () {
    return {
        countM5Stack: "--",
        countM5Stick: "--",
        countM5StackRef: null,
        countM5StickRef: null
    }
  },
  created () {
      this.firebaseInit()
  },
  methods: {
    firebaseInit () {
        // M5StackとM5StickCの内容を取得
        this.countM5StackRef = firebase.database().ref('M5Stack')
        this.countM5StickRef = firebase.database().ref('M5StickC')

        // M5Stackの値をリアルタイム反映させる
        this.countM5StackRef.on('value', (snapshot) => {
            this.countM5Stack = snapshot.val().counter
        })

        // M5StickCの値をリアルタイム反映させる
        this.countM5StickRef.on('value', (snapshot) => {
            this.countM5Stick = snapshot.val().counter
        })

    }
  }
}
</script>