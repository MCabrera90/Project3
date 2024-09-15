<script setup>
  import {ref} from 'vue'

  //declare variables for contact name, contact number, button, and contact list
  const newName = ref('') //contact name user input
  const newNum = ref('') //contact number user input
  const contactList = ref([]); //contact list

  //function to add item from user input into list
  const addContact = () =>{
    if(newName.value.trim() === ''){
      alert("Input a name to add to the Contact List.")
      return
    }
    else if(newNum.value.trim() === ''){
      alert("Input a phone number to add to the Contact List.")
      return
    }
    else if(newName.value.trim() === '' || newNum.value.trim() === ''){
      alert("Input a name and phone number to add to the Contact List.")
      return
    }
    contactList.value.push({
      contact: newName.value,
      number: newNum.value,
    })
    newName.value = ''
    newNum.value = ''
  }
  
  const removeContact = (item) =>{
    contactList.value = contactList.value.filter(Element => Element !== item)
  }
</script>

<template>
  
    <section class="content">
        <div>
        <h1 class="main-title">Create A Contact List</h1>
        <h2>Enter a name and a phone number.
            <br><br>Then click on "Add Contact" to add them to a list</h2>
        </div>

        <div>
          <form @submit.prevent = "addContact">
          <h4>Contact Name</h4>
          <input type="text" placeholder="e.g., John Doe" v-model="newName"/>
          <h4>Phone Number</h4>
          <input type="text" placeholder="e.g., 1234567890" v-model="newNum" onkeypress="return /[0-9]/i.test(event.key)"/>   
      
          <br><br><input type="submit" value="Add Contact"/>

          </form>
        </div>

        <h2>Contact List</h2>
        <h4>Click "Delete Contact to remove a contact from the list"</h4>
        <div class= "list">
          <ul>
            <li v-for="item in contactList" :key="item.id">{{item.contact}} - {{item.number}}
              <button type="button" @click="removeContact(item)">Delete Contact</button>
            </li>
          </ul>
        </div>
        
    </section>
  
</template>


