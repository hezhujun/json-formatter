<script setup lang="ts">
import { computed, ref } from "vue"
import JsonViewer from './components/JsonViewer.vue'

const inputRef = ref('')

function parseString(input:string): string {
  if (input.length == 0) {
    return input
  }

  if (input[0] == "'" || input[0] == '"') {
    let ret = ""
    for (let index = 1; index < input.length - 1; index++) {
      const element = input[index];
      if (element == "\\" && index + 1 < input.length - 1) {
        ret += input[index + 1]
        index++
      } else {
        ret += element
      }
    }
    return ret
  } else {
    return input
  }
}

const jsonData = computed(() => {
  const input = inputRef.value
  console.log(`input: ${input}`)
  const parsedString = parseString(input);
  console.log(`parsed string: ${parsedString}`)
  if (parsedString.length == 0) {
    return {}
  }
  try {
    return JSON.parse(parsedString)
  } catch (error) {
    console.error(error)
    return {}
  }
  
})

const jsonData2 = ref({
        total: 25,
        limit: 10,
        skip: 0,
        links: {
          previous: undefined,
          next: function () {},
        },
        data: [
          {
            id: '5968fcad629fa84ab65a5247',
            firstname: 'Ada',
            lastname: 'Lovelace',
            awards: null,
            known: [
              'mathematics',
              'computing'
            ],
            position: {
              lat: 44.563836,
              lng: 6.495139
            },
            description: `Augusta Ada King, Countess of Lovelace (née Byron; 10 December 1815 – 27 November 1852) was an English mathematician and writer,
            chiefly known for her work on Charles Babbage's proposed mechanical general-purpose computer,
            the Analytical Engine. She was the first to recognise that the machine had applications beyond pure calculation,
            and published the first algorithm intended to be carried out by such a machine.
            As a result, she is sometimes regarded as the first to recognise the full potential of a "computing machine" and the first computer programmer.`,
            bornAt: '1815-12-10T00:00:00.000Z',
            diedAt: '1852-11-27T00:00:00.000Z'
          }, {
            id: '5968fcad629fa84ab65a5246',
            firstname: 'Grace',
            lastname: 'Hopper',
            awards: [
              'Defense Distinguished Service Medal',
              'Legion of Merit',
              'Meritorious Service Medal',
              'American Campaign Medal',
              'World War II Victory Medal',
              'National Defense Service Medal',
              'Armed Forces Reserve Medal',
              'Naval Reserve Medal',
              'Presidential Medal of Freedom'
            ],
            known: null,
            position: {
              lat: 43.614624,
              lng: 3.879995
            },
            description: `Grace Brewster Murray Hopper (née Murray; December 9, 1906 – January 1, 1992)
            was an American computer scientist and United States Navy rear admiral.
            One of the first programmers of the Harvard Mark I computer,
            she was a pioneer of computer programming who invented one of the first compiler related tools.
            She popularized the idea of machine-independent programming languages, which led to the development of COBOL,
            an early high-level programming language still in use today.`,
            bornAt: '1815-12-10T00:00:00.000Z',
            diedAt: '1852-11-27T00:00:00.000Z'
          }
        ]
      })
</script>

<template>
	<textarea class="input" v-model="inputRef" placeholder="输入 JSON 内容"></textarea>

  <JsonViewer :value="jsonData"></JsonViewer>
</template>


<style scoped>

.input {
  width: 99%;
  height: 300px;
}

</style>
