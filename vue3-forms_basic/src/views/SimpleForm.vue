<template>
    <div>
      <h1>Create an event</h1>
      <form @submit.prevent="sendForm">
  
        <BaseSelect
            :options="categories"
            v-model="event.category"
            label="Select a category"
        />
  
        <h3>Name & describe your event</h3>
        
        <BaseInput
            v-model="event.title"
            label="Title"
            type="text"
        />

        <BaseInput
            v-model="event.description"
            label="Description"
            type="text"
        />
  
        <h3>Where is your event?</h3>

        <BaseInput
            v-model="event.location"
            label="Location"
            type="text"
        />
  
        <h3>Are pets allowed?</h3>
        <div>
          <!-- base-radio comp here -->
          <BaseRadioGroup
                v-model="event.pets"
                name="pets"
                :options="petOptions"
            />
        </div>
  
        <h3>Extras</h3>
        <!-- base-checkbox comp -->
        <div>
            <BaseCheckbox
            v-model="event.extras.catering"
            label="Catering"
            />
        </div>

        <div>
            <BaseCheckbox
            v-model="event.extras.music"
            label="Music"
            />
        </div>
  
        <button class="button -fill-gradient" type="submit">Submit</button>
      </form>
    </div>
</template>
  
<script lang="js">
import axios from "axios";
import BaseCheckbox from '../components/BaseCheckbox.vue';
import BaseInput from '../components/BaseInput.vue';
import BaseRadio from '../components/BaseRadio.vue';
import BaseRadioGroup from '../components/BaseRadioGroup.vue';
import BaseSelect from '../components/BaseSelect.vue';

  export default {
    components: {
        BaseInput,
        BaseSelect,
        BaseCheckbox,
        BaseRadio,
        BaseRadioGroup
    },
    data () {
      return {
        categories: [
          'sustainability',
          'nature',
          'animal welfare',
          'housing',
          'education',
          'food',
          'community'
        ],
        event: {
          category: '',
          title: '',
          description: '',
          location: '',
          pets: 1,
          extras: {
            catering: false,
            music: false
          }
        },
        petOptions: [
            { label: 'Yes', value: 1},
            { label: 'No', value: 0},
        ]
      }
    },
    methods: {
        sendForm() {
            axios.post(
                'https://my-json-server.typicode.com/Code-Pop/Vue-3-Forms/events',
                this.event
            )
            .then(function (response) {
                console.log('Response', response);
            })
            .catch(function (err) {
                console.log('Error', err);
            })
        }
    }
  }
</script>