<template>
    <div class="my-class">
        <div>
    <h1> part 1 Template Syntax</h1>
    
    <span>My Message: {{ msg }}</span> 
    <!-- text interpolation, the msg is from the msg constant declared in the js block -->
    <p>Using directives to get html into the span: <span v-html="myHtml"></span></p>
    <!-- using v-html to change the spans message and colour -->
    <div :id="myMessage.id"> </div>
    <!-- binding this div id to the id of myMessage object so inputs can be linked to this object specifically -->
    <p> num is: {{ num }} and num + num is: {{ num + num }} is num > 2?: {{ num > 2 ? 'YES' : 'NO' }}</p>
    <!-- num, num added to num and compared to 2 -->
    <a @click="num++">click</a>
    <p>{{ num }} is now increasing</p>
    </div>

    <div >
        <h1>part 2 Raw HTML</h1>
        <div v-for="i in myList">
            <slot v-if="i % 2"> {{ i }} is %2</slot>
        </div>
    </div>

    <div>
        <h1>part 3 Reactivity Fundmentals</h1>

        <div>counter from other component
            <p>{{ counter }}</p>
        </div>
        <button @click="state.count++">
        {{ state.count }}
        </button>


    </div>

    <div>
        <h1>Part 4 - Computed Properties</h1>
        <div>
            <p>computed reference</p>
            <p> {{ mylistx3 }}</p>
            <!-- use the computed reference to compute data for elements that you might need to use a few
             times in the template, so teh data is processed once, chached and kept ready to use again. -->
            <!-- checking to see if the 3rd value in mylist *7 is more than 5 -->
            <!-- computed are getter only, unless you specify setter as well -->
            <p>

            </p>

        </div>
    </div>

    <div>
        <h1>Part 5 - Class and Style Bindings</h1>
        <div>
            <ul v-for="i in myObjects" :key="id">
                <li :class="{ boring: i.boring, twoerrors: i.veryBoring }" 
                :style="{ 'font-size': num + 10 + 'px' }"> boring?: {{ i.boring }}</li>
            </ul>
                <!-- rendering the elements in different style depending on their properties -->
                <!-- the font will change depending on the number of num from the previous part -->
        </div>
        <ul>
            <li v-for="item in myObjects"
            :key="item.id"
            @click="changeBoring(item)"
            :class="{ boring: item.boring, twoerrors: item.veryBoring}">
                {{ item.id }}
                
            </li>
        <!-- clicking the button changes the objects boring value, and changes how it is displayed -->
        </ul>

        <ul>
            <li v-for="item in myObjects"
            :key="item.id"
            :class="item.objclass">
                {{ item.id }} {{ item.objclass }}                
            </li>
        </ul>
        <!-- getting the class from the class specified in the object -->
        <p :style="changestyle">this is my static style</p>
        <!-- style from const style object -->
    </div>

    <div>
        <h1>Part 6 - Conditional Rendering</h1>
        <div>
            <button @click="myToggle = !myToggle">toggle me</button>
            <p v-if="myToggle">you can see this if toggle</p>
        </div>
        <div>
            <ul>
            <li v-for="i in myPart6Obj"> {{ i }} </li>
            <!-- get the values stored in the part6 object into a list -->
            <li v-for="i in 5"> the number is: {{ i }}</li>
            <!-- show a range of numbers -->
            </ul>
        </div>
        <div>
            <ul>
                <template v-for="i in myPart6Obj">
                <li> {{ i }}</li>
                <li> this is a template</li>
                <li> all the parts are the same</li>
                </template> 
            </ul>         
            <!-- using vfor on a template -->
        </div>
        <div>
            <p v-for="i in 10">
                <p v-if="i % 2">
                    {{ i }} is %2
                </p>
            </p>
            <!-- vfor with a vif loop inside to check if the number is %2 -->
        </div>
            <Part6Component/>
        <!-- imported my component and using its functionality -->
        <div>
            <li v-for="i in 5" > button {{ i }} <Part6Component/> </li>
        </div>
        <!-- using my imported component in vfor loop to get a heap of the component for different objects -->
        <div>
            <Part6Component2 
            v-for="(item, index) in myPart6Obj2"
            :id="item.id"
            :name="item.name"
            :index="index"
            :key="item.id"/>
            <!-- using the layout from the component for the obects in the lsit -->
            <!-- item id and name are specified by me, the index is its place in the list -->
        </div>
    </div>

    <div>
        <h1>Part 7 - Event Handlers</h1>
        <div>
            <button @click="eventclicker++">event-click</button>
            the value is: {{ eventclicker }}
            <!-- inline event handling click actions on the button -->
        </div>
        <div>
            <button @click="dontClick" >dont click me</button>
            <!-- clicking causes function to show an alert message on the page -->
            <br>
            <button @click.ctrl.exact="ctrlClick">hold control and click me</button>
        </div>
    </div>

    <div> 
        <h1>Part 8 - Form Input Bindings</h1>
        <div>
            <input v-model.lazy="userInput"> put some input <br> 
                <p> you entered {{ userInput }}</p>
            <!-- lazy input so the update only appears after the user has finished inputting data -->
            <input v-model="userCheckbox" type="checkbox" > check it<br>
            <input type="radio" value="One" v-model="userRadio"> radio it<br>
            <input type="radio" value="Two" v-model="userRadio"> dont radio it<br>
            <select v-model="userSelect">
                <option disabled value="">select a letter</option>
                <option>A</option>
                <option>B</option>
                <option>C</option>
            </select><br>
            <textarea v-model="userTextarea"> type in some text</textarea>
            <button @click="adduserchoice">update choices</button>

            <p v-for="i in userChoices"> {{ i }} </p>
            <!-- gets a bunch of info from the user form, saves it into an object and iterates through it -->
            <input v-model.trim="trimput" />Userinput trimmed: {{ trimput }} 

            <input v-model="userNumber" /> number * 7 = {{ userNumber * 7  }}
        
        </div>
    </div>

    <div>
        <h1>Part 9 - Watchers</h1>
        <div>
            <p>question api answering your questions</p>
            <p>Ask a yes/no question:
                <input v-model="question" />
            </p>
            <p>{{ answer }}</p>

        </div>

        <div> 
            <input v-model="timerUser"/> type something to see the time update 
            <p>{{ returnedTime }}</p>
        </div>
        <!-- setting a watcher to update the current time when the user enters something into the input field -->
        <div>
            <button @click="changeUpdaterChoice">auto update time?</button>
            {{ updaterChoice }}
            <p> auto time?: {{ autoupdatetime }}</p>
        </div>
    </div>

    <div>
        <h1>Part 10 - Components</h1>
        <div>
            <div :style="{ 'color': emitColour }">
                <Part10Component
                :myprops="myProps"
                @changeColourChild="changeColour"
                /> parent changing colour
                <button @click="changeColour">change colour</button>
                <!-- The changeColourChild call is emitted from the child component, and causes the colour to be changed -->
            </div>
        </div>
        <div>
            <div>
                no content to Slot <br>
                <Part10SlotComponent></Part10SlotComponent>
            </div>
            <div>
                content to slot <br>
                <Part10SlotComponent>
                    content from parent
                    <template #named-slot> named slot</template>
                    <template #named-slot2> named slot 2</template>

                </Part10SlotComponent>
            </div>
        </div>
        <div>
            <a href="/part10router"> route ?</a>
            <RouterLink to="/part10router">Task View</RouterLink>
            <router-link to="/part10router">Go to part 10</router-link>
            <br>
            <router-view to="/part10router">Go to part 19</router-view>
        </div>
    </div>  


    </div>

