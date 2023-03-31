<script>
export default {

    //json passed from app
    props: {
        plantJson: { 
            type: Object
        },
        animalJson: {
            type: Object
        },
    },
    data() {
        return {
            currentButtons: [],
            firstTier: true,
            index: 1,
            objectToUse: Object
        }
    },
    methods: {
        handleClick(type) {
            //assigns json object to use for button labels
            if(type == "plant") {
                this.objectToUse = this.plantJson
                this.firstTier = false
            } else if(type =="animal") {
                this.objectToUse = this.animalJson
                this.firstTier = false
            } else {
                console.log(this.objectToUse[this.index-1][0].noNextTier)
            }
            indexChecker = this.index

            if(indexChecker != 1){
                indexChecker -= 1
            }
            //handles menu when no next set of options available
            if((!this.objectToUse[indexChecker][0].noNextTier)) {
                //deletes old buttons
                for(let y=0; y < this.currentButtons.length; y++) {
                    for(let x=0; x < this.objectToUse[this.index].length; x++) {
                        if(this.objectToUse[this.index][x].label != this.currentButtons[y]) {
                            this.currentButtons.splice(y)
                        } 
                    } 
                }
                //adds new labels to the buttons array
                for( let i=0; i < this.objectToUse[this.index].length; i++) { 
                    this.currentButtons.push(this.objectToUse[this.index][i].label)
                }     
                this.index +=1
            } else { this.handleDisplay()}
        },
        handleDisplay() {
            console.log('handle')
        },
        //handles the backbutton
        handleBack() {
            console.log(this.animalJson.cat[0].label)
            for(let x=0; x < this.currentButtons.length; x++) {
                this.currentButtons.splice(x)
            }
            this.index = 1
            this.firstTier = true
        }
    },
}
//the html for the buttons. If the user has pressed no buttons, the first two buttons are displayed
</script>
<template>
    <div>
        <button v-if="firstTier" @click="handleClick('plant')"> {{plantJson.cat[0].label}}</button>
        <button v-if="firstTier" @click="handleClick('animal')"> {{animalJson.cat[0].label}}</button>
        <button id="btn-group" v-for="label in currentButtons" @click=handleClick()>
            {{ label}}
        </button>
        <button v-if="!firstTier" id="btn-back" @click="handleBack()">Back</button>
    </div>
    
</template>