</template>

<script setup >

import { computed, ref } from 'vue'

const msg = ref('this is my message')

const myHtml = ref('<span style="color: red">this is my script html</span>')

const myMessage = ref({
    id: 1,
    content: 'my vbind message',
    })

const num = ref(1)

const myList = [1, 2, 3, 4, 5, 6,]

const mylistx3 = computed(() => {
    return myList[3] * 7 > 5
}
)


import counter from '../components/PartThreeComponent.vue'

import { reactive } from 'vue'

const state = reactive({ count: 0 })


const myObjects = ref([
        {id:1, boring: true, veryBoring:false, objclass: 'object-class'}, 
        {id:2, boring:false, veryBoring:false, objclass: 'object-class'}, 
        {id:3, boring:true, veryBoring: true, objclass: 'object-class'}])

function changeBoring(item) { 
    item.boring = !item.boring
}

const changestyle = ref({
    color: "blue",
    fontSize: "30pt"
})

// Part 6
const myToggle = ref(true)

const myPart6Obj = ref({id:1, name:'john'})

import Part6Component from '../components/Part6Component.vue';
import Part6Component2 from '../components/Part6Component2.vue';

const myPart6Obj2 = ref([{id:1, name:'john'}, {id:2, name: 'jane'}])


//part7
const eventclicker = ref(0)

function dontClick() {
    alert('no click!')
}

function ctrlClick() {
    alert('control click detected, harddrive encryption initiated')
}

//part 8

const userInput = ref('')
const userCheckbox = ref()
const userRadio = ref()
const userSelect = ref()
const userTextarea= ref('')

const userChoices = ref([])

function adduserchoice(){
    userChoices.value.push({
    input: userInput.value,
    checkbox: userCheckbox.value,
    radio: userRadio.value,
    selected: userSelect.value,
    textarea: userTextarea.value,
})
}

const trimput = ref('')
const userNumber = ref(0)

//Part 9 

import { watch } from 'vue';

const question = ref('')
const answer = ref('Questions usually contain a question mark. ;-)')

// watch works directly on a ref
watch(question, async (newQuestion, oldQuestion) => {
  if (newQuestion.indexOf('?') > -1) {
    answer.value = 'Thinking...'
    try {
      const res = await fetch('https://yesno.wtf/api')
      answer.value = (await res.json()).answer
    } catch (error) {
      answer.value = 'Error! Could not reach the API. ' + error
    }
  }
})

const timerUser = ref('')
const returnedTime = ref('')

watch(timerUser, async (newTime, oldTime) => {
    // if (newTime)
    try {
        const thetime = await fetch('http://worldtimeapi.org/api/timezone/Australia/Brisbane')
        returnedTime.value = (await thetime.json()).datetime
    } catch (error) {
        returnedTime.value = "couldnt connect to the time" + error
    }
})

const autoupdatetime = ref('')
const updaterChoice = ref(true)

function changeUpdaterChoice(){
    updaterChoice.value = !updaterChoice.value
}

watch(updaterChoice, async (newTime, oldTime) => {
    while (updaterChoice){
    try {
        const response = await fetch('http://worldtimeapi.org/api/timezone/Australia/Brisbane/')
        autoupdatetime.value = (await response.json()).datetime
    } catch (error) {
        autoupdatetime.value = "some kinda error " + error
    }}

})

//Part 10 - Components
import Part10Component from '../components/Part10Component.vue';

const myProps = ref("sent from parent")
const emitColour = ref('red')

function changeColour(){
    if (emitColour.value == 'red'){
        emitColour.value = 'green'
    }
    else { emitColour.value = 'red' }
}

import Part10SlotComponent from '../components/Part10SlotComponent.vue'


// const part10router = { template: '<div>Part10Route <h1>is it part 10?</h1></div>'}
// const routes = [
//     { path: '/part10router', name: 'part10router', component: part10router},
//     ]
// const router2 =  new VueRouter({
//     routes
// })
// const app2 = new Vue({
//   router2
// }).$mount('#app2')




</script>


<style scoped>
.my-class {
    background-color: black;
}

.fancy-span {
    color: pink;
}

.boring {
    background-color: brown;
    color: beige;
}
.twoerrors {
    color: red;
}

.object-class{
    color: green;

}

.component10-controlled{
    background-color: yellow;
    color: black;

}

</style>